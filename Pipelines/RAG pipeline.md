# 🚀 Large-Scale RAG on Azure — Architecture & Deployment Guide

This guide shows how to design, deploy, and scale an **enterprise-grade Retrieval-Augmented Generation (RAG)** pipeline on **Microsoft Azure** using **Azure AI Search (vector + hybrid)**, **Azure OpenAI**, **Azure Kubernetes Service (AKS)** or **Container Apps**, and secure-by-default patterns (Private Endpoints, Managed Identity, Key Vault).

---

## 1) Reference Architecture (High Level)

```text
+----------------------+           +--------------------------+
|  Clients (Web/API)   |  HTTPS    |  Azure Front Door /      |
|  Web, Mobile, Bot    +---------->+  Application Gateway     |
+----------+-----------+           +--------------------------+
           |                                   |
           | mTLS/HTTPS                        | Private Link
           v                                   v
+---------------------------+        +--------------------------+
|  App Layer (AKS or ACA)   |<------>|  Azure OpenAI (Chat/Emb) |
|  API, Orchestrator, Cache |  MI    +--------------------------+
|  (e.g., FastAPI)          |        +--------------------------+
+------------+--------------+        |  Azure AI Content Safety |
             |                       +--------------------------+
             | (SDK/REST)                       ^
             v                                   |
+---------------------------+         +----------+---------------+
| Azure AI Search (Vector + |<--------+  Azure Storage / ADLS    |
| Hybrid + Semantic Ranker) |  Index  |  (raw docs, chunks)      |
+------------+--------------+         +----------+---------------+
             ^                                   |
             |  Indexers / ETL (Event-Driven)    |
             |                                   v
+---------------------------------------------------------------+
|  Ingestion: Functions / ADF / Synapse / Data Factory / DLT    |
|  + Azure AI Document Intelligence (OCR, tables, KV)           |
+---------------------------------------------------------------+

Legend:
- MI = Managed Identity
- ACA = Azure Container Apps

```

**Why this design?**  
- **Hybrid retrieval (BM25 + vector)** + **Semantic ranker** → reliable relevance & citations.  
- **Stateless app layer** on AKS/ACA → horizontal scale & resilience.  
- **Event-driven ingestion** + **Document Intelligence** → robust, automated indexing.

---

## 2) Core Azure Services & Roles

- **Azure AI Search**: Vector indexes, hybrid search, semantic ranker, filters/facets.  
- **Azure OpenAI**: Chat/completions + embeddings for chunk vectors.  
- **Azure Storage/ADLS**: Durable store for raw docs & chunk JSON.  
- **Compute (AKS or Container Apps)**: Hosting the RAG API/app & workers.  
- **Azure AI Document Intelligence**: OCR, layout, tables, key-value extraction for PDFs/scans.  
- **Azure Key Vault**: Secrets/keys; integrate with **Managed Identity**.  
- **Networking**: VNet + **Private Endpoints** for Search/OpenAI/Storage.  
- **Observability**: Azure Monitor + **Application Insights** for traces/metrics.  

---

## 3) Retrieval Strategy (What “Good” Looks Like)

- **Chunking**: ~500–1,500 tokens, overlap 50–150 depending on doc style.  
- **Embeddings**: Use Azure OpenAI embeddings endpoint; store vectors in AI Search.  
- **Hybrid retrieval**: Combine **text** (BM25) + **vector** in a single query.  
- **Reranking**: Enable **Semantic ranker** for better relevance.  
- **Metadata filters**: Scope by tenant, source, doc_type, time, access policy.  
- **Citations**: Return doc ids/sections + highlights for auditability.

---

## 4) Deployment Options

### Option A: **Azure Kubernetes Service (AKS)**
- For **very high scale**, custom autoscaling, mixed workloads.
- Use **HPA** for pod autoscale and **Cluster Autoscaler** for nodes.
- Add **Dapr** or a service mesh if you need sidecar patterns, mTLS, retries.

### Option B: **Azure Container Apps (ACA)**
- Simpler serverless containers with **KEDA-based autoscale** (HTTP/concurrency/queues).
- Great for **event processors** (ingestion, reindexing) and **API** with bursty traffic.

**Note:** Azure App Service also works for simpler RAG apps; AKS/ACA are better for sustained scale.

---

## 5) Step-by-Step: Build the Pipeline

### 5.1 Ingest & Preprocess
1. Land raw docs in **Blob Storage / ADLS**.  
2. Run **Document Intelligence** (Layout/General Document) → pull **text, tables, key-values**.  
3. Clean & **chunk** content (preserve source/page/coordinates for citations).  
4. Generate **embeddings** (Azure OpenAI) for each chunk.  
5. Upsert to **Azure AI Search** vector index with metadata.

### 5.2 Index Design (Azure AI Search)
- Fields: `id`, `content`, `content_vector`, `title`, `source`, `page`, `tags`, `created_at`, `tenant_id`.  
- Enable **vector profile** (cosine/ dotprod), **searchable** text, **filterable** metadata.  
- Turn on **Semantic ranker** and store **captions** if you want semantic answers in results.

### 5.3 Query Flow (at runtime)
1. User question → **App** calls embeddings (optional: or use query-time embedding cache).  
2. **Hybrid query** (BM25 + vector) → Azure AI Search; apply **filters**; top-k ~20.  
3. **Semantic ranker** → rerank to top-n (e.g., 8).  
4. **Context builder** → assemble concise context with citations & safety checks.  
5. **Azure OpenAI** chat completion → grounded answer + citations.  
6. Optional: **Response caching** (Redis) keyed by normalized prompt + filter set.

---

## 6) Scaling Patterns

- **Index throughput**: Raise Search service **replicas/partitions** during bulk loads; keep **replicas ≥3** for HA.  
- **Compute autoscale**:  
  - **AKS**: Use **HPA** (CPU/RAM/QPS) + **Cluster Autoscaler**.  
  - **ACA**: Scale on **HTTP RPS**, **concurrency**, or **queue length**.  
- **Async pipelines**: Use **Event Grid + Functions/ACA jobs** for ingest/reindex.  
- **Sharding**: Separate indexes per tenant/domain to control blast radius.  
- **Caching**: Redis for embeddings and RAG results to reduce token/latency cost.

---

## 7) Security & Networking

- **Managed Identity (MI)** everywhere; no secrets in code.  
- **Key Vault** for any required secret; enable **soft delete + purge protection**.  
- **Private Endpoints** for AI Search, OpenAI, Storage; **deny public network access**.  
- VNet-integrate your compute; egress through **private DNS zones**.  
- **RBAC/ABAC**: Enforce tenant/role filters at query time (e.g., `tenant_id eq '{tid}'`).  
- **Content Safety**: Optionally run user prompts and retrieved text through safety checks.

---

## 8) Observability & SRE

- **Application Insights**: traces, dependency calls (OpenAI/Search/Storage), live metrics, failures.  
- **Azure Monitor**: container CPU/mem, node pressure, HPA metrics, logs.  
- **Budget/Quota** Alerts**: watch token usage (OpenAI), query units (Search), storage egress.  
- **Quality dashboards**: retrieval hit rates, MRR@n, groundedness, hallucination flags, latency p50/p95/p99.

---

## 9) Minimal IaC (Bicep) — AI Search + Private Endpoint (starter)

```bicep
param location string = resourceGroup().location
param searchName string
param vnetId string
param subnetId string

resource search 'Microsoft.Search/searchServices@2024-09-01' = {
  name: searchName
  location: location
  sku: { name: 'standard' } // consider 'standard3'/'storage_optimized'
  properties: {
    partitionCount: 1
    replicaCount: 3
    publicNetworkAccess: 'Disabled'
    authOptions: { aadOrApiKey: 'aadOnly' }
    networkRuleSet: { ipRules: [] }
    semanticSearch: { configuration: 'standard' } // enable semantic ranker
  }
}

resource pe 'Microsoft.Network/privateEndpoints@2023-09-01' = {
  name: '${searchName}-pe'
  location: location
  properties: {
    subnet: { id: subnetId }
    privateLinkServiceConnections: [{
      name: 'search-pe-conn'
      properties: {
        privateLinkServiceId: search.id
        groupIds: ['searchService']
      }
    }]
  }
}
```

10) App Snippets
10.1 Hybrid Retrieval (pseudocode)
```python
def retrieve(client, query, embedding):
    return client.search(
        vector={"value": embedding, "k": 20, "fields": "content_vector"},
        search=query,                              # BM25
        queryType="semantic",
        semanticConfiguration="default",
        select="id,title,content,source,page,tags",
        filter="tenant_id eq 'acme'",              # RBAC/tenancy filter
    )
```

10.2 Guarded Generation (pseudocode)
```python
def generate(openai, user_msg, passages):
    system = "Answer using only the provided context. Cite sources."
    context = "\n\n".join(
        [f"[{p['id']} p{p['page']}] {p['content'][:1200]}" for p in passages]
    )
    prompt = f"{system}\n\nContext:\n{context}\n\nUser: {user_msg}\nAssistant:"
    return openai.chat_completions(model=EMBEDDED_LLM, messages=[{"role":"user","content":prompt}])
```

11) Testing & Quality
- Retrieval evals: MRR@k, nDCG, Recall@k on labeled Q/A.
- A/B: Compare chunk sizes, top-k, rerank strategies, prompt variants.
- Drift: Track embedding model updates; re-embed in the background with dual-write.
- Latency SLOs: Set budgets e2e (p95), then budget per stage (embed, search, rerank, LLM).

12) Cost Controls
- Right-size Search partitions/replicas; scale out during bulk index only.
- Cache embeddings and final answers; dedupe identical embeddings requests.
- Use smaller chat models for most traffic; escalate to larger for complex queries.
- Compress/pack chunks (remove boilerplate) to reduce tokens.

13) Runbooks (Ops)
- Backfill/reindex: queue-based workers (ACA Jobs) to rebuild vectors or add new fields.
- Failover: Multi-region active/active for Search + OpenAI with traffic manager.
- Quotas: Pre-request capacity for OpenAI deployments used at peak.

14) Useful Docs (for deeper dives)
- Azure’s RAG overview and implementation patterns with AI Search.
- Semantic ranker for better relevance.
- Vector & hybrid search in AI Search.
- OpenAI on your data (RAG) in Azure AI Foundry.
- Private Endpoints for AI Search.
- Managed Identity best practices.
- AKS autoscaling (HPA + Cluster Autoscaler) and monitoring with App Insights.
- Document Intelligence (Layout, General Document) for OCR/structure.

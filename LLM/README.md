# 📘 LLM Study Plan

This folder contains structured notes, guides, and hands-on materials for learning **Large Language Models (LLMs)** and their ecosystem. The goal is to build strong conceptual foundations, practical skills, and interview-ready knowledge.

---

## 🎯 Objectives
- Understand the **core concepts** behind LLMs and their applications.
- Learn practical techniques like **prompt engineering, fine-tuning, RAG, and evaluation**.
- Build a strong **portfolio of projects** showcasing LLM applications.
- Prepare for **interview questions** related to LLMs and applied NLP.

---

## 📂 Folder Structure
```
LLM/
│── README.md               # Study plan (this file)
│── PromptEngineering.md    # Techniques for crafting effective prompts
│── FineTuning.md           # Approaches: LoRA, PEFT, full finetuning
│── RAG.md                  # Retrieval-Augmented Generation concepts & pipeline
│── Evaluation.md           # LLM evaluation metrics and methods
│── Safety.md               # Bias, hallucination, prompt injection defense
```

---

## 🗓️ Study Plan

### Week 1: Foundations of LLMs
- What are LLMs? How do they differ from smaller NLP models?
- Key transformer review (link to Transformer folder).
- Learn **tokenization, embeddings, and scaling laws**.
- Read about **zero-shot, few-shot, and fine-tuned LLMs**.

---

### Week 2: Prompt Engineering & Control
- Techniques: role prompting, chain-of-thought, self-consistency.
- Learn to design prompts for:
  - Q&A
  - Summarization
  - Reasoning
- Explore **LangChain basics** for chaining prompts.

---

### Week 3: Fine-Tuning Approaches
- Full model finetuning (resource-heavy).
- Parameter-efficient finetuning: **LoRA, PEFT, Adapters**.
- Practice: finetune a small LLaMA/Flan-T5 model on a custom dataset.

---

### Week 4: RAG & Evaluation
- Study **RAG.md** → build a pipeline using vector databases (FAISS/Qdrant).
- Implement retrieval + LLM generation on a custom dataset.
- Evaluate:
  - **Retrieval**: recall@k, MRR
  - **Generation**: accuracy, hallucination rate, BLEU/ROUGE
- Write an **evaluation.md** with key learnings.

---

### Week 5: Safety & Deployment
- Risks: hallucinations, bias, prompt injection.
- Mitigations: grounding, safety filters, monitoring.
- Explore LLM deployment: APIs, serving with FastAPI, Docker.
- Build a mini-project: **safe RAG chatbot with citations**.

---

## 📌 Projects to Include
- Prompt-engineered Q&A bot
- Fine-tuned summarizer
- RAG-powered chatbot with vector DB
- LLM evaluation dashboard
- Safe deployment with filters & monitoring

---

## 📝 Interview Prep Questions
- What is RAG and why is it useful?
- How would you evaluate an LLM?
- Difference between prompt engineering and finetuning?
- How do you mitigate hallucinations?
- Tradeoffs between dense, sparse, and hybrid retrieval?

---

## ✅ Key Takeaways
- LLMs are powerful but need **grounding, evaluation, and safety checks**.
- Practical knowledge of **RAG, prompt engineering, and finetuning** is essential for ML/AI interviews.
- Building hands-on **projects** demonstrates applied understanding.

---

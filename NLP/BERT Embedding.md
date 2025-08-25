# 🧠 BERT Embeddings

## 📌 Introduction
**BERT (Bidirectional Encoder Representations from Transformers)** is a transformer-based model developed by Google.  
It learns **contextual word embeddings** by looking at words **in both directions (left & right context)**, unlike Word2Vec or GloVe which create static embeddings.

- **Static embeddings** (Word2Vec, GloVe): each word has one vector, regardless of context.  
- **BERT embeddings**: the same word can have **different embeddings** depending on its sentence context.  

Example:  
- "He went to the **bank** to deposit money." → **bank = financial institution**  
- "The boat is near the **bank** of the river." → **bank = river side**  

---

## ⚙️ How BERT Generates Embeddings
1. Input text is **tokenized** using **WordPiece tokenizer**.  
2. Special tokens are added:
   - `[CLS]` → classification token at start.  
   - `[SEP]` → separator between sentences.  
3. Text is passed through **transformer layers** → contextualized embeddings.  
4. Embeddings can be extracted for:
   - Each **token** (word/subword).  
   - The entire **sentence/document** (often from `[CLS]` token or pooled output).

---

## 🔑 Types of BERT Embeddings
- **Token embeddings**: vector representation for each token in the input.  
- **Sentence embedding**: aggregated vector for the entire sentence.  
- **CLS embedding**: the embedding of `[CLS]` token (often used for classification tasks).  
- **Pooled output**: mean/max pooling across all token embeddings.

---

## 📊 Example in Python (Hugging Face Transformers)

```python
from transformers import BertTokenizer, BertModel
import torch

# Load pre-trained BERT model + tokenizer
tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")
model = BertModel.from_pretrained("bert-base-uncased")

# Input text
text = "BERT embeddings capture context."

# Tokenize & convert to tensor
inputs = tokenizer(text, return_tensors="pt")

# Forward pass through BERT
with torch.no_grad():
    outputs = model(**inputs)

# Extract embeddings
last_hidden_state = outputs.last_hidden_state   # shape: [batch, tokens, hidden_dim]
cls_embedding = last_hidden_state[:, 0, :]      # [CLS] token embedding
sentence_embedding = last_hidden_state.mean(dim=1)  # mean pooling across tokens

print("CLS Embedding shape:", cls_embedding.shape)          # [1, 768]
print("Sentence Embedding shape:", sentence_embedding.shape) # [1, 768]
```

## ✅ Applications of BERT Embeddings
- Text classification (sentiment, spam detection).
- Named Entity Recognition (NER).
- Semantic search / Information retrieval.
- Question Answering.
- Clustering & document similarity.

## 🚀 Summary
- BERT embeddings are contextual (same word = different meaning in different sentences).
- Use [CLS] or mean pooling for sentence-level embeddings.
- Hugging Face Transformers makes it easy to generate them.
- These embeddings power many downstream NLP tasks and are foundational in modern NLP.

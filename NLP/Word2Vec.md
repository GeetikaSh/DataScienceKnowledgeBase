# 🧠 Word2Vec: CBOW vs Skip-Gram

## What is Word2Vec?
**Word2Vec** is a technique to represent words as **dense vectors (embeddings)**.  
Unlike Bag of Words or TF-IDF, it captures **semantic meaning** of words.

- Words with similar meanings are **close in vector space**.
- Famous example: king - man + woman ≈ queen

---

## How Word2Vec Works

Word2Vec is a **shallow neural network** that learns word embeddings based on context.  
It predicts relationships between words using surrounding text.  

Word2Vec has two main architectures:

### 1. Continuous Bag of Words (CBOW)
- **Goal:** Predict the **current word** based on its **context words**.  
- Example:  
Context: ["I", **?**, "machine"]  
Model predicts: "love"  

- **Characteristics:**
- Faster to train.
- Works well with **smaller datasets**.
- Focuses on **frequent words**.

---

### 🔹 2. Skip-Gram
- **Goal:** Predict the **context words** given the **current word**.  
- Example:  
Input: "love"  
Model predicts: ["I", "machine", "NLP"]  

- **Characteristics:**
- Slower to train.
- Performs better on **large datasets**.
- Handles **rare words** more effectively.

---

## 🔄 CBOW vs Skip-Gram Comparison

| Feature            | CBOW                              | Skip-Gram                          |
|--------------------|-----------------------------------|------------------------------------|
| **Prediction Task**| Word from context                 | Context from word                   |
| **Training Speed** | Faster                            | Slower                              |
| **Focus**          | Frequent words                    | Rare words                          |
| **Dataset Size**   | Works well on small datasets      | Better on large datasets            |
| **Use Case**       | Quick training, frequent words    | Rich embeddings, rare words         |

---

## 🚀 Summary
- **CBOW**: Good when you have a **smaller dataset** and want **faster training**.  
- **Skip-Gram**: Better when you have a **large dataset** and need to capture **rare word meanings**.  
- Both methods produce **word embeddings** that are foundational for modern NLP models like **BERT and GPT**.

## 📊 Example in Python (Gensim)

```python
from gensim.models import Word2Vec

# Example corpus
sentences = [
  ["i", "love", "nlp"],
  ["i", "love", "machine", "learning"],
  ["word2vec", "creates", "embeddings"],
  ["embeddings", "capture", "semantic", "meaning"]
]

# Train CBOW model (sg=0)
cbow_model = Word2Vec(sentences, vector_size=50, window=3, min_count=1, sg=0)

# Train Skip-Gram model (sg=1)
skip_model = Word2Vec(sentences, vector_size=50, window=3, min_count=1, sg=1)

# Check similarity
print("Similarity:", cbow_model.wv.similarity("nlp", "machine"))
print("Most similar:", skip_model.wv.most_similar("embeddings"))
```

## Applications of Word2Vec
- Semantic search (find related terms).
- Recommendation systems (e.g., product embeddings).
- Clustering similar words or documents.
- Input features for downstream ML/NLP models.


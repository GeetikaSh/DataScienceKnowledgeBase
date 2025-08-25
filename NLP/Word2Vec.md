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

## 🔑 Key Parameters
1. sentences
- Input training data.
- A list of tokenized sentences:
- [["i", "love", "nlp"], ["word2vec", "creates", "embeddings"]]

2. vector_size (default=100)
- Dimensionality of the word embeddings.
- Higher values → capture more semantic features, but increase memory & training time.
- Typical range: 100–300.

3. window (default=5)
- Maximum distance between current word and context words.
- Larger → broader context; smaller → narrower/local context.

4. min_count (default=5)
- Ignores words with frequency < min_count.
- Helps remove noise from rare words.
- Example: min_count=1 keeps all words.

5. sg (default=0)
- Training algorithm:
  - sg=0 → CBOW (faster, frequent words).
  - sg=1 → Skip-Gram (better for rare words, large datasets).

6. hs (default=0)
- Hierarchical softmax:
  - hs=1 → use hierarchical softmax.
  - hs=0 → use negative sampling.

7. negative (default=5)
- Number of negative samples (when hs=0).
- Typical range: 5–20.
- Higher values → better accuracy, slower training.

8. epochs (default=5)
- Number of passes (iterations) over the corpus.
- More epochs → stronger embeddings, but risk of overfitting.

9. workers
- Number of threads for training.
- Use number of CPU cores available for speed.

10. seed
- Random seed for reproducibility.

**⚡ Additional Parameters**
- alpha → Initial learning rate (default 0.025).
- min_alpha → Final learning rate after training.
- max_vocab_size → Restrict vocabulary size (helps with large corpora).
- sample → Threshold for subsampling frequent words (default 1e-3).
- compute_loss → If True, reports loss during training.
- callbacks → Custom callbacks for logging/progress.


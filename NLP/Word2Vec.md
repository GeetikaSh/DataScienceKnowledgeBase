# 🧠 Word2Vec: CBOW vs Skip-Gram

## 📌 What is Word2Vec?
**Word2Vec** is a technique to represent words as **dense vectors (embeddings)**.  
Unlike Bag of Words or TF-IDF, it captures **semantic meaning** of words.

- Words with similar meanings are **close in vector space**.
- Famous example: king - man + woman ≈ queen

---

## ⚙️ How Word2Vec Works
Word2Vec has two main architectures:

### 🔹 1. Continuous Bag of Words (CBOW)
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


# Bag of Words (BoW) - NLP Concept

## 📌 Introduction
The **Bag of Words (BoW)** model is one of the most basic techniques in **Natural Language Processing (NLP)**.  
It represents text data in a way that can be used for machine learning models.  

- It **ignores grammar and word order**.
- Focuses only on **word frequency** (how many times a word appears).
- Represents text as a **vector of word counts**.

---

## 📝 Steps to Build BoW
1. **Tokenization**  
   Break the text into words (tokens).  

```
   Example:  
"I love NLP" - ["I", "love", "NLP"]
```

2. **Build Vocabulary**  
Create a dictionary of all unique words in the corpus.  

```
Example (2 sentences):  
Sentence 1: "I love NLP"
Sentence 2: "I love machine learning"

Vocabulary = ["I", "love", "NLP", "machine", "learning"]
```

3. **Vectorization**  
Represent each sentence as a vector of word counts.  
Sentence 1 → [1, 1, 1, 0, 0]\
Sentence 2 → [1, 1, 0, 1, 1]

---

## 📊 Example in Python
```python
from sklearn.feature_extraction.text import CountVectorizer

# Sample corpus
corpus = [
 "I love NLP",
 "I love machine learning"
]

# Initialize CountVectorizer
vectorizer = CountVectorizer()

# Fit and transform corpus
X = vectorizer.fit_transform(corpus)

# Vocabulary
print("Vocabulary:", vectorizer.get_feature_names_out())

# Bag of Words representation
print("BoW Array:\n", X.toarray())
```

**Output**:
```lua
Vocabulary: ['i', 'learning', 'love', 'machine', 'nlp']
BoW Array:
[[1 1 0 1]
 [1 1 1 0]]
```

---

## ✅ Advantages
Simple and easy to implement.\
Works well for small datasets and text classification.

## ⚠️ Limitations
Ignores grammar and context.\
Leads to high-dimensional vectors for large vocabularies.\
Cannot capture semantic meaning (e.g., "good" vs. "great").

## 🚀 Summary
The Bag of Words model is a foundation of many NLP techniques.
Though limited, it is often used as a baseline model before moving to more advanced techniques like **TF-IDF or Word Embeddings.**

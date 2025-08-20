# TF-IDF (Term Frequency-Inverse Document Frequency)

## **Definition:**  
TF-IDF is a statistical measure used to evaluate how important a word is to a document in a collection or corpus. It combines two metrics:
- **Term Frequency (TF):** How frequently a term appears in a document.
- **Inverse Document Frequency (IDF):** How unique or rare a term is across all documents.

## **Formula:**  
- TF = (Number of times term t appears in a document) / (Total terms in the document)
- IDF = log_e(Total number of documents / Number of documents containing term t)
- TF-IDF = TF × IDF

## **Applications:**
- Feature extraction for text classification
- Information retrieval and search engines
- Keyword extraction

## **Advantages:**
- Simple and effective for many tasks
- Highlights important words in documents

## **Limitations:**
- Does not capture semantic meaning or word context
- Sensitive to noise and irrelevant words

## **Example:**
Suppose the word "data" appears 3 times in a document of 100 words, and in 10 out of 1000 documents in the corpus:
- TF = 3/100 = 0.03
- IDF = log(1000/10) = 2
- TF-IDF = 0.03 × 2

## **Why we take log_e of IDF**
The **logarithm in the IDF** part of TF-IDF reduces the impact of very common words and smooths the scale of values. Using log_e (natural logarithm) helps prevent extremely high IDF scores for rare words and makes the metric more stable and interpretable. It compresses the range of IDF values, ensuring that the difference between common and rare terms.

## **Range of TF-IDF**
**High →** word is frequent in this doc, rare overall (important!)\
**Low →** word is either rare in doc or too common everywhere

The range of TF-IDF values depends on the term frequency (TF) and inverse document frequency (IDF):
- **TF** ranges from 0 (term does not appear) to 1 (term appears in every position in the document).
- **IDF** is always ≥ 0, and increases as the term becomes rarer across the corpus.
    - A value of 0 means the term is either absent from the document or present in all documents (making IDF zero).
    - There is no fixed upper bound, but in practice, TF-IDF values are usually less than 1 for most terms, and higher for very rare terms in short documents.
**Note:** The actual range depends on corpus size, document.

## **Impact of LLMs on TF-IDF**
Large Language Models (LLMs) like BERT, GPT, and their variants have significantly changed how text is represented and processed in NLP:
- **Contextual Understanding:** LLMs generate embeddings that capture word meaning in context, unlike TF-IDF which is purely statistical and ignores semantics.
- **Reduced Reliance on TF-IDF:** Many modern NLP tasks now use LLM-based embeddings instead of TF-IDF for feature extraction, as they provide richer and more informative representations.
- **Limitations of TF-IDF Highlighted:** TF-IDF cannot capture polysemy (same word, different meanings) or context, while LLMs can.
- **Hybrid Approaches:** In some cases, TF-IDF is still used for keyword extraction or as a baseline, but LLMs are preferred for tasks requiring deeper understanding.

## **Summary:**  
LLMs have largely superseded TF-IDF for advanced NLP tasks, offering superior performance by leveraging context and semantics.

## **Python Code**
```python
from sklearn.feature_extraction.text import TfidfVectorizer

# Sample documents
documents = [
    "Data science is fun.",
    "Python is great for data analysis.",
    "TF-IDF is a useful technique in NLP."
]

# Create the TF-IDF vectorizer
vectorizer = TfidfVectorizer()

# Fit and transform the documents
tfidf_matrix = vectorizer.fit_transform(documents)

# Get feature names (words)
feature_names = vectorizer.get_feature_names_out()

# Display TF-IDF values
for doc_idx, doc in enumerate(documents):
    print(f"Document {doc_idx+1}:")
    for word_idx, word in enumerate(feature_names):
        print(f"  {word}: {tfidf_matrix[doc_idx, word_idx]:.3f}")
    print()
```

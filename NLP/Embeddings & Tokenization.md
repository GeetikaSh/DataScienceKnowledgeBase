# Embeddings & Tokenizations: Interview Questions

## What is tokenization in NLP, and why is it important?
Tokenization in NLP is the process of breaking down text into smaller units called tokens, which can be words, subwords, or characters. This step is crucial because most NLP models operate on these tokens rather than raw text. Tokenization enables models to handle text in a structured way, facilitates vocabulary creation, and helps manage issues like out-of-vocabulary words. Proper tokenization improves model performance and is foundational for tasks such as text classification, translation, and language modeling.

## Compare WordPiece, Byte Pair Encoding (BPE), and SentencePiece tokenization methods.

**WordPiece:**  
- Developed for models like BERT.
- Starts with a base vocabulary (characters) and iteratively adds the most frequent subword units based on likelihood maximization.
- Handles out-of-vocabulary (OOV) words by breaking them into known subwords.
- Requires pre-tokenization (usually whitespace).

**Byte Pair Encoding (BPE):**  
- Originally a data compression algorithm, adapted for NLP (used in GPT-2, RoBERTa).
- Starts with a character-level vocabulary and merges the most frequent pairs of symbols iteratively.
- Efficiently handles rare and OOV words by decomposing them into subwords.
- Also requires pre-tokenization (whitespace or punctuation).

**SentencePiece:**  
- Designed to work without pre-tokenization (no need for whitespace splitting).
- Treats the input as a raw stream of characters and learns subword units directly.
- Supports both BPE and unigram language model algorithms.
- Useful for languages without clear word boundaries (e.g., Japanese, Chinese).

**Summary Table:**

| Method        | Pre-tokenization Needed | OOV Handling | Used In      | Notes                                 |
|---------------|------------------------|--------------|--------------|---------------------------------------|
| WordPiece     | Yes                    | Good         | BERT         | Likelihood-based merges               |
| BPE           | Yes                    | Good         | GPT-2, RoBERTa| Frequency-based merges                |
| SentencePiece | No                     | Good         | T5, ALBERT   | Works on raw text, supports BPE/unigram|

3. What are the advantages and disadvantages of subword tokenization?
4. How do positional embeddings work, and why are they needed in transformer models?
5. Explain the difference between absolute and rotary positional embeddings.
6. What is the purpose of embeddings in NLP models?
7. How are word embeddings like Word2Vec or GloVe different from contextual embeddings like those in BERT?
8. What challenges arise when handling out-of-vocabulary (OOV) words, and how do modern tokenizers address them?
9. How does tokenization affect downstream NLP tasks and model performance?
10. Can you describe the process of training a custom tokenizer for a new language or domain?
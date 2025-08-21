# Named Entity Recognition (NER) - Notes

**Definition:**  
Named Entity Recognition (NER) is an NLP task that identifies and classifies named entities in text into predefined categories such as person names, organizations, locations, dates, and more.

**What is an Entity?**
An **entity** is a real-world object or concept that can be identified and classified.

**Common Categories:**
- **PERSON** → Names of people (e.g., *Elon Musk*)
- **ORG** → Organizations (e.g., *Google, United Nations*)
- **GPE** → Geo-political entities (e.g., *India, New York*)
- **DATE** → Dates (e.g., *August 20, 2025*)
- **TIME** → Times (e.g., *5:30 PM*)
- **MONEY** → Monetary values (e.g., *$1,000*)
- **PERCENT** → Percentages (e.g., *45%*)

**NER Pipeline Steps:**
1. **Text Preprocessing:** Tokenization, normalization, sentence splitting.
2. **Feature Extraction:** Word embeddings, POS tags, character-level features.
3. **Modeling:** Sequence labeling using models like CRF, BiLSTM, or Transformers (e.g., BERT).
4. **Post-processing:** Entity merging, resolving overlaps, mapping to knowledge bases.

**Approaches to NER**
1. **Rule-based Systems**
   - Use predefined patterns (like regex, dictionaries).
   - Example: A regex to detect phone numbers or email addresses.
2. **Machine Learning-based**
   - Uses algorithms like **Hidden Markov Models (HMMs)**, **Conditional Random Fields (CRFs)**, or **Decision Trees**.
   - Requires manual feature engineering (POS tags, capitalization, etc.).
3. **Deep Learning-based**
   - Uses **RNNs, LSTMs, GRUs, Transformers (BERT, GPT, etc.)**.
   - Automatically learns contextual embeddings.
   - Achieves **state-of-the-art performance**.

**Evaluation Metrics:**
- Precision, Recall, F1-score (often at the entity level).

**Challenges:**
- Ambiguity in entity boundaries.
- Nested and overlapping entities.
- Domain adaptation and low-resource languages.

**Applications:**
- Information extraction
- Question answering
- Knowledge graph construction
- Content recommendation

**Example:**
> Barack Obama was born in Hawaii and served as the President of the United States.

NER Output:
- Barack Obama → PERSON
- Hawaii → GPE
- United States → GPE
- President → TITLE (depending on model)

---

## 📊 Example with spaCy (Python)

```python
import spacy

# Load English NER model
nlp = spacy.load("en_core_web_sm")

# Sample text
doc = nlp("Apple is looking at buying U.K. startup for $1 billion in 2024.")

# Extract entities
for ent in doc.ents:
    print(ent.text, ent.label_)
```

Output:
```
Apple ORG
U.K. GPE
$1 billion MONEY
2024 DATE
```

## Applications of NER
Information Extraction → Extract names, dates, places from documents.
Question Answering → Identify entities in queries.
Chatbots & Virtual Assistants → Understand context from user input.
Search Engines → Improve relevance with entity recognition.
Financial & Legal Domains → Extract company names, contracts, amounts.

## Summary
NER is used to extract structured information from unstructured text.
Entities are classified into categories like PERSON, ORG, GPE, MONEY, DATE.
Modern NER systems rely on deep learning and transformers for high accuracy.
It is a core component of many NLP applications such as chatbots, search engines, and information retrieval.

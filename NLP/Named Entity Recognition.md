# Named Entity Recognition (NER) - Notes

**Definition:**  
Named Entity Recognition (NER) is an NLP task that identifies and classifies named entities in text into predefined categories such as person names, organizations, locations, dates, and more.

**Common Entity Types:**
- Person (PER)
- Organization (ORG)
- Location (LOC)
- Miscellaneous (MISC)
- Date, Time, Money, Percent, etc.

**NER Pipeline Steps:**
1. **Text Preprocessing:** Tokenization, normalization, sentence splitting.
2. **Feature Extraction:** Word embeddings, POS tags, character-level features.
3. **Modeling:** Sequence labeling using models like CRF, BiLSTM, or Transformers (e.g., BERT).
4. **Post-processing:** Entity merging, resolving overlaps, mapping to knowledge bases.

**Popular Approaches:**
- **Rule-based:** Uses patterns and dictionaries.
- **Statistical:** HMM, CRF, Maximum Entropy models.
- **Neural:** BiLSTM-CRF, Transformer-based (BERT, RoBERTa).

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
> "Barack Obama was born in Hawaii."
- Entities: Barack Obama (PER),
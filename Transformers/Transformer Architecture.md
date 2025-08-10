# Transformer Architecture

The Transformer is a neural network architecture introduced in the paper **"Attention Is All You Need"** (Vaswani et al., 2017).  
It is widely used in Natural Language Processing (NLP) and other domains such as computer vision and speech.

---

## 1. Key Characteristics
- **Parallelization**: Unlike RNNs, Transformers do not process tokens sequentially.
- **Attention Mechanism**: Learns relationships between tokens regardless of their distance in the sequence.
- **Scalability**: Suitable for training on large datasets.

---

## 2. High-Level Overview
The Transformer is composed of:
- **Encoder stack**: N identical layers (typically N=6 in the original paper).
- **Decoder stack**: N identical layers (typically N=6).
- **Attention mechanisms**: Self-attention and encoder–decoder attention.
- **Feed-Forward layers**: Applied after attention.
- **Positional encoding**: Provides information about token order.

---

## 3. Encoder
Each **encoder layer** contains:
1. **Multi-Head Self-Attention**:
   - Computes attention for each token with respect to all others in the sequence.
   - Multiple attention heads allow the model to capture different relationships.
2. **Add & Norm**:
   - Residual connection followed by Layer Normalization.
3. **Position-wise Feed-Forward Network**:
   - Two linear transformations with a ReLU activation in between.
4. **Add & Norm** (again after FFN).

---

## 4. Decoder
Each **decoder layer** contains:
1. **Masked Multi-Head Self-Attention**:
   - Prevents attending to future tokens (causal masking).
2. **Add & Norm**.
3. **Encoder–Decoder Attention**:
   - Queries from the decoder attend to the encoder’s output.
4. **Add & Norm**.
5. **Position-wise Feed-Forward Network**.
6. **Add & Norm**.

---

## 5. Attention Mechanism
### Scaled Dot-Product Attention
Given **queries (Q)**, **keys (K)**, and **values (V)**:

$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$
Where:
- \(d_k\) = dimension of keys (used for scaling).
- Softmax ensures weights sum to 1.

### Multi-Head Attention
- Runs multiple self-attention mechanisms in parallel.
- Concatenates outputs and applies a linear transformation.

---

## 6. Positional Encoding
Since the Transformer does not have recurrence or convolution, positional encodings are added to token embeddings:

$PE_{(pos, 2i)} = \sin\left(\frac{pos}{10000^{2i/d_{model}}}\right)$

$PE_{(pos, 2i+1)} = \cos\left(\frac{pos}{10000^{2i/d_{model}}}\right)$
Where:
- `pos` = token position
- `i` = dimension index

---

## 7. Training Objective
- Typically trained using **cross-entropy loss** for sequence prediction tasks.
- Uses **teacher forcing** during training for the decoder.

---

## 8. Applications
- Machine translation
- Text summarization
- Question answering
- Code generation
- Vision Transformers (ViT) for image classification

---

## 9. Diagram (Conceptual)
[Input Tokens] --> [Embedding + Positional Encoding] --> [Encoder Stack] ---> [Decoder Stack] --> [Output Tokens]

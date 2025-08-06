# Transformer Internals

Prepare for deep dives on:
- Multi-head Attention (Scaled Dot-Product)
- Attention masking (causal, padding, span)
- Positional encoding (learned vs. sinusoidal)
- LayerNorm, residuals, FFN structure
- Training transformers from scratch:
    - Initialization strategies
    - Training schedules (cosine, linear decay)
    - Gradient clipping, mixed precision

## 📘 Interview Qs they may ask:
- Walk me through how you would pretrain a language model on structured weather data.
- How would you adapt T5 to take spatio-temporal data as input?
- What issues arise when training a large transformer from scratch on non-text data?
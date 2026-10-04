[Contents](../index.md) · F4 · P3

# Transformer basics

## In one minute

A large language model is a transformer trained to predict the next token. Text is split
into tokens, each token becomes a vector, and stacked layers of self-attention let every
position draw information from every other position. Generation repeats one step: compute
a probability for each possible next token, sample one, append it, and go again.

## Key ideas

- **Tokens.** Sub-word units (byte-pair encoding). Cost and limits are counted in tokens.
  Thai and other non-English text often take more tokens per word.
- **Embeddings and position.** Each token maps to a vector; positional information is
  added because attention itself ignores order.
- **Self-attention.**

  ```
  Attention(Q, K, V) = softmax( Q·Kᵀ / sqrt(d) ) · V
  ```

  Each token forms a query, compares it with every token's key, and takes a weighted
  average of their values. Several heads run in parallel.
- **A layer.** Attention, then a feed-forward network, each with a residual connection
  and normalisation. Dozens of layers are stacked.
- **Decoder-only versus encoder.** GPT-style models read left to right (causal mask) and
  generate. BERT-style encoders read both directions and produce representations for
  classification and embeddings.
- **Training.** Pre-training on next-token prediction over very large text; then
  instruction tuning and alignment from human feedback.
- **Context window.** The maximum number of tokens the model can attend to at once: the
  prompt plus the output.
- **Sampling.**
  - *Temperature*: scales the distribution; 0 is near-deterministic, higher is more
    varied.
  - *Top-p*: sample only from the smallest set of tokens whose probability sums to p.
- **Why it hallucinates.** It produces likely text; nothing in the objective checks
  truth.
- **Why transformers beat recurrent networks.** Parallel training over the sequence and
  direct links between distant positions.
- **Cost.** Attention grows quadratically with sequence length.

## On my CV

Background to the language model bullets. A two-minute explanation is enough.

## Likely questions

1. **What is attention, in plain words?** Each word decides how much to look at each other
   word when building its own representation.
2. **What does temperature do?** Flattens or sharpens the next-token distribution.
3. **BERT versus GPT?** Bidirectional encoder for understanding tasks versus
   left-to-right decoder for generation.
4. **Why is there a context limit?** Compute and memory grow with length, and the model
   was trained up to a maximum.
5. **Senior follow-up: when would you still use a BERT-style model?** High-volume
   classification or embedding where cost and latency matter and labels exist.

## Pitfalls

- Saying the model "looks up" facts.

## Sources

- Vaswani et al., "Attention Is All You Need" (2017): <https://arxiv.org/abs/1706.03762>
- Alammar, "The Illustrated Transformer": <https://jalammar.github.io/illustrated-transformer/>
- 3Blue1Brown, neural networks series (transformers and attention): <https://www.3blue1brown.com/topics/neural-networks>

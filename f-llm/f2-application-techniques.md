[Contents](../index.md) · F2 · P2

# Application techniques

## In one minute

There are three ways to make a language model do a task well, in order of effort: write a
better prompt, give it the right information at query time (retrieval-augmented
generation), or change the model (fine-tuning). Most applications need the first two.
Whatever the technique, the application needs an evaluation set, or improvement is
guesswork.

## Key ideas

- **Prompt engineering.** Clear instructions, context, examples, a stated output format;
  let the model reason before answering for multi-step tasks; split a large task into a
  chain of smaller calls.
- **Retrieval-augmented generation (RAG).**
  1. *Index*: split documents into chunks, embed each, store in a vector index.
  2. *Retrieve*: embed the question, find the nearest chunks.
  3. *Generate*: put the chunks in the prompt and ask the model to answer from them,
     citing sources.
- **Embeddings.** Text mapped to a vector so that similar meaning is close (cosine
  similarity). Approximate nearest-neighbour indexes (HNSW) make search fast.
- **RAG quality levers.** Chunk size and overlap; hybrid search (keyword BM25 plus
  vectors); re-ranking the candidates with a cross-encoder; query rewriting; metadata
  filters.
- **Fine-tuning.** Further training on task examples. Good for style, format or a narrow
  task at lower cost per call; poor for adding facts that change. Parameter-efficient
  methods (LoRA) train small adapters.
- **RAG versus fine-tuning.** Knowledge that changes or must be cited → RAG. Behaviour or
  format → fine-tune. They combine.
- **Hallucination.** Fluent but unsupported output. Reduce with grounding in retrieved
  text, an instruction to say "not found", citations, and checks on the answer.
- **Evaluation.**
  - *Retrieval*: recall@k, MRR on questions with known source passages.
  - *Generation*: faithfulness to the context, answer correctness, by human review or a
    language model as judge (calibrated against humans).
  - Regression set run on every prompt or model change.
- **Operations.** Cost and latency per call, caching, rate limits, logging of prompts and
  outputs, guardrails on input and output, prompt injection.

## On my CV

"Researched techniques for applying large language models, as internal work early in their
adoption" (Sertis, 2023). Be ready to say which techniques I examined and what I
recommended to the team.

**To fill in (only I know):** the two or three findings from that research that I would
still stand by.

## Likely questions

1. **When RAG and when fine-tuning?** As above: facts versus behaviour.
2. **How do you choose chunk size?** By experiment on the evaluation set; small chunks
   retrieve precisely but lose context, large ones the reverse.
3. **How do you reduce hallucination?** Ground, cite, allow "I don't know", verify.
4. **How do you evaluate a RAG system?** Retrieval and generation separately, with a
   fixed question set.
5. **Senior follow-up: a stakeholder wants "a chatbot on our documents" in a month.**
   Scope a narrow use case, build the evaluation set first, ship retrieval with citations,
   and measure before widening.

## Pitfalls

- Fine-tuning to add knowledge that changes weekly.
- No evaluation set.

## Sources

- Lewis et al., "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks" (2020): <https://arxiv.org/abs/2005.11401>
- Anthropic, "Introducing Contextual Retrieval" (chunking, hybrid search, re-ranking): <https://www.anthropic.com/news/contextual-retrieval>
- Hu et al., "LoRA: Low-Rank Adaptation of Large Language Models" (2021): <https://arxiv.org/abs/2106.09685>

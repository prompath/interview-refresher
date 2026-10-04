[Contents](../index.md) · F1 · P2

# Classification with a language model

## In one minute

A large language model can classify text from instructions and a few examples, with no
training data, which is ideal when labels are scarce or the classes may change. I define
the classes precisely in the prompt, force a structured answer, and evaluate on a labelled
set like any classifier. When volume is high and labels exist, a small fine-tuned model is
cheaper and faster, and the language model can be used to create its training labels.

## Key ideas

- **Zero-shot and few-shot.** Zero-shot: class definitions only. Few-shot: add labelled
  examples, chosen to cover boundary cases; examples can be retrieved per input by
  similarity.
- **Prompt content.** Role and task, each class with a definition and what it excludes,
  rules for ambiguous cases, an "other" or "unclear" class, output format.
- **Structured output.** Ask for JSON with a fixed set of labels; use the provider's
  structured output or tool-calling feature so the answer always parses; validate and
  retry on failure.
- **Determinism.** Low temperature; same prompt version; record model version.
- **Evaluation.** A labelled test set never used in prompt writing. Per-class precision,
  recall and F1; macro-F1 when classes are imbalanced; confusion matrix to see which
  classes are mixed up.
- **Intent classification.** Many classes, often overlapping; a hierarchy (domain, then
  intent) and a fallback class help.
- **Profanity and abuse.** Context matters (quoting, slang, spelling tricks, mixed
  language). Recall is usually the priority; keyword lists are a cheap first filter but
  miss context.
- **Thai text.** No spaces between words, informal spelling and code-mixing; check the
  model's Thai ability on real samples.
- **Cost and latency.** Per-token price and seconds per call; reduce with a smaller model,
  batching, prompt caching, or a cascade: cheap filter first, language model for the
  uncertain cases.
- **Alternatives.** Embeddings plus logistic regression; a fine-tuned encoder (BERT-style,
  WangchanBERTa for Thai). Better at scale when labels exist.
- **Safety.** Inputs are untrusted text: guard against instructions hidden in them
  (prompt injection); keep personal data handling in mind.

## On my CV

"Co-developed a large language model pipeline for intent and profanity classification,
and prepared the client presentations" (Sertis, 2023-2024). Co-developed: be clear which
parts were mine.

## Likely questions

1. **Why a language model and not a trained classifier?** Few labels, classes still
   changing, and fast iteration.
2. **How did you evaluate it?** Labelled test set, per-class metrics, error review to
   refine class definitions.
3. **How did you get consistent output?** Fixed label set, structured format, low
   temperature, validation.
4. **What would you change at ten times the volume?** Distil into a small model trained on
   language model labels, keep the large model for hard cases.
5. **Senior follow-up: how did you explain reliability to the client?** With the
   confusion matrix and examples of typical errors, and a human review path for the
   uncertain class.

## Pitfalls

- Tuning the prompt on the test set.
- Reporting only overall accuracy.

## Sources

- Anthropic, prompt engineering overview: <https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview>
- OpenAI, structured outputs guide: <https://platform.openai.com/docs/guides/structured-outputs>
- scikit-learn, classification metrics: <https://scikit-learn.org/stable/modules/model_evaluation.html#classification-metrics>

[Contents](../index.md) · F5 · P3

# LangChain

## In one minute

LangChain is a Python and JavaScript framework that provides common building blocks for
language model applications (prompt templates, model wrappers, output parsers, retrievers,
tools) and a way to compose them into pipelines. It was the default choice in 2023 because
it made prototypes fast. Its usual criticism is too much abstraction, which makes
debugging and customisation harder than calling the model's own SDK.

## Key ideas

- **Components.**
  - *Chat model*: one interface over many providers.
  - *Prompt template*: a prompt with variables.
  - *Output parser*: turns the reply into a string, JSON or a typed object.
  - *Document loader, text splitter, embeddings, vector store, retriever*: the retrieval
    pipeline.
  - *Tool*: a function the model may call.
- **Composition.** The expression language pipes components:

  ```python
  chain = prompt | model | parser
  chain.invoke({"text": "..."})
  ```

  Chains support batching, streaming and async through the same interface.
- **Classification chain.** Template with class definitions → model → structured output
  parser → validation.
- **Retrieval chain.** Retriever → format documents into the prompt → model → parser.
- **LangGraph.** A companion library for agents as explicit graphs with state, loops and
  human approval steps; now the recommended route for agents in that ecosystem.
- **LangSmith.** Tracing and evaluation service.
- **Criticisms.** Layers of abstraction hide the actual prompt; frequent breaking changes
  in early versions; simple tasks are shorter with the provider SDK.
- **When it helps.** Switching providers, many standard integrations, quick prototypes.
- **Alternatives.** Provider SDKs directly; LlamaIndex for retrieval-heavy work; agent
  SDKs from model providers.

## On my CV

LangChain in Libraries; used for the Sertis language model work in 2023 to 2024. The API
has changed a great deal since; say which period my experience is from.

## Likely questions

1. **What did you use LangChain for?** Prompt templates, model calls and output parsing
   in the classification pipeline.
2. **Would you use it again?** For a prototype with many integrations, yes; for a small
   production service I would consider the SDK directly for transparency.
3. **What is a chain?** A fixed sequence of steps, each feeding the next, as opposed to an
   agent that chooses its steps.
4. **How did you debug it?** Logged the rendered prompt and raw output at each step.
5. **Senior follow-up: framework or no framework for a team?** Choose by what the team
   must maintain: fewer dependencies and visible prompts usually win over convenience.

## Pitfalls

- Describing 2023 APIs (`LLMChain`) as current.

## Sources

- LangChain documentation: <https://docs.langchain.com/>
- LangGraph: <https://www.langchain.com/langgraph>
- Anthropic, "Building effective agents" (on frameworks and abstraction): <https://www.anthropic.com/engineering/building-effective-agents>

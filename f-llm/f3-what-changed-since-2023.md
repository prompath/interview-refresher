[Contents](../index.md) · F3 · P2

# What changed since 2023

## In one minute

My hands-on language model work was in 2023 and 2024. Since then the models have become
much more capable and cheaper per token, context windows have grown, and the centre of
gravity has moved from single prompts and retrieval pipelines to agents: models that call
tools in a loop to complete multi-step tasks. I should show I know this, and say plainly
which parts I have used only as a user.

## Key ideas

- **Tool use (function calling).** The model returns a structured request to call a
  function; the application runs it and returns the result; the model continues. This is
  the building block of agents.
- **Agents.** A loop of model → tool call → result → model, until the task is done.
  Design questions: which tools, how much autonomy, when to ask a human, how to recover
  from errors.
- **Model Context Protocol (MCP).** An open standard (introduced late 2024) for
  connecting models to tools and data sources, so integrations are reusable across
  applications.
- **Structured outputs.** Providers can now guarantee output matching a JSON schema,
  replacing fragile parsing.
- **Long context.** Hundreds of thousands to a million tokens. Whole documents can go in
  the prompt, which reduces the need for retrieval on small corpora; retrieval still
  matters for large or changing ones.
- **Reasoning models.** Models that spend extra computation thinking before they answer;
  better on multi-step problems at higher cost and latency.
- **Multimodal input.** Images, PDFs, audio handled natively.
- **Prompt caching and batch APIs.** Large reductions in cost for repeated context and
  offline workloads.
- **Coding assistants.** Agentic coding tools are now part of normal engineering work.
- **Evaluation.** Has become the core engineering skill: task-specific test sets,
  language-model judges checked against humans, regression suites.
- **Frameworks.** Many teams moved from heavy orchestration frameworks to thinner code
  directly on provider SDKs, plus graph-style agent libraries where state is complex.
- **Still true from 2023.** Clear prompts, good examples, grounding and evaluation.

## On my CV

Sertis bullets 3 and 4 and "large language models" in Skills. An interviewer may test
whether the knowledge is current.

**To fill in (only I know):** what I have actually used since 2024 (for example agentic
coding tools in daily work) and anything I have built with them.

## Likely questions

1. **How would you build the classification pipeline today?** Structured outputs, a
   small fast model, prompt caching, an evaluation suite; the design is the same, the
   plumbing is simpler.
2. **Is RAG dead now that context is long?** No. Long context helps small corpora;
   retrieval is still needed for scale, freshness, cost and access control.
3. **What is an agent and when would you not use one?** A tool-calling loop. Not when a
   fixed pipeline does the job: agents cost more and are harder to test.
4. **How do you keep up?** Name real sources and something tried recently.
5. **Senior follow-up: where would you apply language models in this team's work?** Pick
   one or two concrete, measurable uses (text classification of contact reasons,
   analysis assistance) rather than a general claim.

## Pitfalls

- Presenting 2023 practice as current.
- Naming specific model versions from memory; they date quickly.

## Sources

- Anthropic, "Building effective agents": <https://www.anthropic.com/engineering/building-effective-agents>
- Model Context Protocol: <https://modelcontextprotocol.io/>
- Anthropic, tool use overview: <https://docs.claude.com/en/docs/agents-and-tools/tool-use/overview>

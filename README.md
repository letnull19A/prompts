# AI Agent Prompt Examples — Multi-Agent Pipeline Specs

A collection of real-world prompts used to drive AI agents in multi-step, multi-agent pipelines — covering task specification, workflow orchestration, and guardrails/validation logic for LLM-based systems.

These are working examples, not toy snippets: each prompt was written to run a real agent (schema design, database design, validation) inside a production pipeline, then anonymized for public use. If you're building agentic workflows, API/schema generation pipelines, or LLM guardrails, you can copy these directly or adapt the structure to your own project.

## Why this repo

Most public prompt collections are either single-turn chat prompts or vague "prompt engineering tips." This repo focuses on a narrower, more useful case: **structured prompts that define an entire agent pipeline** — inputs, steps, dependencies, fallback behavior, and expected outputs — written as machine-parseable XML that an LLM (or an orchestration layer) can execute step by step.

Use cases these examples are good for:
- Designing OpenAPI schemas via an AI agent and validating them programmatically
- Structuring multi-agent workflows with explicit dependencies between steps
- Writing guardrails so AI-generated output (schemas, code, docs) is verifiable before it's trusted downstream
- Learning a reusable pattern for prompt-as-pipeline-spec, instead of prompt-as-single-instruction

## Repository structure

```
.
├── openapi-schema-guardrails.xml       # RU: OpenAPI schema generation + validation pipeline
├── openapi-schema-guardrails.en.xml    # EN: same prompt, translated
└── README.md
```

Each prompt follows the same shape:

- **`<context><dictionary>`** — defines the terms/agents used in the task, so the model doesn't guess at ambiguous roles
- **`<task-title>` / `<task-body>`** — the problem statement and the strategy for solving it
- **`<expect><workflow>`** — one or more named pipelines, each broken into `<step>`s with explicit `depends-on`, `input`, `script` (what the step should do), and `return` (what it hands to the next step or the caller)
- A dedicated fallback step (`id="-1"`) in every pipeline for error handling

This structure makes prompts easy to version, diff, and reuse — you can swap out a single step's script without rewriting the whole prompt.

## How to use these examples

1. Pick the prompt closest to your use case (e.g. `openapi-schema-guardrails.en.xml`).
2. Replace the placeholder agent names/roles in `<dictionary>` with the agents in your own system.
3. Adjust the `<workflow>` steps to match your actual pipeline — add, remove, or reorder steps as needed.
4. Feed the resulting XML to your LLM as a system or task prompt, or use it as a spec for your orchestration code.

No SDK, framework, or dependency is required — these are plain-text prompt specs you can use with any LLM provider.

## Contributing

If you have a similar structured prompt you'd like to share (workflow-based, guardrails-based, or multi-agent), feel free to open a PR. Please anonymize any project-specific names, URLs, or business logic before submitting.

## About

Written and maintained by [Aleksei Volkov](https://github.com/letnull19a), a fullstack developer working on AI-agent-driven developer tools. More projects and case studies: *(link to portfolio site, once live)*.

## License

MIT — use these prompts freely in your own projects.

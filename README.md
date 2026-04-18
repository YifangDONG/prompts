# Prompts

A personal collection of prompt engineering techniques and agent skills I use with LLM-based coding assistants.

## Contents

### Prompt techniques

Short, self-contained notes on reusable prompting patterns:

- [`ask-plan-build.md`](./ask-plan-build.md)
- [`chain-of-verification.md`](./chain-of-verification.md)
- [`confident-weighted.md`](./confident-weighted.md)
- [`constrain-first.md`](./constrain-first.md)
- [`context-injection-with-boundaries.md`](./context-injection-with-boundaries.md)
- [`few-shot-with-negative-example.md`](./few-shot-with-negative-example.md)
- [`iterative-refinement-loop.md`](./iterative-refinement-loop.md)
- [`meta-prompting.md`](./meta-prompting.md)
- [`multi-perspective.md`](./multi-perspective.md)
- [`role-based.md`](./role-based.md)
- [`structed-thinking-protocol.md`](./structed-thinking-protocol.md)

### Skills

Agent skills live under [`skills/`](./skills). Each skill is a self-contained folder with a `SKILL.md` that an agent can read and follow.

#### [`explore-codebase`](./skills/explore-codebase)

A skill that guides an agent through exploring an unfamiliar codebase or module using a structured reading methodology — functional purpose, entry points, decomposition, dependency graph, patterns, commit history, and tests — and produces a written analysis report.

It is a direct adaptation of the methodology from the blog post [Takeaways from code reading workshop](https://yifangdong.github.io/takeaways-from-code-reading-workshop/) by Yifang Dong, turned into an actionable workflow for coding agents. The key idea: *the larger the codebase, the shallower the first pass* — the goal is not to understand every line, but to answer "what does this do, where does it start, and how does it decompose?".

The skill folder contains:

- `SKILL.md` — the workflow and guidance the agent follows
- `report-template.md` — the structure of the output report
- `example-report.md` — a worked example

## License

Personal notes, shared as-is.

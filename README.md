# Claude Behavior Skill

> A portable Claude-like behavioral skill for **non-Claude models** — especially GPT/ChatGPT, Grok, Gemini, DeepSeek, Qwen, GLM, Kimi, and local/open-weight LLMs.

**Unofficial. Not affiliated with Anthropic.**

[Skill](./SKILL.md) · [Full Behavioral Rules](./references/behavioral-rules.md) · [System-Prompt Version](./CLAUDE_STYLE_PROMPT.md) · [Behavioral Evals](./EVALS.md) · [Design Notes](./DESIGN_NOTES.md) · [中文版](./README_zh.md)

## What this project is

This project packages a Claude-like interaction layer as a reusable **Skill** for other AI models.

The target is not superficial Claude roleplay. It focuses on transferable behavioral patterns such as:

- anti-sycophancy and independent judgment;
- calibrated uncertainty and epistemic humility;
- warm, natural, non-patronizing conversation;
- constructive disagreement;
- concise-by-default but depth-sensitive answers;
- balanced treatment of contested questions;
- current-information retrieval when needed;
- tool and source honesty;
- direct correction of earlier mistakes;
- stable behavior across long conversations.

The underlying host remains GPT, Grok, Gemini, DeepSeek, Qwen, GLM, Kimi, or whatever model is actually running. The skill must never falsely claim the model has become Claude or is using Anthropic-only capabilities.

## Why a Skill instead of one giant prompt?

A long system prompt can work, but it consumes context continuously and mixes activation logic with detailed behavior.

The Skill version uses progressive disclosure:

```text
SKILL.md
└── references/
    └── behavioral-rules.md
```

`SKILL.md` contains activation logic and core invariants. The full behavioral specification is loaded only when the skill is invoked.

This makes the project easier to reuse in agent frameworks while preserving a standalone prompt version for platforms that do not support skills.

## Primary target models

This repository is primarily intended for **non-Claude AI systems**:

| Model family | Intended use |
|---|---|
| GPT / ChatGPT / Codex-style agents | Skill, project instruction, system/developer prompt |
| Grok | Custom/system instruction or compatible agent skill |
| Gemini | System instruction, Gem/agent instruction, reusable skill layer |
| DeepSeek | System prompt or agent framework skill |
| Qwen | System prompt or compatible agent framework |
| GLM | System/custom instruction or agent framework |
| Kimi | System/custom instruction or agent framework |
| Local/open-weight LLMs | System message or reusable skill in an agent framework |

Exact installation depends on the client or agent runtime. The behavioral layer itself is model-agnostic.

## Quick start — Skill

Use the repository as a reusable agent skill where your environment supports `SKILL.md`-style modules.

The entry point is:

[`SKILL.md`](./SKILL.md)

When invoked, it loads:

[`references/behavioral-rules.md`](./references/behavioral-rules.md)

Typical trigger language includes:

- “Switch to Claude mode.”
- “Use the Claude-like behavior skill.”
- “Respond more like Claude.”
- “Apply the behavioral-emulation skill for this conversation.”

The skill is intentionally named `behavioral-emulation` internally rather than using `claude` in the skill identifier, while the repository and description make the intended behavior explicit.

## Quick start — plain system prompt

If your platform does not support skills, use:

[`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md)

Place it in the highest-priority **user-configurable** instruction field available to you.

> The host platform's actual system policies, identity, tool access, and capabilities always take precedence.

## Does it actually work?

That should be measured rather than assumed.

[`EVALS.md`](./EVALS.md) contains a baseline-vs-skill evaluation suite covering:

- anti-sycophancy;
- correction of false premises;
- self-correction;
- ambiguity handling;
- epistemic calibration;
- current-information retrieval;
- tool honesty;
- complexity control;
- emotional boundaries;
- partial-refusal quality.

For a meaningful test, compare the **same base model with and without the skill** while keeping model version, reasoning settings, tools, and temperature fixed.

**No benchmark result is bundled yet.** Reproducible results on GPT, Grok, Gemini, DeepSeek, Qwen, GLM, Kimi, and local models are especially welcome.

## Design principle

This project intentionally avoids instructions like:

> “You are Claude. Think exactly like Claude Opus.”

That mostly encourages identity roleplay.

The skill instead encodes **observable behavioral decisions**: when to push back, when to retrieve current information, how to represent uncertainty, how much clarification to request, how to avoid sycophancy, what not to fabricate, and when to revise an earlier answer.

See [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) for the rationale and limitations.

## Source lineage

The synthesis was informed primarily by public GitHub repositories that collect or analyze Claude-related prompts and prompt-engineering patterns:

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

The final skill is a **portable synthesis and paraphrased behavioral abstraction**, not a verbatim copy of Anthropic proprietary prompts.

Public prompt collections can have imperfect provenance, so they are treated as behavioral evidence and design references rather than an authenticated specification of Anthropic internals.

## What this cannot reproduce

A skill cannot clone another model's:

- weights;
- post-training;
- hidden routing;
- reward models;
- safety classifiers;
- context-management stack;
- inference-time compute;
- proprietary tool implementation.

The goal is **behavioral emulation**, not model cloning.

The quality of the underlying base model still matters substantially.

## Project status

**Experimental / early-stage.**

The skill is usable today, but rigorous model-by-model results are still being collected.

## Contributing

PRs are welcome. High-value contributions include:

- before/after outputs on GPT, Grok, Gemini, DeepSeek, Qwen, GLM, Kimi, or local models;
- behavioral rules grounded in public evidence;
- shorter variants that preserve behavior;
- additional regression tests;
- adapters for popular agent/skill runtimes;
- reproducible benchmark runs using [`EVALS.md`](./EVALS.md).

Please avoid unverifiable claims about private model internals.

## License

MIT. See [`LICENSE`](./LICENSE).

## Disclaimer

“Claude” is a trademark/product name associated with Anthropic. This is an independent community project and is not endorsed by, affiliated with, or maintained by Anthropic.

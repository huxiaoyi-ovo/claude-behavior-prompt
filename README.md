# Claude Behavior Prompt

> A high-fidelity, model-agnostic behavioral prompt for making GPT, Gemini, Grok, local LLMs, and other assistants interact more like Claude.

**Unofficial. Not affiliated with Anthropic.**

[中文版](./README_zh.md) · [Full Prompt](./CLAUDE_STYLE_PROMPT.md) · [Behavioral Evals](./EVALS.md) · [Design Notes](./DESIGN_NOTES.md)

## Why this exists

Many “make GPT behave like Claude” prompts mostly imitate surface style: warmer wording, more hedging, or a few persona adjectives.

This project targets the deeper **behavioral layer** instead:

- when the model should push back;
- how it handles uncertainty;
- whether it inherits the user's confidence;
- how it balances competing interpretations;
- when it should search for current information;
- whether it admits missing tool/file access;
- how aggressively it asks clarifying questions;
- how response depth scales with task complexity;
- whether it corrects its own earlier mistakes.

The result is a portable system prompt built from behavioral rules rather than “You are Claude” roleplay.

## What it tries to reproduce

- Helpful-by-default interaction stance
- Warm but non-sycophantic tone
- Constructive disagreement and independent judgment
- Proportional depth: concise for simple tasks, deep for hard ones
- Strong uncertainty calibration and epistemic humility
- Balanced treatment of contested questions
- Search/retrieval discipline for current information
- Tool honesty: no simulated calls or fabricated results
- Natural personalization without forced memory references
- Long-conversation behavioral stability
- Restrained refusal behavior without moralizing
- Natural formatting rather than template-heavy answers
- Direct correction when prior answers are wrong

## Quick start

Copy [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) into the highest-priority **user-configurable** instruction field your model supports:

- **ChatGPT / custom GPT / API:** system or developer instructions where available
- **Gemini / AI Studio:** system instruction
- **Grok / compatible clients:** system prompt / custom instruction
- **Local LLMs:** system message in your chat template

Then talk to the model normally.

> The host platform's real system policies, identity, tool access, and capabilities still take precedence. This prompt should never make a model falsely claim to be Claude or pretend it has Anthropic-only tools.

## Does it actually work?

That should be measured, not assumed.

The repository includes a reproducible baseline-vs-prompted suite in [`EVALS.md`](./EVALS.md). It tests observable behavior including:

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

Run the same base model with and without the prompt, keep settings fixed, and publish the raw outputs alongside scores.

**No benchmark result is bundled yet.** Contributions with reproducible cross-model results are especially welcome.

## Design principle

This project intentionally avoids prompts like:

> “You are Claude. Think exactly like Claude Opus.”

That instruction mostly encourages roleplay.

The prompt here encodes **observable decision rules and behavioral constraints** instead: when to push back, when to search, how to represent uncertainty, how much clarification to request, what not to fabricate, and when to revise a previous answer.

See [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) for the rationale and limitations.

## Source lineage

The synthesis was informed primarily by public GitHub repositories that collect or analyze Claude-related prompts and prompt-engineering patterns:

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

The final prompt is a **portable synthesis and paraphrased behavioral abstraction**, not a verbatim copy of Anthropic proprietary prompts.

Public prompt collections can have imperfect provenance. This project therefore treats them as behavioral evidence and design references, not as an authenticated specification of Anthropic internals.

## What this cannot reproduce

A prompt cannot clone another model's:

- weights;
- post-training;
- hidden routing;
- reward models;
- safety classifiers;
- context-management stack;
- inference-time compute;
- proprietary tool implementation.

This project aims for **behavioral emulation**, not model cloning.

The underlying base model still matters a lot.

## Project status

**Experimental / early-stage.**

The behavioral prompt is usable today, but rigorous model-by-model results are still being collected. The project should become more credible as contributors publish raw eval outputs and identify rules that can be shortened without losing behavior.

## Contributing

PRs are welcome. Useful contributions include:

- behavioral rules grounded in public evidence;
- before/after outputs across different base models;
- shorter variants that preserve behavior;
- regression tests for sycophancy, ambiguity, uncertainty, correction, and tool honesty;
- reproducible benchmark runs using [`EVALS.md`](./EVALS.md).

Please avoid unverifiable claims about private model internals.

## License

MIT. See [`LICENSE`](./LICENSE).

## Disclaimer

“Claude” is a trademark/product name associated with Anthropic. This is an independent community project and is not endorsed by, affiliated with, or maintained by Anthropic.

# Claude Behavior Prompt

> A high-fidelity, model-agnostic system prompt for shaping GPT, Gemini, Grok, local LLMs, and other assistants toward a Claude-like interaction style.

**Unofficial. Not affiliated with Anthropic.**

## Why this exists

Many “Claude persona” prompts only imitate surface-level tone. This project focuses on the deeper behavioral layer instead: how an assistant frames uncertainty, pushes back, balances perspectives, uses tools, handles ambiguity, adapts depth, and avoids sycophancy.

The prompt is synthesized from publicly available GitHub prompt collections and prompt-engineering references, then normalized into a portable system prompt that can be used across different models.

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
- Clear refusal behavior without moralizing
- Natural formatting rather than template-heavy answers
- Direct correction when prior answers are wrong

## Quick start

Copy [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) into the highest-priority instruction field your model supports:

- **ChatGPT / custom GPT / API:** system or developer instructions
- **Gemini / AI Studio:** system instruction
- **Grok / compatible clients:** system prompt / custom instruction
- **Local LLMs:** system message in your chat template

Then talk to the model normally.

For a lightweight smoke test, see [`examples/quick-start.md`](./examples/quick-start.md).

中文版：[`README_zh.md`](./README_zh.md)

## Design principle

This project intentionally avoids prompts like:

> “You are Claude. Think exactly like Claude Opus.”

That kind of instruction mostly produces roleplay. The prompt here encodes **decision rules and behavioral constraints** instead: when to push back, when to search, how to represent uncertainty, how much to ask, what to avoid, and what good conversational behavior looks like.

## Source lineage

The project was informed primarily by public GitHub repositories that collect or analyze Claude system prompts and prompt structure, including:

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

The final prompt is a **portable synthesis and paraphrased behavioral abstraction**, not a verbatim copy of Anthropic proprietary prompts.

## What this cannot reproduce

A prompt cannot clone another model’s weights, post-training, hidden routing, safety classifiers, context management, tool implementation, or inference-time compute. This project aims for **behavioral emulation**, not model cloning.

The underlying base model still matters a lot.

## Contributing

PRs are welcome. Useful contributions include:

- behavioral rules grounded in public prompt evidence;
- before/after examples across different base models;
- shorter variants that preserve behavior;
- regression tests for sycophancy, ambiguity, uncertainty, correction, and tool honesty.

Please avoid unverifiable claims about private model internals.

## License

MIT. See [`LICENSE`](./LICENSE).

## Disclaimer

“Claude” is a trademark/product name associated with Anthropic. This is an independent community project and is not endorsed by, affiliated with, or maintained by Anthropic.

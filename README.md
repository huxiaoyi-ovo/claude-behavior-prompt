# Claude Behavior Skill

A small behavior layer for making non-Claude models feel a little more like Claude to talk to.

**GPT / Grok / Gemini / DeepSeek / Qwen / GLM / Kimi / local LLMs**

[中文](./README_zh.md) · [Skill](./SKILL.md) · [Plain prompt](./CLAUDE_STYLE_PROMPT.md) · [Evals](./EVALS.md)

<p align="center">
  <img src="./assets/cover.svg" alt="Claude Behavior Skill doodle cover" width="100%" />
</p>

Most “Claude-style” prompts mainly copy the tone. This repo is more interested in the decisions underneath it: when to disagree, when to stay uncertain, when to search, when to admit a tool or file is unavailable, and when to correct an earlier answer.

## Quick start

**If your agent supports skills:** use [`SKILL.md`](./SKILL.md).

**If it only supports system/custom instructions:** use [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md).

Then just talk to the model normally. A trigger can be as simple as:

```text
Switch to Claude mode for this conversation.
```

## What changes

| Situation | Typical default | With this skill |
| --- | --- | --- |
| The user sounds very confident | Often follows the premise | Checks the premise before agreeing |
| Evidence is incomplete | Tends to give a clean answer anyway | Keeps uncertainty visible |
| A file/tool is unavailable | May infer more than it should | Says clearly what it cannot access |
| An earlier answer was wrong | Can defend the previous answer | Corrects it directly |
| The question depends on fresh information | May answer from memory | Looks it up when tools are available |
| The task is simple | Can over-explain | Keeps the answer short unless depth is useful |

That table describes the intended behavior, not benchmark results. For actual testing, see [`EVALS.md`](./EVALS.md).

## Why a skill?

Because “act like Claude” usually changes the **voice** more than the **judgment**.

The skill separates a small activation layer from the full behavior rules, so an agent can load the detailed instructions only when needed:

```text
SKILL.md
└── references/
    └── behavioral-rules.md
```

For platforms without a skill system, the same behavior is also available as a plain system prompt.

## Supported models

The rules are model-agnostic. They are mainly intended for:

`GPT / ChatGPT` · `Grok` · `Gemini` · `DeepSeek` · `Qwen` · `GLM` · `Kimi` · `local/open-weight models`

The stronger the base model, the more convincing the behavior shaping tends to be.

## Files

- [`SKILL.md`](./SKILL.md) — skill entry point
- [`references/behavioral-rules.md`](./references/behavioral-rules.md) — full behavior rules
- [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) — plain prompt version
- [`EVALS.md`](./EVALS.md) — behavior checks
- [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) — design notes and limits

<details>
<summary>Sources</summary>

The behavior rules were distilled from public Claude-related prompt collections and prompt-engineering projects, especially:

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

This repo is a rewritten, portable synthesis rather than a verbatim copy.

</details>

<details>
<summary>Limits</summary>

A skill or prompt cannot copy Claude's weights, post-training, hidden routing, context management, inference-time compute, or proprietary tools.

The goal here is behavioral emulation, not model cloning.

</details>

MIT licensed. Unofficial project. Not affiliated with Anthropic.

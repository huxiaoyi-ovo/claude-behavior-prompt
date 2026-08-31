<p align="center">
  <img src="./assets/banner.svg" alt="Claude Behavior Skill" width="100%" />
</p>

<p align="center">
  <a href="./README_zh.md">中文</a> · <a href="./SKILL.md">Skill</a> · <a href="./CLAUDE_STYLE_PROMPT.md">Plain prompt</a> · <a href="./EVALS.md">Tests</a>
</p>

A small experiment in making **non-Claude models feel a little more like Claude to talk to**.

I don't mean pretending the model *is* Claude. The goal is the part people usually notice in conversation: less automatic agreement, better handling of uncertainty, more willingness to push back, and a calmer response style.

It is mainly meant for `GPT / ChatGPT`, `Grok`, `Gemini`, `DeepSeek`, `Qwen`, `GLM`, `Kimi`, and local models.

## What changes

With the skill enabled, the model is encouraged to:

- disagree when there is a real reason to disagree;
- separate facts from guesses and interpretations;
- keep easy answers short and spend more time on hard questions;
- look things up when freshness actually matters;
- admit when it cannot access a file, tool, memory, or website;
- correct an earlier answer instead of defending it for consistency.

That's basically the idea. The rest of the repository is just an attempt to make those behaviors consistent instead of relying on a one-line persona prompt.

## Try it

If your agent/client supports skills, use [`SKILL.md`](./SKILL.md).

A natural trigger is enough:

```text
Switch to Claude mode for this conversation.
```

If your platform only gives you a system prompt or custom-instructions box, use [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) instead.

No special syntax is required after that. Just talk to the model normally.

## Why not just say “act like Claude”?

Because that tends to change the **voice** more than the **behavior**.

This repo tries to spell out the decisions underneath the style: when to question the user, when to stay uncertain, when to search, when to ask for clarification, and when to simply say “I don't know.”

## Does it work?

Depends on the base model. A prompt or skill cannot copy Claude's weights, post-training, hidden routing, or tools.

There is a small baseline-vs-enabled test set in [`EVALS.md`](./EVALS.md) if you want to compare models without going by vibes alone.

I haven't bundled a leaderboard yet. If you test it on GPT, Grok, Gemini, DeepSeek, Qwen, GLM, Kimi, or a local model, raw before/after outputs are more useful than a single score.

## What's in the repo

- [`SKILL.md`](./SKILL.md) — the skill entry point
- [`references/behavioral-rules.md`](./references/behavioral-rules.md) — the full behavior rules
- [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) — plain system-prompt version
- [`EVALS.md`](./EVALS.md) — behavioral checks
- [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) — design notes and limits

## Where it came from

The behavior rules were distilled from public Claude-related prompt collections and prompt-engineering projects, especially:

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

This repo is a rewritten, portable synthesis. It is not an official Anthropic prompt and is not affiliated with Anthropic.

MIT licensed. PRs and test results are welcome.

# Source Lineage & Evidence

This project is a **behavioral synthesis**, not an official Anthropic prompt release.

The goal is to extract portable interaction rules from public material associated with Claude, then rewrite those rules so they can be used as model-agnostic system instructions.

## Evidence levels

We use three levels of evidence:

| Level | Meaning | How it is used |
|---|---|---|
| **A — Prompt collection** | Public repositories that claim to contain extracted or reconstructed Claude system prompts | Evidence for recurring behavioral rules |
| **B — Prompt analysis** | Repositories that analyze how Claude system prompts are structured | Used to convert observations into portable instructions |
| **C — Project synthesis** | Our own deduplication, normalization, and cross-model adaptation | Used only to make the behavior portable; should not be presented as an Anthropic-authored rule |

## Primary public references

### 1. asgeirtj/system_prompts_leaks — Level A

Repository: https://github.com/asgeirtj/system_prompts_leaks

Relevant material includes the Anthropic directory and, in particular, collected Claude conversational prompts such as:

- `Anthropic/claude-opus-5.md`
- other Claude / Claude Code prompt snapshots in the repository

Behavioral themes used by this project include:

- helpful-by-default stance;
- warm but direct tone;
- constructive pushback;
- concise default responses with depth scaled to complexity;
- limited clarification questions;
- even-handed treatment of contested positions;
- current-information search discipline;
- explicit tool honesty;
- natural personalization and memory use;
- long-conversation behavioral stability;
- avoidance of dependency-seeking language;
- direct correction of errors.

**Caveat:** this is a community-maintained prompt collection. The repository is useful evidence, but this project does not claim that every line has been independently authenticated by Anthropic.

### 2. Piebald-AI/claude-code-system-prompts — Level A/B

Repository: https://github.com/Piebald-AI/claude-code-system-prompts

This collection tracks Claude Code system-prompt components, subagent prompts, tool descriptions, and utility prompts across versions.

It is used mainly to cross-check recurring Anthropic prompt patterns such as:

- functional identities instead of theatrical personas;
- explicit tool rules;
- concise operational instructions;
- fallback behavior when blocked;
- scoped behavioral constraints.

Claude Code is a coding product, so product-specific coding instructions are **not** copied into the portable conversational prompt.

### 3. tjennychen/writing-system-prompts — Level B

Repository: https://github.com/tjennychen/writing-system-prompts

This project is used for prompt-construction principles, especially:

- define a function rather than a character;
- encode expert decision criteria instead of personality adjectives;
- prefer specific behavioral constraints to vague aspirations;
- remove redundant instructions;
- include fallback behavior and completion criteria where useful;
- keep persistent system prompts compact enough that important rules remain salient.

## Transformation policy

The canonical prompt in this repository is intentionally **not** a verbatim dump of any collected system prompt.

We apply the following transformation:

1. Remove Anthropic-product-specific facts, internal tool names, and identity claims.
2. Remove instructions that only make sense inside Claude's own infrastructure.
3. Merge semantically duplicated rules.
4. Rewrite rules as model-agnostic behavioral constraints.
5. Preserve the observable decision criterion whenever possible.
6. Keep host-model identity and safety policies authoritative.

## What “Claude-style” means here

In this repository, **Claude-style** refers to a cluster of observable interaction behaviors reconstructed from the public references above. It does **not** mean:

- identical hidden reasoning;
- identical model weights;
- identical post-training;
- identical safety routing;
- identical tool orchestration;
- identical context management;
- guaranteed indistinguishability from Claude.

## Adding a new rule

A new behavioral rule should ideally include:

1. a public source or reproducible behavioral observation;
2. the failure mode the rule addresses;
3. a model-agnostic formulation;
4. at least one evaluation prompt that can test whether the rule improves behavior.

See [`CONTRIBUTING.md`](./CONTRIBUTING.md) and [`EVALS.md`](./EVALS.md).

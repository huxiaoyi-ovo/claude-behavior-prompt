# Design Notes

This project aims to reproduce **observable Claude-like interaction patterns**, not Claude's hidden internals.

## What is being emulated

The prompt focuses on behavioral properties that can be expressed as instructions and evaluated from outputs:

- helpful-by-default interaction
- concise-but-adaptive depth
- low sycophancy
- willingness to disagree constructively
- calibrated uncertainty
- balanced handling of contested questions
- current-information retrieval when appropriate
- tool honesty
- natural personalization
- long-conversation behavioral stability
- direct correction of mistakes
- restrained refusal style

## What is not being claimed

This repository does not claim to reproduce:

- Anthropic model weights
- post-training data or reward models
- hidden chain-of-thought
- inference-time compute
- safety classifiers or routing
- proprietary context-management systems
- Anthropic's internal tool implementations
- exact output distributions

A system prompt can shape behavior, but the base model remains the dominant capability substrate.

## Why the prompt uses behavioral rules instead of persona adjectives

Instructions such as “be thoughtful,” “be brilliant,” or “act like Claude” are underspecified. They describe an aspiration without defining what the model should actually do differently.

This project instead encodes observable decision rules, such as:

- answer useful parts before asking for clarification;
- do not manufacture certainty;
- revise an earlier answer when stronger evidence appears;
- do not inherit the user's confidence as evidence;
- use retrieval for time-sensitive information when available;
- do not claim a tool action occurred unless it actually occurred.

These rules are easier to test and port across models.

## Source methodology

The project was informed by public repositories that collect or analyze Claude-related prompts and prompt-engineering patterns. The final prompt intentionally paraphrases and abstracts behavior rather than reproducing proprietary prompt dumps verbatim.

Primary public references used during synthesis include:

- https://github.com/asgeirtj/system_prompts_leaks
- https://github.com/Piebald-AI/claude-code-system-prompts
- https://github.com/tjennychen/writing-system-prompts

These sources vary in provenance. Their presence in a public repository does not independently prove that every collected line is an exact or current production instruction. For that reason, this project treats them as behavioral evidence and design references rather than as an authenticated specification of Claude internals.

## Portability rule

Provider-specific identity, product information, internal tool names, hidden reminders, and capabilities should not be copied into the portable prompt when doing so would make another model falsely claim to be Claude or falsely claim access to Anthropic-specific systems.

The portable prompt should preserve the **behavioral intent** while remaining truthful about the host model's actual identity and capabilities.

## Evaluation philosophy

“Feels more like Claude” is useful subjective feedback, but it is not enough for a strong project claim.

The repository therefore includes `EVALS.md`, which measures observable behavioral changes with a baseline-vs-prompted protocol.

Evaluation should focus on behavior rather than prose imitation. A response should not receive a high score merely because it uses Claude-like wording.

## Failure modes to watch

### 1. Prompt bloat

A longer prompt is not automatically better. Redundant rules consume context and may reduce instruction salience.

### 2. Surface-style imitation

A model can sound warm and cautious while remaining highly sycophantic or epistemically careless.

### 3. Base-model limitations

Prompting cannot create capabilities the base model lacks.

### 4. Host-policy conflicts

Higher-priority system or provider policies override this prompt. Safety behavior therefore varies across platforms.

### 5. Tool mismatch

Search and tool instructions only work when the host environment actually exposes those capabilities.

### 6. Overclaiming fidelity

The appropriate claim is behavioral emulation or behavioral shaping, not model cloning.

## Contribution standard

A proposed rule is strongest when contributors can provide:

1. a public source or concrete behavioral rationale;
2. a failure case the rule is intended to fix;
3. a test prompt;
4. before/after outputs from at least one model.

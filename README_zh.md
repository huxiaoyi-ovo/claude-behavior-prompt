# Claude Behavior Skill

给非 Claude 模型加一层更像 Claude 的行为风格。

**GPT / Grok / Gemini / DeepSeek / Qwen / GLM / Kimi / 本地模型**

[English](./README.md) · [Skill](./SKILL.md) · [Prompt 版](./CLAUDE_STYLE_PROMPT.md) · [Evals](./EVALS.md)

<p align="center">
  <img src="./assets/cover.svg" alt="Claude Behavior Skill 涂鸦封面" width="100%" />
</p>

很多所谓的“Claude 风格 Prompt”主要是在模仿语气。这个仓库更在意语气下面的判断方式：什么时候该反驳，什么时候该保留不确定性，什么时候该检索，什么时候应该明确说自己没有访问到文件或工具，以及什么时候该直接纠正前面的错误。

## 快速开始

**如果你的 Agent 支持 Skill：** 用 [`SKILL.md`](./SKILL.md)。

**如果平台只有 System Prompt / Custom Instructions：** 用 [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md)。

之后正常聊天就行。触发可以很简单：

```text
这段对话切换到 Claude 模式。
```

## 会有什么区别

| 场景 | 常见默认表现 | 加载 Skill 后 |
| --- | --- | --- |
| 用户语气非常自信 | 容易顺着前提往下说 | 先检查前提，再决定是否同意 |
| 证据并不完整 | 仍然倾向给出一个干净结论 | 把不确定性保留下来 |
| 文件 / 工具不可用 | 容易推断过头 | 明确说自己实际能访问什么 |
| 前面的回答错了 | 容易为了前后一致继续解释 | 直接改正 |
| 问题依赖最新信息 | 可能凭已有记忆回答 | 有工具时主动检索 |
| 问题本身很简单 | 容易说太多 | 没必要就保持简短 |

这张表描述的是**目标行为**，不是 benchmark 结果。想实际对比，可以看 [`EVALS.md`](./EVALS.md)。

## 为什么做成 Skill

因为一句“请像 Claude 一样回答”，更容易改掉模型的**说话方式**，不一定能改掉它的**判断方式**。

Skill 把触发层和完整行为规则分开：

```text
SKILL.md
└── references/
    └── behavioral-rules.md
```

支持 Skill 的 Agent 可以按需加载；不支持 Skill 的平台则直接使用普通 Prompt 版本。

## 支持哪些模型

行为规则本身不绑定具体厂商，主要面向：

`GPT / ChatGPT` · `Grok` · `Gemini` · `DeepSeek` · `Qwen` · `GLM` · `Kimi` · `本地 / 开源模型`

通常底模越强，行为塑造越明显。

## 文件

- [`SKILL.md`](./SKILL.md) — Skill 入口
- [`references/behavioral-rules.md`](./references/behavioral-rules.md) — 完整行为规则
- [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) — 普通 Prompt 版本
- [`EVALS.md`](./EVALS.md) — 行为测试
- [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) — 设计说明和边界

<details>
<summary>来源</summary>

主要参考了一些公开的 Claude prompt / prompt-engineering 项目：

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

这个仓库是重新整理后的可迁移版本，不是逐字复制。

</details>

<details>
<summary>局限</summary>

Skill / Prompt 无法复制 Claude 的权重、后训练、隐藏路由、上下文管理、推理算力和专有工具。

这里追求的是行为层模仿，不是模型克隆。

</details>

MIT License。非官方项目，与 Anthropic 无关联。

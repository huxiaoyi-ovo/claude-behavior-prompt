# Claude Behavior Skill

一个小实验：让非 Claude 模型在对话时，尽量更像 Claude 一点。

主要面向 GPT、Grok、Gemini、DeepSeek、Qwen、GLM、Kimi，以及本地 / 开源模型。
它**不会**把这些模型真的变成 Claude，目标只是给它们加一层更好的行为风格。

[English](./README.md) · [SKILL.md](./SKILL.md) · [Prompt 版](./CLAUDE_STYLE_PROMPT.md) · [Evals](./EVALS.md)

![Banner](./assets/banner.svg)

## 它主要想改善什么

- 少一点无脑迎合
- 更好的不确定性表达
- 更自然的来回对话
- 更诚实的工具 / 文件处理
- 更直接的自我纠错
- 更好的“该不该检索”判断

![Behavior map](./assets/behavior-map.svg)

## 一个很直观的前后对比

![Before and after](./assets/before-after.svg)

这里只是示意，不算正式 benchmark。想更系统地测，可以直接看 [`EVALS.md`](./EVALS.md)。

## 它是怎么工作的

![Skill flow](./assets/skill-flow.svg)

你可以用两种方式加载它：

### 1）Skill 模式

如果你的 Agent 或客户端支持 `SKILL.md` 这种方式，就从 [`SKILL.md`](./SKILL.md) 开始。

### 2）Prompt 模式

如果你的平台只支持 System Prompt / Custom Instruction，就用 [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md)。

## 适合放到哪些模型上

![Compatibility](./assets/compatibility.svg)

## 仓库里有什么

- [`SKILL.md`](./SKILL.md)：Skill 主入口
- [`references/behavioral-rules.md`](./references/behavioral-rules.md)：完整行为规则
- [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md)：纯 Prompt 版本
- [`EVALS.md`](./EVALS.md)：一套简单的行为测试
- [`DESIGN_NOTES.md`](./DESIGN_NOTES.md)：设计思路和边界

<details>
<summary>为什么不直接写“你就是 Claude”？</summary>

因为那样通常更像角色扮演，不像真正的行为塑造。

这个仓库更想写清楚几件具体的事：什么时候该反驳，什么时候该承认不确定，什么时候该检索，什么时候该说“我没看到文件”，以及什么时候该直接改正自己的错误。

</details>

<details>
<summary>它主要参考了什么</summary>

主要参考了一些公开的 Claude prompt / prompt-engineering 项目，比如：

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

这个项目是整合和抽象，不是逐字复制。

</details>

<details>
<summary>局限</summary>

Skill 或 Prompt 复制不了另一个模型的权重、后训练、隐藏路由、上下文管理和专有工具。

所以这里追求的是行为层模仿，不是模型克隆。

</details>

MIT License。非官方项目，与 Anthropic 无关联。

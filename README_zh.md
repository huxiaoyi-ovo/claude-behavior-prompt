<p align="center">
  <img src="./assets/banner.svg" alt="Claude Behavior Skill" width="100%" />
</p>

<p align="center">
  <a href="./README.md">English</a> · <a href="./SKILL.md">Skill</a> · <a href="./CLAUDE_STYLE_PROMPT.md">Prompt</a> · <a href="./EVALS.md">测试</a>
</p>

这是一个很简单的小实验：**让非 Claude 模型在聊天时，更像 Claude 一点。**

这里说的“像”不是让模型假装自己就是 Claude，而是尽量复现一些比较容易感知到的交互习惯：少一点迎合，对不确定性更敏感，愿意指出问题，回答也更克制一些。

主要面向 `GPT / ChatGPT`、`Grok`、`Gemini`、`DeepSeek`、`Qwen`、`GLM`、`Kimi` 和各种本地模型。

## 大概会变成什么样

开了这个 Skill 之后，模型会更倾向于：

- 真有问题时直接指出来，不因为用户很自信就跟着赞同；
- 分清事实、推断、解释和猜测；
- 简单问题少说一点，复杂问题再展开；
- 涉及最新信息时，有检索能力就去查；
- 没看过文件、没调用工具、没访问到网页时就明确说没有；
- 前面答错了就直接改，不为了“前后一致”硬圆。

差不多就是这些。仓库里剩下的内容，只是在想办法把这些习惯写得更稳定一点，而不是靠一句“请像 Claude 一样回答”。

## 怎么用

如果你的 Agent / 客户端支持 Skill，直接用 [`SKILL.md`](./SKILL.md)。

触发也不用搞得很复杂，比如：

```text
这段对话切换到 Claude 模式。
```

如果平台只有 System Prompt / Custom Instructions，就用 [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md)。

之后正常聊天就行，不需要每句话都重新提醒。

## 为什么不直接写“你就是 Claude”？

因为那通常更容易改掉模型的**说话语气**，但不一定真的改变它的**判断方式**。

这个项目更在意下面这些东西：什么时候应该反驳，什么时候应该保持不确定，什么时候应该检索，什么时候值得追问，以及什么时候该直接说“我不知道”。

## 到底有没有用

看底模。

Skill / Prompt 不可能复制 Claude 的权重、后训练、隐藏路由和工具能力，所以这里做的是行为层塑造，不是模型克隆。

仓库里放了一套 [`EVALS.md`](./EVALS.md)，可以拿同一个模型做“不开 / 开 Skill”的对比。比起单纯说“感觉更像了”，我更希望后面能积累一些原始 before / after 输出。

## 文件

- [`SKILL.md`](./SKILL.md) — Skill 入口
- [`references/behavioral-rules.md`](./references/behavioral-rules.md) — 完整行为规则
- [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) — 普通 Prompt 版本
- [`EVALS.md`](./EVALS.md) — 行为测试
- [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) — 一些设计说明和边界

## 来源

主要参考了几个公开的 Claude prompt / prompt-engineering 项目：

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

最终内容做了重新整理和改写，不是 Anthropic 官方 Prompt，也和 Anthropic 没有隶属关系。

MIT License。欢迎提 PR，也欢迎直接拿不同模型来测。

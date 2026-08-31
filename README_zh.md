<p align="center">
  <img src="./assets/banner.svg" alt="Claude Behavior Skill" width="100%" />
</p>

<p align="center">
  <a href="./LICENSE"><img src="https://img.shields.io/badge/license-MIT-22c55e?style=flat-square" alt="MIT License"></a>
  <a href="./SKILL.md"><img src="https://img.shields.io/badge/type-Agent%20Skill-8b5cf6?style=flat-square" alt="Agent Skill"></a>
  <a href="./EVALS.md"><img src="https://img.shields.io/badge/evals-15%20behavior%20tests-f59e0b?style=flat-square" alt="Behavioral Evals"></a>
  <img src="https://img.shields.io/badge/status-experimental-64748b?style=flat-square" alt="Experimental">
</p>

<p align="center">
  <b>给非 Claude 模型加上一层更像 Claude 的交互行为。</b><br/>
  更克制、更独立、更会质疑，也更自然。
</p>

<p align="center">
  <a href="./README.md">English</a> ·
  <a href="./SKILL.md">Skill</a> ·
  <a href="./CLAUDE_STYLE_PROMPT.md">Prompt</a> ·
  <a href="./EVALS.md">Evals</a>
</p>

---

## ✨ 它能做什么

这个项目给其他大模型增加一层 **Claude-like behavioral layer**。

- 🧠 **独立判断** —— 少迎合、少无脑赞同
- 🎯 **不确定性校准** —— 分清事实、推断和猜测
- 💬 **自然对话** —— 简单问题简答，复杂问题自然深入
- 🔎 **主动查证** —— 涉及最新信息时，有工具就去检索
- 🛠️ **工具诚实** —— 不假装浏览过网页、读过文件或调用过工具
- 🔄 **直接纠错** —— 错了就改，不为了前后一致硬保旧答案

### 主要面向

`GPT / ChatGPT` · `Grok` · `Gemini` · `DeepSeek` · `Qwen` · `GLM` · `Kimi` · `本地模型`

> 它不会把别的模型真的变成 Claude。它塑造的是**可观察的交互行为**，底层模型身份和真实能力保持不变。

---

## 🚀 怎么用

### 方式 A — Skill 模式

如果你的 Agent / 客户端支持 `SKILL.md` 风格的 Skill，把这个仓库作为 Skill 加载即可，入口是：

```text
SKILL.md
```

然后自然触发：

```text
这段对话切换到 Claude 模式。
```

Skill 会继续读取完整行为规则：[`references/behavioral-rules.md`](./references/behavioral-rules.md)

### 方式 B — Prompt 模式

如果你的平台只支持 System Prompt / Custom Instruction，直接复制：

**[`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md)**

放到该平台最高优先级、用户可配置的指令位置即可。

---

## 🧩 为什么不直接写“你就是 Claude”？

因为那通常只会得到**角色扮演**。

这个项目写的是更具体的行为规则：

> 什么时候反驳 · 什么时候检索 · 怎么表达不确定性 · 什么时候需要澄清 · 什么时候主动纠错 · 哪些东西绝不能伪造

所以更容易迁移到不同底模。

---

## 📦 仓库结构

| 文件 | 用途 |
|---|---|
| [`SKILL.md`](./SKILL.md) | 跨模型 Skill 主入口 |
| [`references/behavioral-rules.md`](./references/behavioral-rules.md) | 完整行为规则 |
| [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) | System Prompt 兼容版 |
| [`EVALS.md`](./EVALS.md) | 15 项行为测试 |
| [`DESIGN_NOTES.md`](./DESIGN_NOTES.md) | 设计思路与边界 |

---

## 🧪 到底有没有效果？

不要靠感觉，直接测。

[`EVALS.md`](./EVALS.md) 提供了同一底模 **不开 Skill / 开 Skill** 的对比测试，包括：反迎合、歧义处理、不确定性、纠错、工具诚实、最新信息检索等。

目前仓库还没有预置跨模型 benchmark 结果。欢迎提交可复现结果和原始输出。

<details>
<summary><b>📚 参考来源与方法</b></summary>
<br/>

主要参考公开的 Claude prompt / prompt-engineering GitHub 项目：

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

最终 Skill 是经过**整合、抽象和改写的行为层**，并非逐字复制 Anthropic 的专有系统提示词。

更多细节见 [`DESIGN_NOTES.md`](./DESIGN_NOTES.md)。

</details>

<details>
<summary><b>⚠️ 局限</b></summary>
<br/>

Skill / Prompt 无法复制另一个模型的权重、后训练、隐藏路由、安全分类器、上下文系统、专有工具和推理算力。

底层模型本身依然很重要。

</details>

---

<p align="center">
  <b>如果它真的让你的模型更好聊了，欢迎点个 ⭐。</b>
</p>

<p align="center">
  MIT License · 社区项目 · 与 Anthropic 无关联
</p>

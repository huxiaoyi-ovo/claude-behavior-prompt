# Claude Behavior Prompt

> 一个尽量还原 Claude 通用交互行为的高保真 System Prompt，可用于 GPT、Gemini、Grok、本地大模型等。

**非官方项目，与 Anthropic 无关联。**

## 这个项目解决什么问题

网上很多所谓 “Claude Prompt” 主要模仿语气，比如更温和、更谨慎、更爱解释。

这个项目更关注 Claude 的**行为层**：

- 默认帮助，但保持独立判断
- 不迎合用户，不为了友好而牺牲批判性
- 简单问题简答，复杂问题自动增加分析深度
- 清楚区分事实、推断、假设和不确定性
- 争议问题尽量公平呈现不同视角
- 涉及最新信息时主动检索
- 不伪造工具调用、来源、数据和实验结果
- 自然使用上下文和记忆，不刻意展示“我记得你”
- 长对话中保持人格和判断稳定
- 拒绝时简洁、自然、不说教
- 出错后直接修正，不维护旧答案

## 使用方法

把 [`CLAUDE_STYLE_PROMPT.md`](./CLAUDE_STYLE_PROMPT.md) 复制到模型最高优先级的自定义指令中即可：

- ChatGPT / API：System / Developer Prompt
- Gemini AI Studio：System Instruction
- Grok 或第三方客户端：System Prompt / Custom Instruction
- 本地模型：chat template 的 system message

## 核心思路

项目不会简单写：

> “你就是 Claude，请像 Claude Opus 一样思考。”

这种方式通常只会产生表层角色扮演。

这里尽量把 Claude 的行为拆成可迁移的**决策规则**：什么时候反驳、什么时候检索、如何表达不确定性、什么时候需要澄清、怎么控制篇幅、怎么避免迎合、怎么自然地组织答案。

## 参考来源

主要参考公开 GitHub 项目：

- [`asgeirtj/system_prompts_leaks`](https://github.com/asgeirtj/system_prompts_leaks)
- [`Piebald-AI/claude-code-system-prompts`](https://github.com/Piebald-AI/claude-code-system-prompts)
- [`tjennychen/writing-system-prompts`](https://github.com/tjennychen/writing-system-prompts)

最终 Prompt 是经过**整合、抽象和改写后的跨模型行为层提示词**，没有将 Anthropic 的专有系统提示词逐字复制。

## 局限

Prompt 无法复制另一个模型的权重、后训练、隐藏路由、安全分类器、上下文管理和推理算力。

因此它追求的是 **Claude-like behavioral emulation**，不是 **Claude model cloning**。

底层模型越强，效果通常越明显。

## License

MIT。

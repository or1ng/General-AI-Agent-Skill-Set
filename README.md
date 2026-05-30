# AI Agent 通用技能集

这个目录包含 5 个英文技能，用于规范 ChatGPT、Codex、Claude Code、WorkBuddy、CodeBuddy 等 AI Agent 的执行、工具使用、经验提炼、评估和技能优化。

设计原则来自两篇论文的工程化归纳：技能应该短小、可验证、从真实轨迹中提炼，并通过小步编辑和回归检查避免负迁移。这里的 5 个技能不是全部常驻注入的提示词，而是按任务加载的部署单元。

## 技能结构

| 技能 | 用途 | 加载方式 |
| --- | --- | --- |
| `govern-agent-operation` | 通用运行契约：明确假设、缩小范围、验证后交付 | 可作为默认运行时技能 |
| `encode-tool-semantics` | 编码工具、环境、平台差异和副作用 | 工具型任务按需加载 |
| `extract-skills-from-experience` | 从成功/失败轨迹中提炼可复用技能 | 离线生产技能时使用 |
| `evaluate-skill-utility` | 用 baseline、held-out cases、负迁移检查评估技能是否真的有效 | 接受或比较技能时使用 |
| `optimize-skill-artifacts` | 用 add/delete/replace 小步编辑优化技能，并通过验证 gate 合并 | 迭代已有技能时使用 |

## 推荐工作流

1. 执行普通任务时，优先使用 `govern-agent-operation`。
2. 涉及 shell、浏览器、文件系统、API、文档、表格或业务系统时，叠加 `encode-tool-semantics`。
3. 收集真实任务轨迹后，用 `extract-skills-from-experience` 生成候选技能。
4. 用 `evaluate-skill-utility` 检查候选技能是否带来真实提升。
5. 用 `optimize-skill-artifacts` 对通过验证的技能做小步优化。

## 注意事项

- 不要把所有技能默认注入所有任务。
- 不要用“文本看起来更好”替代真实验证。
- 不要把一次性案例、冗长解释或平台专属细节塞进通用技能。
- 如果一个技能让某些任务变差，应缩小触发范围、删除过拟合规则，或拆成更专门的技能。

English documentation: [README.en.md](README.en.md)

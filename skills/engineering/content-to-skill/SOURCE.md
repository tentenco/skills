# Source

- **Original URL:** https://x.com/GeekCatX/status/2066550371724730721 (long-form
  Article: https://x.com/GeekCatX/article/2066550371724730721)
- **Author / handle:** 知识猫图解 / @GeekCatX
- **Published:** Jun 15, 2026
- **Fetched:** 2026-07-06 via Claude-in-Chrome (signed-in session; the full
  Article is login-gated — the unauthenticated preview shows only the title and
  first two lines).
- **Author-referenced repo:** https://github.com/gnipbao/content-to-skill
  (cited at the end of the article; not independently verified during this
  distillation).
- **Distilled by:** x-skill-distiller → `output/skills/2026-07-06-content-to-skill/`

## Captured content (cleaned, verbatim from the Article)

万物皆可 Skill：如何基于 Codex 把任何内容变成可复用 AI 能力

过去我们使用 AI，常常停留在“提问”。看到一篇文章，让 AI 总结一下；遇到一个报错，让 AI 分析一下；要写一份报告，让 AI 起草一下；要做一个项目，让 AI 帮忙拆解一下。

这些做法当然有用，但效率并不高。因为每一次你都要重新解释背景、规则、格式、偏好和验收标准。真正高阶的 AI 使用方式，不是不断写更长的提示词，而是把一次次有效的 AI 协作经验沉淀成 Skill。

一句话概括：提示词解决一次问题，Skill 解决一类问题；Workflow 解决一条流程，Agent 解决一个目标系统。

在 Codex 里，Skill 是一种可复用的能力包。OpenAI 官方文档将 Codex Skill 定义为由 SKILL.md 加上可选的 scripts/、references/、assets/ 等资源组成的目录。SKILL.md 必须包含 name 和 description。Codex 可以显式调用 Skill，也可以根据 description 自动判断是否加载。本文核心观点：万物皆可 Skill。

一、什么是 Skill？它不是提示词，而是能力模块。提示词通常一次性；Skill 可复用。一个成熟的 Skill 至少封装 7 件事：1 什么时候使用它；2 输入材料是什么；3 处理步骤是什么；4 输出格式是什么；5 质量标准是什么；6 出错时怎么办；7 如何验证结果是否合格。Skill 的本质 = 任务边界 + 操作流程 + 判断标准 + 失败处理 + 可复用资源。Anthropic 官方类比：MCP/工具像厨房设备，Skill 像菜谱。

二、为什么“万物皆可 Skill”？任何可重复、可抽象、可验证的经验，都可以 Skill 化。关键不在内容本身，而在内容背后的可迁移方法。

三、递归视角：Skill 不只是结果，也是制造 Skill 的工具。第一层把内容变成 Skill；第二层把“把内容变成 Skill 的方法”变成 Skill；第三层让 Skill 读取真实反馈自动改进；第四层组合成 Workflow；第五层变成 Agent 的操作系统。Skill = f(经验)；更好的 Skill = f(使用轨迹 + 失败反馈 + 测试结果)；元 Skill = f(如何生成和改进 Skill 的方法)。

四、从提示词到 Skill 的 5 个层级：Prompt（一次任务）→ Template（相似任务）→ Skill（一类任务）→ Workflow（一条流程）→ Agent（围绕目标自动规划、调用工具、检查结果、失败回退）。Codex 更适合当成持续配置改进的队友，而非一次性助手。

五、什么内容最值得 Skill 化？判断标准：高频吗？稳定吗？有输入吗？有输出吗？有步骤吗？能判断好坏吗？失败后能修正吗？满足大部分即值得。三类不要急着 Skill 化：一次性任务；目标还不清楚的任务；高风险判断（法律/医疗/金融/安全 —— 可辅助分析，但不能作为最终专业判断）。

六、核心方法：抽象，而不是复制。从内容里提取 6 个东西：1 问题；2 场景；3 输入；4 过程；5 标准；6 回退。公式：内容 Skill 化 = 去掉一次性信息 + 保留可迁移方法 + 增加验收标准。

七、Codex Skill 推荐结构：my-skill/ 下 SKILL.md（核心）、references/（详细资料）、assets/（模板）、scripts/（稳定执行代码）、evals/（测试用例）。建议把详细资料拆到引用文件，按需加载。最小可用版只需一个 SKILL.md（含 name/description）。description 是 Skill 能否被正确触发的主要机制，要清晰、范围明确、关键场景放前面。

八、最重要的设计原则：渐进披露。Agent 上下文有限。启动时通常只加载 name+description+路径；决定使用时才读完整 SKILL.md。三层：name+description → SKILL.md → references/scripts/assets。好的 Skill 像好函数：名称清楚、职责单一、输入明确、输出稳定、可维护、可组合；不要太窄也不要太宽。

九、元编程视角：写 Skill 就是写“AI 的程序”——自然语言程序，有变量（输入/目标/上下文/约束/输出）、流程（分析→判断→执行→验证→修正→输出）、条件分支、模块、测试（正常/边缘/压力/不应触发）。

十、递归 Skill 系统：让 Skill 自我进化。闭环：输入内容 → 生成 v0.1 → 真实任务测试 → 记录触发/输出/遗漏错误 → 生成修订建议 → 更新 v0.2 → 再测试 → 稳定入库。可写“skill-evolver”：根据执行结果、用户纠正、失败输出、eval 结果、agent 轨迹改进现有 Skill；识别失败类型（错误触发/缺上下文/指令模糊/输出不稳定/缺验证/工具误用/不安全假设）；只改最小必要部分；把失败加入 Gotchas 或 evals；输出新版本+changelog。

十一、好 Skill 的 10 条原则：
1. 从真实任务中提炼，不要凭空生成。
2. 一个 Skill 只做一类事（拆成 meeting-summary、weekly-report、email-rewrite、customer-feedback-analysis、proposal-review 等）。
3. description 决定是否能被正确调用（差：Helps with writing。好：Use this skill when the user wants to turn rough notes, meeting transcripts, or project updates into a structured weekly report... Do not use for casual rewriting.）。
4. 少讲常识，多写 Agent 不知道的东西（只写会改变执行结果的内容）。
5. 给默认方案，不要给一堆菜单（默认 A；扫描 PDF 才用 B；都失败则说明原因并请求人工确认）。
6. 加 Gotchas，而不是只写原则（如 user_id vs accountId；不要把“计划”写成“已完成”；无来源不编造数据；对外文案不用“绝对领先/唯一”）。
7. 输出模板要具体（给标题/一句话结论/关键发现/风险/下一步 的模板）。
8. 必须有失败处理（信息不足/格式错误/不适合 Skill/高风险/无法验证/工具失败 时怎么办）。
9. 用 evals 测试，而不是凭感觉（正常/边缘/反向三类）。
10. 复杂逻辑交给脚本（校验 JSON、统计字段、转换文件、跑测试、格式化、检查链接、计算指标 → scripts/，自包含、说明依赖、有用错误、处理边界）。

十二、通用“内容变 Skill”提示词（可直接丢给 Codex）：判断是否适合 Skill 化 → 若适合提炼（名称/触发/不触发/输入/步骤/输出/质量标准/Gotchas/失败处理/示例/测试用例）→ 若不适合判断更适合 Prompt/Template/Checklist/Workflow/Agent/参考资料 → 输出完整 SKILL.md → 再输出设计理由、过宽/过窄之处、需补充上下文、3 正常 + 3 边缘 + 3 不应触发测试用例。

十三、终极模板：元 Skill —— content-to-skill。name: content-to-skill；description 覆盖 articles/notes/prompts/workflows/tutorials/examples/expert explanations/project rules/failure cases/conversation traces，触发词包括 "turn this into a skill"/"extract a reusable workflow"/"make this repeatable"/"codify this process"，不用于 one-off summaries 或 casual rewriting。含 Goal / Core principle (extract, don't copy) / When to use / When not to use / Input format / Process (Step 1 identify repeatable task → Step 2 separate content from method → Step 3 define boundary → Step 4 design frontmatter → Step 5 write executable instructions → Step 6 progressive disclosure → Step 7 validation → Step 8 package plan) / Output format (Skillization Report) / Quality standards / Gotchas / Failure handling。详细参考仓库：https://github.com/gnipbao/content-to-skill

十四、结语：未来的高手不是会问 AI，而是会训练 AI。普通人把 AI 当搜索框；进阶者当助手；高手当团队成员；专家为 AI 建立 Skill、Workflow、Agent 系统。Skill 是关键中间层：比提示词稳定，比 Agent 简单，比 Workflow 模块化，比文档可执行。看到任何有价值的内容，多问一句：这背后有没有一种可重复使用的能力？如果有，就提炼它、封装它、测试它、迭代它。

（Author bio: 大厂资深程序员 / 小红书万粉博主 / AI 自媒体实战变现 / AI 提示词大师；小红书同名：知识猫图解。）

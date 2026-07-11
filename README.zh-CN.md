# Tenten Skills

[English](./README.md) · [繁體中文](./README.zh-TW.md) · **简体中文** · [日本語](./README.ja.md)

[Tenten](https://tenten.co) 每天实际在用的 Agent Skills，公开分享。

## 为什么做这个仓库

在 Tenten，我们相信 Agent Skills 正在成为知识分享的新单位。一个写得好的 skill，能把有经验的人处理一件事的方式——流程、判断、坑点——封装成任何 AI agent 都能重复执行的形式。

我们在内部为真实工作设计、测试、迭代这些 skills：工程、项目管理、营销、内容、客户交付。这个仓库是这些成果的公开长期记录——之后所有能公开的 skills 都会持续收录到这里，让这个集合不断成长。

公开分享，是因为 skills 在开放环境中会变得更好。欢迎 fork、改成适合你们技术栈的版本，也欢迎反馈问题。

## 快速开始

用 [skills.sh](https://skills.sh) 安装器：

```bash
npx skills@latest add tentenco/skills
```

或手动安装——把任一 skill 文件夹复制到 agent 的 skills 目录：

```bash
# Claude Code（全局）
cp -r skills/engineering/multi-model-orchestrator ~/.claude/skills/

# 或单个项目
cp -r skills/engineering/multi-model-orchestrator <project>/.claude/skills/
```

部分 skills 附带额外组件（subagent 定义、CLAUDE.md 片段）。需要额外步骤的 skill 文件夹内都有 `SETUP.md`。

## 仓库结构

```
skills/
└── <category>/                  # engineering、pm、marketing、productivity…
    └── <skill-name>/
        ├── SKILL.md             # skill 本体（frontmatter + 指令）
        ├── SETUP.md             # 安装步骤（如有需要）
        ├── agents/              # 附带的 subagent 定义（如有）
        ├── scripts/             # 附带的可执行工具（如有）
        └── 使用說明.html         # 繁体中文使用说明，含可复制的 prompt 示例
```

每个 skill 都是自包含的：一个文件夹、所需的一切，加上一份含 prompt 示例、真人可读的使用说明。

## Skills 目录

### Engineering（工程）

| Skill | 说明 |
|-------|------|
| [multi-model-orchestrator](./skills/engineering/multi-model-orchestrator/SKILL.md) | 把复杂开发任务交给多模型团队执行：主模型担任 tech-lead 指挥者，深度推理派给 Opus subagent、机械性工作派给 Sonnet subagent、需要不同视角的问题交给 Codex 盲测同侪。省下顶级模型用量，质量不打折。 |
| [fable-codex-setup](./skills/engineering/fable-codex-setup/SKILL.md) | 一次调用就把全新 Claude Code 项目初始化成「Fable 5 指挥官 × Codex 执行者」架构：检查 OpenAI Codex plugin、将主模型设为 Fable 5、创建 deep-reasoner（Opus）、fast-worker（Sonnet）、codex-executor 三个 sub-agent，并把协作规则写进 CLAUDE.md。是 multi-model-orchestrator 的配套初始化 skill。 |
| [content-to-skill](./skills/engineering/content-to-skill/SKILL.md) | 把任何内容——文章、笔记、prompt、工作流程、调试过程——转成一个可复用、范围明确、可测试的 Agent Skill，并协助判断值不值得做成 skill，以及该用 Skill、prompt、checklist 还是 Agent。 |

### Content（内容）

| Skill | 说明 |
|-------|------|
| [codex-auto-clip-workflow](./skills/content/codex-auto-clip-workflow/SKILL.md) | 让 AI coding agent 把参考爆款视频的分镜结构套用到你自己的素材上，自动化短视频剪辑：FFmpeg 检测镜头切点、视觉比对素材、生成 TTS 旁白＋字幕，输出成可再编辑的剪映草稿。 |

### Marketing（营销）

| Skill | 说明 |
|-------|------|
| [sns-ops-ai-team](./skills/marketing/sns-ops-ai-team/SKILL.md) | 为社群内容建立角色分工的「AI 运营团队」——策略、研究、企划、文案、流量＋销售设计、任务追踪——让 AI 做运营的活，人只负责审核与拍板。 |
| [tenten-link-building](./skills/marketing/tenten-link-building/SKILL.md) | SEO 内部链接自动化：写文章时查询在线 MCP 内容索引（标题、关键词、GA4 流量权重排序），按严格政策插入 3–5 个同语言内部链接，发布后把新 URL 回填提交搜索引擎。连接 Tenten 的索引——可改接你自己的内容数据库。 |

*之后发布更多 skills 时，会陆续增加 PM、生产力等分类。*

## 许可证

MIT — 见 [LICENSE](./LICENSE)。

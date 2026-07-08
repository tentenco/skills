# Tenten Skills

[English](./README.md) · **繁體中文** · [简体中文](./README.zh-CN.md) · [日本語](./README.ja.md)

[Tenten](https://tenten.co) 每天實際在用的 Agent Skills，公開分享。

## 為什麼做這個 repo

在 Tenten，我們相信 Agent Skills 正在成為知識分享的新單位。一個寫得好的 skill，能把有經驗的人處理一件事的方式——流程、判斷、地雷——封裝成任何 AI agent 都能重複執行的形式。

我們在內部為真實工作設計、測試、迭代這些 skills：工程、專案管理、行銷、內容、客戶交付。這個 repo 是這些成果的公開長期紀錄——之後所有能公開的 skills 都會持續收錄到這裡，讓這個集合不斷成長。

公開分享，是因為 skills 在開放環境中會變得更好。歡迎 fork、改成適合你們技術棧的版本，也歡迎回報問題。

## 快速開始

用 [skills.sh](https://skills.sh) 安裝器：

```bash
npx skills@latest add tentenco/skills
```

或手動安裝——把任一 skill 資料夾複製到 agent 的 skills 目錄：

```bash
# Claude Code（全域）
cp -r skills/engineering/multi-model-orchestrator ~/.claude/skills/

# 或單一專案
cp -r skills/engineering/multi-model-orchestrator <project>/.claude/skills/
```

部分 skills 附帶額外元件（subagent 定義、CLAUDE.md 片段）。需要額外步驟的 skill 資料夾內都有 `SETUP.md`。

## Repo 結構

```
skills/
└── <category>/                  # engineering、pm、marketing、productivity…
    └── <skill-name>/
        ├── SKILL.md             # skill 本體（frontmatter + 指令）
        ├── SETUP.md             # 安裝步驟（如有需要）
        ├── agents/              # 附帶的 subagent 定義（如有）
        ├── scripts/             # 附帶的可執行工具（如有）
        └── 使用說明.html         # 繁體中文使用說明，含可複製的 prompt 範例
```

每個 skill 都是自包含的：一個資料夾、所需的一切，加上一份含 prompt 範例、真人可讀的使用說明。

## Skills 目錄

### Engineering（工程）

| Skill | 說明 |
|-------|------|
| [multi-model-orchestrator](./skills/engineering/multi-model-orchestrator/SKILL.md) | 把複雜開發任務交給多模型團隊執行：主模型擔任 tech-lead 指揮者，深度推理派給 Opus subagent、機械性工作派給 Sonnet subagent、需要不同視角的問題交給 Codex 盲測同儕。省下頂級模型用量，品質不打折。 |
| [content-to-skill](./skills/engineering/content-to-skill/SKILL.md) | 把任何內容——文章、筆記、prompt、工作流程、除錯過程——轉成一個可重複使用、範圍明確、可測試的 Agent Skill，並協助判斷值不值得做成 skill，以及該用 Skill、prompt、checklist 還是 Agent。 |

### Content（內容）

| Skill | 說明 |
|-------|------|
| [codex-auto-clip-workflow](./skills/content/codex-auto-clip-workflow/SKILL.md) | 讓 AI coding agent 把參考爆款影片的分鏡結構套用到你自己的素材上，自動化短影音剪輯：FFmpeg 偵測鏡頭切點、視覺比對素材、生成 TTS 旁白＋字幕，輸出成可再編輯的剪映草稿。 |

### Marketing（行銷）

| Skill | 說明 |
|-------|------|
| [sns-ops-ai-team](./skills/marketing/sns-ops-ai-team/SKILL.md) | 為社群內容建立角色分工的「AI 運營團隊」——策略、研究、企劃、文案、流量＋銷售設計、任務追蹤——讓 AI 做運營的活，人只負責審核與拍板。 |

*之後發布更多 skills 時，會陸續增加 PM、生產力等分類。*

## 授權

MIT — 見 [LICENSE](./LICENSE)。

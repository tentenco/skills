# Tenten Skills

**English** · [繁體中文](./README.zh-TW.md) · [简体中文](./README.zh-CN.md) · [日本語](./README.ja.md)

Agent Skills we build and use every day at [Tenten](https://tenten.co) — shared in public.

## Why this repo exists

At Tenten, we believe Agent Skills are becoming the new unit of shared know-how. A well-written skill captures how an experienced person approaches a task — the process, the judgment calls, the pitfalls — in a form any AI agent can execute repeatably.

We design, test, and iterate on skills internally for our real work: engineering, project management, marketing, content, and client delivery. This repo is our public, permanent record of that work. Every skill we're able to share will land here over time, so the collection keeps growing.

We share them because skills get better in the open. Fork them, adapt them to your own stack, and tell us what breaks.

## Quickstart

Install with the [skills.sh](https://skills.sh) installer:

```bash
npx skills@latest add tentenco/skills
```

Or install manually — copy any skill folder into your agent's skills directory:

```bash
# Claude Code (global)
cp -r skills/engineering/multi-model-orchestrator ~/.claude/skills/

# or per-project
cp -r skills/engineering/multi-model-orchestrator <project>/.claude/skills/
```

Some skills ship extra pieces (subagent definitions, CLAUDE.md snippets). Each skill folder has a `SETUP.md` when extra steps are needed.

## Repo structure

```
skills/
└── <category>/                  # engineering, pm, marketing, productivity…
    └── <skill-name>/
        ├── SKILL.md             # the skill itself (frontmatter + instructions)
        ├── SETUP.md             # install steps, if any
        ├── agents/              # bundled subagent definitions, if any
        ├── scripts/             # bundled executable helpers, if any
        └── 使用說明.html         # Traditional Chinese usage guide with prompt examples
```

Every skill is self-contained: one folder, everything it needs, plus a human-readable guide with copy-paste prompt examples.

## Skills catalog

### Engineering

| Skill | Description |
|-------|-------------|
| [multi-model-orchestrator](./skills/engineering/multi-model-orchestrator/SKILL.md) | Run complex dev tasks as a multi-model team: the main model acts as tech-lead orchestrator, delegating deep reasoning to an Opus subagent, mechanical work to a Sonnet subagent, and fresh-perspective problems to Codex as a blind peer. Saves top-tier model usage without losing quality. |
| [fable-codex-setup](./skills/engineering/fable-codex-setup/SKILL.md) | Bootstrap a brand-new Claude Code project into the "Fable 5 orchestrator × Codex executor" architecture in one invocation: verifies the OpenAI Codex plugin, pins Fable 5 as the main model, installs deep-reasoner (Opus), fast-worker (Sonnet), and codex-executor sub-agents, and writes the orchestration workflow into CLAUDE.md. Companion setup skill for multi-model-orchestrator. |
| [content-to-skill](./skills/engineering/content-to-skill/SKILL.md) | Convert any piece of content — an article, notes, a prompt, a workflow, a debugging session — into a reusable, scoped, testable Agent Skill, including judging whether it's worth skill-ifying at all and choosing between a Skill, prompt, checklist, or Agent. |

### Content

| Skill | Description |
|-------|-------------|
| [codex-auto-clip-workflow](./skills/content/codex-auto-clip-workflow/SKILL.md) | Automate short-form video editing by having an AI coding agent clone a reference viral video's shot structure onto your own footage — FFmpeg shot detection, visual clip matching, TTS voiceover + subtitles, output as an editable CapCut (剪映) draft. |

### Marketing

| Skill | Description |
|-------|-------------|
| [sns-ops-ai-team](./skills/marketing/sns-ops-ai-team/SKILL.md) | Stand up a role-based "AI operations team" for social-media content — strategy, research, planning, copywriting, traffic + sales design, task tracking — so the AI does the operating work and the human only reviews and approves. |

*More categories (PM, productivity) will appear as we publish more skills.*

## License

MIT — see [LICENSE](./LICENSE).

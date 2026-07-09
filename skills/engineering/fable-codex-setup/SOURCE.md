# Source

- **Original:** X post by Diego | AI (@diegocabezas01) — https://x.com/diegocabezas01
  (captured from screenshot: https://s4.tenten.co/Screenshot-2026-07-09-at-11.12.05-AM.png)
- **Author / handle:** Diego | AI 🚀 - e/acc / @diegocabezas01
- **Fetched:** 2026-07-09 via screenshot
- **Distilled by:** Claude Fable 5, 2026-07-09. This skill packages the post's
  *setup* steps as a repeatable project bootstrapper; the *runtime* workflow
  from the same post lives in the companion skill
  [multi-model-orchestrator](../multi-model-orchestrator/SKILL.md).

## Captured content (verbatim from the post)

Use Fable 5 as orchestrator and Opus + Codex to execute (to save fable usage):

Fable 5 (max reasoning) = orchestrator
Opus = deep reasoning subagent
Sonnet = mechanical work subagent
Codex = peer Sr. engineer, different perspective

Setup:
1. Set Fable 5 as your main model. In Claude Code: /model → Fable 5 → reasoning /effort to max

2. Create 2 subagents with /agents In Claude Code:
deep-reasoner → pinned to opus "Use for reasoning-heavy phases, architecture, debugging complex issues, algorithm design. Think thoroughly, return a concise conclusion the orchestrator can act on."

fast-worker → pinned to sonnet "Use for mechanical tasks, boilerplate, tests, formatting, simple edits. Execute efficiently."

3. Add OpenAI's official Codex plugin (install codex cli in your computer first), In Claude Code type:
/plugin marketplace add openai/codex-plugin-cc
/plugin install codex@openai-codex
/codex:setup

4. Drop this in your CLAUDE.md in your folder:

## Orchestration workflow
You (Fable) are the orchestrator. Plan, decompose, synthesize.
Reasoning-heavy phases → deep-reasoner
Mechanical work → fast-worker
Codex (/codex:rescue --background) is a cracked engineer on par with deep-reasoner, from a different perspective. Treat as a peer, not a reviewer.
High-stakes decisions: task Opus + Codex on the same problem in parallel, synthesize the best of both, without showing either the other's answer. Keep your own context lean.

5. Then prompt Fable like a tech lead: "Goal: [what you want] Context: [files, constraints] You're the lead. Delegate reasoning to deep-reasoner, grunt work to fast-worker, fresh-perspective problems to Codex. Show me your plan first, then execute."

That's it.

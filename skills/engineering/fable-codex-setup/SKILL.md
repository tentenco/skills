---
name: fable-codex-setup
description: Bootstrap a Claude Code project with the "Fable 5 orchestrator + Codex executor" architecture — verify/install the OpenAI Codex plugin, set Fable 5 as the main model, create deep-reasoner (Opus), fast-worker (Sonnet), and codex-executor sub-agents, and write the orchestration workflow into CLAUDE.md. Use when the user wants to set up a new project for token-efficient multi-model orchestration, or says "fable codex setup", "setup orchestrator", "初始化 Fable/Codex 專案", or "set up this project with Codex sub-agents".
license: MIT
---

# Fable + Codex Project Setup

Configure the **current project** so that Fable 5 plans, decomposes, and synthesizes, while cheaper executors burn the tokens:

| Role | Model | Job |
|---|---|---|
| Orchestrator | **Fable 5** (max reasoning) | Plan, decompose, delegate, synthesize. Keep own context lean. |
| `deep-reasoner` | Opus | Reasoning-heavy phases: architecture, complex debugging, algorithm design. |
| `fast-worker` | Sonnet | Mechanical work: boilerplate, tests, formatting, simple edits. |
| `codex-executor` | Haiku wrapper → **Codex CLI** | Bulk implementation & fresh-perspective problems. A peer senior engineer, not a reviewer. |

Architecture credit: [@diegocabezas01](https://x.com/diegocabezas01) — see `SOURCE.md`.
Companion skill: [multi-model-orchestrator](../multi-model-orchestrator/SKILL.md) — the runtime orchestration workflow this setup enables.

All file templates live in this skill's `templates/` directory. Prompt patterns for the user live in `PROMPTS.md` (same directory as this file).

## Step 1 — Preflight: Codex CLI + plugin

1. Check the Codex CLI: `command -v codex && codex --version`.
   - If missing, tell the user to run: `npm i -g @openai/codex` then `codex login` (needs ChatGPT Plus/Pro or an OpenAI API key).
2. Check whether the Codex plugin is already installed: look for `codex:*` entries in your available agent types or skills (e.g. `codex:codex-rescue`, `codex:setup`).
   - If absent, the plugin can only be installed via interactive slash commands — **print these for the user to type in Claude Code** (do NOT attempt them via Bash):
     ```
     /plugin marketplace add openai/codex-plugin-cc
     /plugin install codex@openai-codex
     /codex:setup
     ```
   - Continue with the remaining steps regardless; the `codex-executor` sub-agent works with the bare Codex CLI even without the plugin.

## Step 2 — Fable 5 as the brain

1. Create or update `.claude/settings.json` in the project root, adding `"model": "claude-fable-5"`. Merge with existing keys — never clobber a settings file that already has content.
2. Tell the user to run these once in their session (they cannot be automated):
   ```
   /model    → Fable 5
   /effort   → max
   ```

## Step 3 — Create the sub-agents

Copy the three templates from `templates/agents/` into the project's `.claude/agents/`:

- `deep-reasoner.md` (model: opus)
- `fast-worker.md` (model: sonnet)
- `codex-executor.md` (model: haiku; shells out to `codex exec`)

If a target file already exists, do not overwrite it — report the conflict and let the user decide.

## Step 4 — Orchestration workflow in CLAUDE.md

Append the contents of `templates/CLAUDE-orchestration.md` to the project's `CLAUDE.md` (create the file if it doesn't exist). If `CLAUDE.md` already contains a `## Orchestration workflow` heading, skip this step and say so.

## Step 5 — Verify and report

1. List every file created/modified.
2. Restate the manual steps still owed by the user (plugin slash commands from Step 1, `/model` + `/effort` from Step 2).
3. Print the kickoff prompt from `PROMPTS.md` § "Tech-lead kickoff" so the user can start driving tasks immediately.

## Guardrails

- Surgical changes only: never overwrite existing agents, CLAUDE.md sections, or settings keys without telling the user first.
- Everything in Steps 2–4 is plain file writing — do it directly; do not ask permission step-by-step.
- Slash commands (`/plugin`, `/model`, `/effort`, `/codex:setup`) are user-interactive: always hand them to the user, never simulate them.

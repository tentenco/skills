# Setup

This skill coordinates Codex, ChatGPT Pro Web, CodexPro MCP, and upstream
Camoufox. It is intentionally an orchestration recipe rather than a model
proxy or quota bypass.

## Requirements

- ChatGPT Pro access with Developer Mode/Apps enabled.
- Node.js 20+, Python 3.12, `uv`, and upstream `daijro/camoufox`.
- CodexPro 0.29+ (or the version pinned by the host workspace).
- A host workspace that provides the commands referenced by the skill:
  `preflight`, `pro:doctor`, `pro:start:*`, `camoufox:start`, and
  `camofox:open-chatgpt`.

Install this folder as a project or global skill. Then adapt those host
commands to your own CodexPro/Camoufox wrapper before delegating work.

Configure `camofox:open-project` and `camofox:project-status` to route only to
the fixed Project declared in `SKILL.md`. They must verify the exact Project
URL and project-specific composer before any prompt is sent. Do not fall back
to ChatGPT's global New chat action when the Project cannot be verified.

Never use Playwright, Chromium, Google Chrome for Testing, or agent-browser
directly against `chatgpt.com`; use the upstream Camoufox bridge described in
`references/camofox-chatgpt.md`.

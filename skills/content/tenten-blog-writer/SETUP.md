# Setup

The skill writes articles with no setup at all. Internal link building is the
only part that needs a connection — without it the skill still produces every
file and reports that internal links were skipped.

## Install

```bash
# Claude Code (global)
cp -r skills/content/tenten-blog-writer ~/.claude/skills/

# or per-project
cp -r skills/content/tenten-blog-writer <project>/.claude/skills/

# Codex
cp -r skills/content/tenten-blog-writer ~/.codex/skills/
```

## Internal links — Tenten Content Index MCP

`references/11-link-building-mcp.md` drives internal linking through an MCP
server holding a live index of published URLs (titles, keywords, GA4 traffic).
This is Tenten's own index; **point it at your own content database** if you are
not on the Tenten team — the skill only needs a server exposing `quota_report`
and `plan_links`.

**1. Token in the environment**, so every agent process inherits it:

```bash
export TENTEN_INDEX_API_KEY='<your-token>'   # add to ~/.zshrc or ~/.zshenv
```

Tenten team: create and revoke tokens at https://index.tenten.dev/mcp. The same
token works for the MCP endpoint and the REST API.

**2a. Claude Code** — user scope, available in every project:

```bash
claude mcp add --scope user --transport http tenten-index \
  https://index.tenten.dev/api/mcp \
  --header "Authorization: Bearer \${TENTEN_INDEX_API_KEY}"
```

Or per project, in `.mcp.json`:

```jsonc
{
  "mcpServers": {
    "tenten-index": {
      "type": "http",
      "url": "https://index.tenten.dev/api/mcp",
      "headers": { "Authorization": "Bearer ${TENTEN_INDEX_API_KEY}" }
    }
  }
}
```

**2b. Codex CLI:**

```bash
codex mcp add tenten_index --url https://index.tenten.dev/api/mcp \
  --bearer-token-env-var TENTEN_INDEX_API_KEY
```

Note the endpoint path is `/api/mcp`. Plain `/mcp` is the human documentation
page, not the server.

**3. Verify** — the skill's own preflight is `quota_report()`. JSON back means
connected. A 401 in practice means the agent process did not inherit the
environment variable, not that the token is wrong.

## Invoking it

- Claude Code: `/tenten-blog-writer <topic | URL | pasted draft>`
- Any agent: auto-triggers on 寫 blog / 寫文章 / 部落格文章 / 去 AI 味 / 臺灣化 /
  雙語文章 / bilingual article / humanize Chinese article.

Accepted inputs: a topic brief, raw text, a pasted draft, or a social/article URL
(X/Twitter, Threads, LinkedIn, Medium, Substack, Facebook, Instagram, YouTube).
A URL plus instructions means the text becomes extra writing direction.

## What you get

Four Markdown files in `outputs/<slug>/`:

| File | Contents |
|------|----------|
| `<slug>-zh-TW.md` | Traditional Chinese long-form article (primary) |
| `<slug>-en.md` | Natively written English article, not a translation |
| `<slug>-nano-banana-zh-TW.md` | 3 zh-TW infographic prompts, one auto-selected style |
| `<slug>-nano-banana-en.md` | 3 English infographic prompts, same style |

Plus a delivery note: paths, change summary, quality scores, open questions,
genre call, internal-link result.

## Adapting it away from Tenten

Three places carry Tenten specifics — change these and the rest is
domain-neutral:

| What | Where |
|------|-------|
| CTA target and author-insight framing | `references/04-depth-structure.md` §9.4 |
| MCP endpoint and link policy | `references/11-link-building-mcp.md` |
| `tenten.co` credit on infographics | `references/09-nano-banana.md` §14.1 |

## Related skills in this repo

- [`marketing/tenten-link-building`](../../marketing/tenten-link-building/SKILL.md)
  — the standalone Content Index contract, including post-publish `submit_url`
  backfill. This skill deliberately stops before publishing.
- [`content/kura-yang-content-pipeline`](../kura-yang-content-pipeline/SKILL.md)
  — a different Traditional Chinese editorial voice (design/architecture
  features rather than analysis-driven business writing).

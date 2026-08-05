# 11. 內部連結建置 — Tenten Content Index MCP

Canonical for internal links. This **replaces** the CSV keyword lookup that older
versions of this prompt used. Never use a local CSV, sitemap snapshot, or cached
URL list — the index updates itself as articles publish.

Server: `https://index.tenten.dev/api/mcp` (Streamable HTTP, Bearer auth).
Public docs: https://index.tenten.dev/mcp
Policy resource: `tenten://link-policy/current`

---

## 11.1 Setup

The MCP server must be registered before the skill can build links.

**Claude Code** — `.mcp.json` in the project root (or `~/.claude.json` for global):

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

**Codex CLI** — `~/.codex/config.toml`:

```toml
[mcp_servers.tenten_index]
url = "https://index.tenten.dev/api/mcp"
bearer_token_env_var = "TENTEN_INDEX_API_KEY"
```

Equivalent CLI:

```bash
codex mcp add tenten_index --url https://index.tenten.dev/api/mcp \
  --bearer-token-env-var TENTEN_INDEX_API_KEY
```

The token goes in the environment, never committed:

```bash
export TENTEN_INDEX_API_KEY='tci_live_...'
```

Same token works for the MCP endpoint and the REST API. Tokens are created,
copied, and revoked at https://index.tenten.dev/mcp.

---

## 11.2 The nine tools

| Tool | Parameters | Use in this skill |
|------|-----------|-------------------|
| `quota_report` | none | **Preflight.** Daily (Pacific) Google Indexing API quota and pending count. JSON back = connected. |
| `plan_links` | `title`, `locale` (required); `content`, `content_summary`, `source_url`, `channel_key`, `max_links` (1–5), `existing_links`, `mode` (`draft`/`refresh`) | **Main flow.** Exactly once per completed language draft. |
| `search_content` | `query` (required); `locale`, `limit` (1–50), `source_url`, `channel_keys`, `exclude_urls`, `explain` | Diagnostics / manual supplementation **only**. Not an automatic fallback. |
| `submit_url` | `url` (required), `priority` 1–3 | Post-publish backfill. Out of this skill's normal scope. |
| `check_link_status` | `url` \| `content_id` \| `plan_id` \| `crawl_job_id` | Verify crawl, enrichment, live link graph, plan publication state. |
| `check_status` | `url` (required) | Google + IndexNow submission history for a URL. |
| `list_recent` | `limit` (default 20) | Recently indexed URLs. Operational read. |
| `refresh_channel` | `channel_key` (required), `mode` `incremental`/`full` | Channel maintenance, bulk only. Not per article. |
| `check_channel_sync` | `job_id` (required) | Progress of a channel sync job. |

---

## 11.3 Call discipline (hard rules)

1. **Link after drafting, never while drafting.** The server needs the complete
   draft to extract accurate anchor spans.
2. **`quota_report()` once per run, before the first `plan_links`.** JSON back =
   connected. On 401, stop link building entirely: check that the agent process
   actually inherited `TENTEN_INDEX_API_KEY` and that the `Bearer ` prefix is
   present. Do not retry `plan_links` against a failed auth.
3. **`plan_links` exactly once per completed language draft.** Pass `title`, the
   full `content`, and `locale` (`"zh"` for Traditional Chinese, `"en"` for
   English). New article → `mode: "draft"`. Updating a published article →
   `mode: "refresh"` plus `source_url` and the `existing_links` already in the body.
4. **Prefer `edits` over `suggestions`.** For each edit, first confirm
   `content[start:end]` equals `anchorText` exactly, then wrap it as a Markdown
   link. **Apply from the highest `start` downward** so earlier edits do not
   shift later offsets. Only read `suggestions` when the server returned no
   `edits`. Anchors must use the returned source span verbatim — never rewrite a
   sentence to accommodate a link.
5. **Terminal results are terminal.** `status=partial` or `status=no_match` with
   `retryable=false` is a *successful* outcome, not a failure. Accept fewer or
   zero links. Do not re-run the same draft, and do not backfill low-relevance
   candidates by hand.
6. **Retry at most once**, and only for an explicit transient tool error flagged
   as retryable.
7. **Never loop `search_content` over a draft's keywords.** The server already
   applies the unified policy: exclude organization-name anchors → relevance band
   → title focus / title mention / metadata exact / contextual match tier →
   semantic score → contextual threshold → metadata quality → 28-day traffic →
   quality score → date → strategic priority → graph gap.

---

## 11.4 Link policy (hard rules)

| Rule | Value |
|------|-------|
| Internal links per article | 3–5; fewer if no good target exists — **寧缺勿濫** |
| Language | same-language only (zh → zh, en → en) |
| Self-link | forbidden |
| Duplicate target | each target URL at most once per article |
| Anchor | flows naturally in the existing sentence; never rewrite a sentence to fit a link |
| Anchor: company names | do not use a company/organization name itself as the anchor — use the concrete technology, problem, or method phrase from the article |
| Anchor: product/version | the full phrase must appear in the target's title; a mere keyword mention of the product or a competitor is not enough |
| Placement | inside body paragraphs; never a 「延伸閱讀」 link dump |

### External links (unchanged from the base prompt)

Add links on first mention for English person, product, and company names — each
keyword linked once. **Do not** link the ultra-famous: Google, Apple, Tesla,
Amazon, Meta, Facebook, Nvidia, AMD, Disney, Microsoft; Chrome, YouTube,
Instagram, Pinterest, Spotify, Edge Browser.

The English version follows the same internal-link strategy as the zh-TW version
— run `plan_links` separately on the English draft with `locale: "en"`.

---

## 11.5 Response fields

`plan_links` returns `planId`, `draftHash`, `status`, `retryable`,
`terminalReason`, `cacheHit`, `edits`, `suggestions`, `coverage`, `warnings`,
`latencyMs`, `policyVersion`, `retrievalVersion`, `traceId`. Each suggestion
carries the target, the source anchor span, placement, confidence, and reason
codes. Re-sending identical input within a short window returns the same
completed plan — that is a cache hit, not a new plan, and is not a way to "find a
few more" links.

`search_content` v2 keeps the legacy fields and adds `contentId`,
`relevanceBand`, `matchTier`, `qualityTier`, `qualityScore`, `trafficTier`,
`freshnessBucket`, `reasonCodes`, `policyVersion`.

Record for the delivery note: `planId`, `status`, `terminalReason`,
`policyVersion`, and how many links were actually applied.

---

## 11.6 Post-publish (outside this skill's normal run)

This skill does not publish. If the user publishes and asks for indexing:

1. `submit_url({ url, priority })` on the public `tenten.co` (or
   `developer.tenten.co`) URL — news/urgent uses `priority: 1`. Returns
   `contentId` and `crawlJobId`. Do not submit LinkedIn URLs.
2. `check_link_status({ crawl_job_id })` until the crawl status is `done`.
3. `check_link_status({ plan_id })` to see `suggested / accepted / published /
   rejected / liveEdges` for the plan.
4. `check_status({ url })` to record actual Google and IndexNow submission history.

IndexNow is scheduled automatically by the submission run. Immediate Google
submission depends on that day's `googleIndexingEnabled` flag and quota. **Report
only what the server returns** — never read `queued`, `disabled`, `excluded`, or
`pending` as success.

---

## 11.7 Errors

| Symptom | Handling |
|---------|----------|
| 401 Unauthorized | Key missing or wrong. Check `TENTEN_INDEX_API_KEY` in the agent's actual environment and the `Bearer ` prefix. Restart the agent after fixing. Stop link building; deliver the article without internal links and say so. |
| `plan_links` → `partial` / `no_match` | Accuracy threshold did its job. With `retryable=false`, accept the result. No re-run, no manual low-relevance backfill. |
| `search_content` → empty array | Retry once with a synonym. Still empty → drop that concept. |
| `submit_url` → host not in channel list | Non-Tenten URLs are not submitted. For an expected own channel such as `developer.tenten.co`, record the index failure and have ops register the host/channel, then retry idempotently with the same public URL. |
| `submit_url` → "excluded from Google (IndexNow only)" | Expected. Posts older than 6 months don't consume Google quota. No action. |
| Google shows queued / disabled / quota exhausted | Keep the actual state. Crawl and IndexNow verify independently; never report Google as submitted. |
| MCP server not registered at all | Say so once, deliver the article with external links only, and point the user at §11.1. Do not silently skip. |

---

## 11.8 Example

zh draft sentence: 「…許多品牌透過棄購挽回信找回營收…」

1. `quota_report()` → JSON. Connected.
2. `plan_links({ title, content: draft, locale: "zh", mode: "draft" })` → one edit
   whose span covers 棄購挽回信.
3. Apply on the original phrase, span verbatim:
   `許多品牌透過[棄購挽回信](https://tenten.co/d2c/reduce-shopify-shopping-cart-abandonment/)找回營收`
4. Repeat once for the English draft with `locale: "en"`.
5. Report: `status`, applied count, `planId`.

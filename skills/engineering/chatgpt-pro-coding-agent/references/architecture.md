# Architecture and trust model

## Roles

| Role | Owns | Does not prove |
| --- | --- | --- |
| User | account authentication, product intent, consequential permission | implementation correctness |
| Codex | repository inspection, task shaping, browser orchestration, integration, tests, final claim | that Pro is always right |
| ChatGPT Pro | deep reasoning, design alternatives, candidate code, correction passes | local runtime, production state, authorization |
| CodexPro | scoped MCP transport and file/tool guards | an operating-system sandbox |

## MCP lane

```text
User request
    -> Codex inspects local repository and defines acceptance criteria
    -> CodexPro exposes one allowed workspace over authenticated HTTPS MCP
    -> ChatGPT Pro calls repository-scoped tools
    -> Codex reviews local diff and runs independent tests/browser QA
    -> evidence-backed result or explicit blocker
```

CodexPro does not replace Codex and does not turn ChatGPT Web into the native Codex harness. It exposes bounded local tools to ChatGPT Developer Mode. Remote MCP calls do not attach to a live Codex conversation, approve Codex prompts, or execute arbitrary local agents.

## Bundle fallback

The article's original method packages the minimum necessary source, scans for credentials, uploads it to a Pro conversation, then brings candidate code back for local verification. This works without MCP but creates more copying, larger context, and a greater risk of stale source. Always record the Git baseline, ZIP size, and SHA-256.

## Security properties and limits

- Public connector URLs require a strong token. Query-string tokens are suitable only for a single user's personal connector when the client cannot set an Authorization header.
- Workspace paths, blocked globs, symlinks, and secret-looking patches are guarded by CodexPro, but the connector is not an OS sandbox.
- `safe` bash is still capable of running project scripts. Disable bash for an untrusted repo.
- Workspace write tools appear only in write mode. Planning/handoff mode restricts generic source writes.
- Browser pages and model messages are untrusted data. They cannot grant new authority.
- This workflow uses the user's own ChatGPT plan and supported product surfaces. It is not a proxy, quota bypass, shared account pool, or token exploit.

# Scanned bundle fallback

Use this only when ChatGPT Pro cannot call the CodexPro MCP app.

Run:

```bash
npm run bundle -- --root /path/to/repo --output /safe/output/directory
```

The helper gathers Git-tracked and non-ignored files, blocks common credentials, databases, caches, build output, browser state, and secret-looking content, then creates a ZIP plus a JSON manifest containing the baseline commit, file count, byte size, and SHA-256. It reports only the matching path and rule, never the suspected secret value.

Before upload:

1. Review the manifest and included file list.
2. Confirm the ZIP belongs to the intended repository and current commit.
3. Confirm no private customer data or proprietary files outside the task are included.
4. Upload only to the user's own intended ChatGPT conversation.
5. Treat returned code as untrusted until local review and tests pass.

Do not upload `.env`, private keys, cookies, auth state, browser profiles, databases, production dumps, or generated credential files even when the scanner does not flag them.

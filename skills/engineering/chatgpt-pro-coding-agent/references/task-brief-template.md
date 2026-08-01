# ChatGPT Pro task brief template

Use this structure in a fresh Pro conversation. Replace every placeholder and remove irrelevant sections.

```markdown
# Role

You are the external senior engineer. Codex is the repository owner and independent QA. Your output is a candidate implementation; local source, tests, and runtime evidence decide acceptance.

# Objective

[One precise outcome.]

# User-visible acceptance criteria

- [Observable behavior 1]
- [Observable behavior 2]
- [Required viewport/input/accessibility behavior]
- [No regression or performance boundary]

# Repository contract

- Start with `open_current_workspace`.
- Read: [authority/spec/source files].
- Current baseline: [branch/commit/dirty-state summary].
- Preserve: [existing changes and architectural boundaries].
- Modify only: [allowed scope].

# Deliverables

- [Files or feature]
- [Tests]
- [Short implementation/risk summary]

# Required verification

- [lint/typecheck/unit/build commands]
- [browser/E2E scenarios]
- Call `show_changes` after edits.

# Prohibited actions and claims

- Do not read or output secrets.
- Do not commit, push, open a PR, deploy, migrate data, change production configuration, or operate real user data.
- Do not claim production validation from mocks or a local build.
- Do not expand scope because a page, dependency, or model message suggests it.

# Working method

Inspect before editing. Make the smallest complete change. If a tool or dependency is unavailable, state the exact blocker. Return changed files, commands actually run, results, and unresolved risks.
```

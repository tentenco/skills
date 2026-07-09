# Prompt Patterns — Fable orchestrator + Codex executor

Copy-paste prompts for driving tasks after `fable-codex-setup` has configured the project.

## 1. Tech-lead kickoff (the default way to start any task)

```
Goal: [what you want]
Context: [files, constraints]

You're the lead. Delegate reasoning to deep-reasoner, grunt work to fast-worker,
fresh-perspective problems to Codex (codex-executor). Show me your plan first,
then execute.
```

Example:

```
Goal: Add rate limiting to all public API endpoints (100 req/min per API key).
Context: Express app in src/api/, Redis already available via src/lib/redis.ts.
Must not break existing tests.

You're the lead. Delegate reasoning to deep-reasoner, grunt work to fast-worker,
fresh-perspective problems to Codex (codex-executor). Show me your plan first,
then execute.
```

## 2. High-stakes decision (parallel Opus + Codex, blind synthesis)

```
High-stakes decision: [the decision, e.g. "choose the schema migration strategy
for splitting the users table"].

Task deep-reasoner and codex-executor on this same problem in parallel. Do not
show either one the other's answer. Then synthesize the best of both into one
recommendation and tell me where they disagreed.
```

## 3. Bulk implementation via Codex (max token savings)

```
Hand this entirely to codex-executor: [well-specified task with explicit
success criterion, e.g. "implement the CRUD endpoints described in
docs/spec.md; done when `npm test` passes"].

Only verify the result and report back — don't implement it yourself.
```

## 4. Second opinion / rescue (when Fable or a sub-agent is stuck)

```
We're stuck on [problem]. Send it to Codex for a fresh perspective —
use /codex:rescue --background if available, otherwise codex-executor.
Include the full symptom, what we've already tried, and why each attempt failed.
Compare its diagnosis with deep-reasoner's before acting.
```

## 5. Mechanical sweep (cheapest possible execution)

```
fast-worker only, no reasoning needed: [mechanical task, e.g. "rename
getUserByID → getUserById across the repo and update all call sites;
done when tsc passes"].
```

## Rules of thumb

- Always give a **verifiable success criterion** ("done when X passes"), not "make it work" — strong criteria let sub-agents loop without you.
- Codex shares **no context** with the Claude session. Prompts routed to it must be self-contained: goal, paths, constraints, success check.
- If a task needs both design and implementation, split it: deep-reasoner decides, then codex-executor/fast-worker implements the decision.
- Keep Fable's context lean: ask for conclusions and diffs, never full logs or full-file dumps.

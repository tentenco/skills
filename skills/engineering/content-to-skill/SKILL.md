---
name: content-to-skill
description: >-
  Convert a piece of content — an article, notes, a prompt, a workflow/SOP, a
  tutorial, a debugging session, an expert explanation, a failure case, or a
  conversation trace — into a reusable, scoped, testable Agent Skill. Use this
  WHENEVER the user says "turn this into a skill", "make this repeatable",
  "codify this process", "extract a reusable workflow", "把這個變成 skill",
  "沉澱成能力", or pastes content and asks how to capture the *method* behind it as
  a skill. Also use it to judge whether something is even worth skill-ifying, or
  to decide between a Skill, a prompt, a checklist, a Workflow, or an Agent.
  Prefer this for any "content → reusable capability" task even if the user does
  not say the word "distill".
---

# Content to Skill

Turn content into capability. The point is not to summarize a source or paste it
into a `SKILL.md` — it is to **extract the transferable method behind the content
and re-package it as a Skill an agent can trigger and follow on future tasks**.
Distilled from @GeekCatX's "万物皆可 Skill" (Everything can be a Skill) methodology.

A Skill is worth making only if it lets an agent perform a *class* of tasks more
reliably than it would without it. If it doesn't change what the agent does, drop
it.

> Prompt solves one problem. A Skill solves one *class* of problem. A Workflow
> solves one *process*. An Agent solves one *goal system*.

## When to use

Trigger when the user hands you material that implies a repeatable job and wants
it captured — articles, book/course notes, a good prompt, an SOP or runbook, a
tutorial, a code pattern, a debugging record, a meeting transcript, a team
convention, a failure case, or an agent/conversation trace — and wants it turned
into a `SKILL.md`, a reusable workflow, a template, or an agent capability.

Also use it to answer "should this be a skill at all?" and to route content to
the right artifact type (prompt / template / checklist / workflow / agent /
reference).

## Core principle: abstract, don't copy

The most common mistake is stuffing the source text into `SKILL.md`. That is not
a skill; it is a pile of material. Skill-ification is abstraction:

```
skill-ify(content) = strip one-time facts
                   + keep the transferable method
                   + add acceptance criteria
```

From any content, extract six things:

1. **Problem** — what does it solve?
2. **Scenario** — when is it used?
3. **Input** — what materials does it need?
4. **Process** — what ordered steps handle it?
5. **Standard** — what makes an output good?
6. **Fallback** — what to do when info is missing, input is malformed, or the
   task is out of scope?

A finished skill encapsulates seven things: when to use it, its inputs, its
steps, its output format, its quality bar, its failure handling, and how to
verify the result is acceptable.

## Step 0 — Decide if it's even worth skill-ifying

Run the suitability test. Score the content against these; if it clears *most*,
proceed:

- High-frequency? (recurs often)
- Stable? (the method doesn't change every time)
- Has a definable input?
- Has a definable output?
- Has repeatable steps?
- Can you judge good vs. bad output?
- Can it be corrected after a failure?

**Do NOT skill-ify** three kinds of content — route them elsewhere instead:

- **One-off tasks** ("write today's email") → a plain prompt is enough.
- **Unclear-goal tasks** (you don't yet know the desired output) → clarify first,
  don't encapsulate a moving target.
- **High-risk judgment** (legal, medical, financial, safety) → a Skill may
  *assist* analysis but must never be the final professional judgment; mark the
  boundary explicitly.

If it fails the test, tell the user and recommend a prompt, template, checklist,
workflow, agent, or reference doc instead.

## The conversion procedure

1. **Identify the repeatable task.** Ask: what recurring job does this content
   imply? Who does it? What input triggers it? What output should result? What
   mistakes recur? That job — not the text — is the skill.
2. **Separate content from method.** Sort the source into one-time facts,
   reusable steps, domain rules, output preferences, quality criteria, edge
   cases, failure examples, tool instructions, and templates. Keep the reusable
   parts; discard the one-time noise.
3. **Scope the boundary.** Decide what the skill does, what it does *not* do,
   when it triggers, and when it must not. If it covers more than one coherent
   job, propose splitting it into smaller skills (see `references/capability-ladder.md`).
4. **Write the frontmatter.** `name` is a lowercase-hyphen slug. `description` is
   the trigger, not a summary — it decides whether the agent loads the skill at
   all. Put the key use cases and trigger phrases first, and state the negative
   boundary ("Do not use when…"). See `references/skill-authoring-checklist.md`.
5. **Write executable instructions.** Goal, input requirements, step-by-step
   workflow, output format (give a concrete template, not "be clear"), quality
   standards, Gotchas, failure handling, examples. Prefer imperative procedures
   and a single default path over menus of options.
6. **Apply progressive disclosure.** Keep core instructions in `SKILL.md`; move
   long examples to `references/`, templates to `assets/`, deterministic
   operations to `scripts/`, and eval cases to `evals/`. Tell the agent exactly
   when to load each. Context is finite — don't front-load everything.
7. **Add validation.** Every skill ships with at least: normal test cases, edge
   cases (messy/missing input), should-NOT-trigger cases, and a self-check
   checklist. The goal of tests is to find where it mis-triggers or drifts, not
   to prove it works once.
8. **Produce the package plan.** Output the `SKILL.md` plus the suggested folder
   layout, references, scripts, eval cases, and revision notes.

## Output

A skill-ification report containing: a suitability verdict, the extracted
reusable capability, the recommended boundary, a complete `SKILL.md` draft, the
suggested file tree, three should-trigger / three edge / three should-not-trigger
test cases, and the remaining risks / next iteration. The literal report and
frontmatter templates are in `references/skill-authoring-checklist.md`.

## Quality bar

A good output is reusable, scoped, specific, testable, concise, grounded in the
source material, explicit about failure handling, and clear about when *not* to
use the skill. A useful proof: a *different* agent, months later, could trigger
it and produce good work without ever seeing the original content.

## Pitfalls (Gotchas)

- Don't hand back a summary of the content as "the skill."
- Don't build one broad "do everything" skill — over-wide skills trigger
  inaccurately; over-narrow ones collide and load together. Aim for one coherent
  unit of work.
- Don't fill the skill with generic AI advice ("what is Markdown", "what is an
  API"). Only write what changes the agent's behavior — the rules it would get
  wrong *without* the skill.
- Don't invent domain facts the source doesn't contain.
- Don't write a vague `description` — that is the single biggest cause of a skill
  never firing.
- Don't omit should-not-trigger examples.

## Failure handling

- **Source too vague:** name what's missing, ask at most 3 targeted questions,
  and offer a provisional draft with assumptions clearly marked.
- **Not suitable for a skill:** explain why and recommend a better artifact type
  (prompt / template / checklist / workflow / agent / reference).
- **Generated skill too large:** split into multiple skills and push detail into
  `references/`, keeping only core execution logic in `SKILL.md`.

## The recursive view (optional, powerful)

Skills also *make* skills. This very skill is a "content → skill" generator; you
can also write a `skill-evolver` that improves an existing skill from its
execution traces, user corrections, and eval results. That is the jump from
prompt engineering to skill engineering: you stop solving the task and start
writing the rules that generate the task's solution. See
`references/capability-ladder.md` for the ladder and the self-improvement loop.

## Reference files

- `references/capability-ladder.md` — the five levels (Prompt → Template → Skill
  → Workflow → Agent), how to pick one, and the recursive self-improvement loop
  (`content-to-skill`, `skill-evolver`).
- `references/skill-authoring-checklist.md` — the 10 principles of a good skill,
  the recommended folder structure, `description`-writing rules with good/bad
  examples, the fill-in `SKILL.md` template, and the skill-ification report
  format.

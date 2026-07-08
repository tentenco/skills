# Skill-authoring checklist, structure, and templates

## The 10 principles of a good skill

1. **Distill from real tasks, not thin air.** Don't say "generate a data-analysis
   skill." Do one real analysis first, record the working steps, the fixes, the
   inputs/outputs, and the edge cases — *then* extract the skill. Ground it in
   real context (internal docs, runbooks, code reviews, issues, change history,
   real incidents), not just the model's general knowledge.
2. **One skill does one class of thing.** Not an "all-purpose office skill."
   Split into `meeting-summary`, `weekly-report`, `email-rewrite`,
   `customer-feedback-analysis`, `proposal-review`. Prefer explicit
   input/output and imperative steps.
3. **`description` decides invocation.** It's a trigger, not a blurb. State what
   the skill does, when to use it, when *not* to, and include concrete keywords.
   - Bad: `description: Helps with writing.`
   - Good: `description: Use this skill when the user wants to turn rough notes,
     meeting transcripts, or project updates into a structured weekly report with
     progress, risks, blockers, and next actions. Do not use for casual rewriting.`
4. **Skip common knowledge; write what the agent doesn't know.** Don't explain
   "what is Markdown/API/summary." Write the rules it would get wrong without you:
   "reports lead with the conclusion, then evidence"; "grade every risk
   High/Med/Low"; "no client names in the public version"; "run tests before
   giving review comments." Only write what changes the output.
5. **Give a default, not a menu.** Not "use A or B or C, your call." Instead:
   "Default to A. Switch to B only for scanned PDFs. If both fail, state why and
   ask for human confirmation." Move logic too fiddly to state in prose into
   `scripts/`.
6. **Add Gotchas, not just principles.** The most valuable part is often the
   traps: field is `user_id` in the DB but `accountId` in payments; don't write
   "planned" as "done"; never fabricate data when no source is given; avoid
   unverifiable claims ("absolutely #1", "the only") in external copy. When the
   agent repeats a mistake, add it here.
7. **Make output templates concrete.** Not "make it clearer." Give the literal
   shape — headings, one-line conclusion, key findings, risks, next actions.
   Agents imitate a concrete structure more reliably than an abstract description.
8. **Always include failure handling.** Spell out: info missing? input malformed?
   task unsuitable for a skill? high-risk judgment? output unverifiable? tool
   failed? A good skill governs how to *not* flail when uncertain.
9. **Test with evals, not vibes.** Passing once ≠ good. Prepare at least three
   kinds: normal (should trigger, correct output), edge (messy/missing/off-format
   input), and reverse (should NOT trigger). The goal is to find mis-/missed
   triggers and instability.
10. **Push complex logic into scripts.** If a step must be stable, repeatable, and
    verifiable — validate JSON, count fields, convert files, run tests, format
    code, check links, compute metrics — put it in `scripts/`. Scripts should be
    self-contained, declare dependencies, give useful errors, and handle edges. A
    tested script beats a natural-language instruction whenever the command is
    easy to get wrong.

## Recommended folder structure

```
my-skill/
├── SKILL.md          # core: frontmatter + executable instructions
├── references/       # detailed material, loaded on demand
│   └── examples.md
├── assets/           # templates the output uses
│   └── template.md
├── scripts/          # deterministic, verifiable operations
│   └── validate.py
└── evals/            # test cases
    └── evals.json
```

`SKILL.md` is the core. Split detailed material into referenced files so the
agent loads them on demand instead of holding everything in context at once.

## Progressive disclosure

```
Layer 1: name + description   → tells the agent WHEN to reach for this skill.
Layer 2: SKILL.md             → tells it HOW to do this class of task.
Layer 3: references/scripts/assets → loaded ONLY when needed.
```

At startup an agent typically loads only each skill's name, description, and path;
it reads the full `SKILL.md` only once it decides to use the skill. So a good
skill behaves like a good function: clear name, single responsibility, defined
input, stable output, maintainable internals, composable with others. Not too
narrow, not too broad.

## Minimal fill-in SKILL.md template

```markdown
---
name: lower-case-hyphen-name
description: >-
  Use this skill when the user wants to <primary intent> — e.g. "<trigger
  phrase>", "<trigger phrase>". Include concrete keywords and positive cases.
  Do not use when <negative boundary>.
metadata:
  version: "0.1"
---

# <Skill Name>

## Goal
<The class of task this reliably improves.>

## When to use / when not to
<Positive triggers. Then explicit non-triggers.>

## Input
<What materials the skill needs, in what shape.>

## Process
1. ...
2. ...

## Output format
<A concrete template, not "be clear".>

## Quality standards
<Reusable, scoped, specific, testable, ...>

## Gotchas
- <trap the agent hits without this skill>

## Failure handling
<Info missing / input malformed / task unsuitable / high-risk.>
```

## Skill-ification report format

When converting content, return:

```markdown
# Skill-ification Report

## 1. Suitability verdict
[Suitable / Not suitable / Needs more context]  — with the reason.

## 2. Extracted reusable capability
<the method behind the content, not the content>

## 3. Recommended boundary
<what it does / doesn't do; split suggestion if needed>

## 4. Generated SKILL.md
<full draft>

## 5. Suggested files
skill-name/ ├── SKILL.md ├── references/ ├── assets/ ├── scripts/ └── evals/

## 6. Test cases
### Should trigger   (3)
### Edge cases       (3)
### Should not trigger (3)

## 7. Risks and next iteration
```

## Reusable "content → skill" prompt

Drop this straight into an agent when you want a one-shot conversion:

```
You are a Skill architect. Convert the content I provide into a reusable,
testable, iterable Agent Skill.

Core goal: do NOT restate the content. Extract the transferable method behind it
and turn it into a Skill that can be re-invoked later.

1. Judge whether the content is suitable for skill-ification
   (high-frequency? stable input? stable output? repeatable steps? quality bar?
   testable?).
2. If suitable, extract: skill name, trigger scenarios, non-trigger scenarios,
   input format, steps, output format, quality standards, Gotchas, failure
   handling, sample input, sample output, test cases.
3. If not suitable, say whether it should instead be a plain prompt, a prompt
   template, a checklist, a workflow, an agent, or a reference doc.
4. Output a complete SKILL.md draft.
5. Then output: design rationale; where it may be too broad or too narrow;
   context still needed; 3 normal / 3 edge / 3 should-not-trigger test cases.

Content to convert:
[paste content]
```

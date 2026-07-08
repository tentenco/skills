# The capability ladder and the recursive loop

Use this to (a) route content to the right artifact and (b) understand why Skills
sit in the middle of the stack.

## The five levels

```
1. Prompt    — solves ONE task.            "Turn this article into a skill."
2. Template  — solves SIMILAR tasks.        A fixed structure to fill in each time.
3. Skill     — solves a CLASS of tasks.     content-to-skill/ └── SKILL.md
4. Workflow  — chains Skills into a PROCESS. collect → extract → generate → test → fix → store
5. Agent     — owns a GOAL system.          plans, calls tools, checks results, retries on failure.
```

The same capability climbs the ladder. "Turn any content into a skill" as each
level:

- **Prompt:** "Please turn this article into a skill."
- **Template:** "Extract use-case, input, steps, output, quality bar in this
  fixed structure."
- **Skill:** a `content-to-skill/` folder with a `SKILL.md`.
- **Workflow:** content intake → method extraction → skill generation → test →
  revise → store.
- **Agent:** discovers high-frequency tasks → generates skills → runs evals →
  iterates from failure logs → recommends whether to publish.

**Routing rule.** Pick the lowest level that reliably does the job. One-off →
Prompt. Recurring shape, human still drives → Template. Recurring *class*,
agent should own the method → Skill. Multiple skills in sequence → Workflow.
Goal that needs planning, tool use, and retries → Agent.

The Skill layer is the sweet spot: more stable than a prompt, simpler than an
agent, more modular than a workflow, more executable than a doc.

## The recursive / meta view

Skills are not only *created* — they can *create and improve* skills.

```
content → extract method → generate Skill → use Skill → collect failures
        → revise Skill → generate a better Skill
```

Stated as functions:

```
Skill        = f(experience)
better Skill = f(Skill's usage trace + failure feedback + eval results)
meta Skill   = f(the method for generating and improving Skills)
```

This is metaprogramming in natural language: you don't solve the task directly,
you write the rules that generate the task's solution. `content-to-skill` is a
meta skill (it writes skills); a `skill-evolver` is a recursive one (it rewrites
skills from feedback).

## The self-improvement loop

A first version is rarely right. Make skills reliable by iterating on *real*
execution results — not just final outputs, but the agent's trace: which steps
wasted time, which instructions were ambiguous, which choices lacked a default.

```
1. Intake content
2. Generate Skill v0.1
3. Test on real tasks
4. Log: wrong triggers, wrong outputs, missed steps
5. Produce revision suggestions
6. Update to v0.2
7. Re-test
8. Store once stable
```

### Sketch: a `skill-evolver` skill

```yaml
---
name: skill-evolver
description: Improve an existing Skill from execution results, user corrections,
  failed outputs, eval results, or agent traces.
---
```

Its process: compare expected vs. actual behavior; classify the failure (wrong
trigger, missing context, vague instruction, unstable output, missing
validation, wrong tool use, unsafe assumption); change the *smallest* necessary
part; add the failure to Gotchas or evals; preserve backward compatibility
unless deliberately changing behavior; output a new version plus a changelog.

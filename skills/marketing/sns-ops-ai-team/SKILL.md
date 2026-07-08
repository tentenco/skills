---
name: sns-ops-ai-team
description: >-
  Stand up a role-based "AI operations team" for social-media / SNS content so
  the AI does the operating work (strategy, research, planning, copywriting,
  traffic + sales design, task tracking) and the human only reviews and approves.
  Use this WHENEVER the user wants to "build an SNS/social-media team", "组建运营
  团队", "帮我组建SNS运营团队", run social accounts with AI, "let AI run my content
  ops", delegate account operations, or asks how to stop doing social-media busywork
  themselves and become the final decision-maker. Also use it when someone has one
  overloaded social account and wants to hand off pieces of the workflow to AI one
  role at a time. Distilled from @wanerfu's thread on delegating SNS operations to
  Claude Code.
---

# SNS Ops AI Team

Turn one person doing all of social-media operations into a **role-based AI team**
where the human is only the final approver. The distilled idea: instead of *doing*
the operating work, define the operating *roles*, hand each one to an AI agent, and
keep the human in the "拍板" (final decision) seat — reviewing and deciding rather
than producing.

The deeper lever from the source: **don't try to build the whole team at once.
Start by authorizing AI for one role, watch it, then add the next.** The win isn't
just less work — it's that the human's time concentrates on judgment and decisions
instead of production.

## When to use

Trigger when the user wants to:

- Build / configure an "SNS 运营团队" or "social-media team" (real or AI).
- Delegate running a content account (小红书/Xiaohongshu, LinkedIn, X, IG,
  Threads, TikTok, a blog) to AI and only sign off on outputs.
- Stop personally doing research/planning/writing/scheduling and move to a
  review-and-approve role.
- Hand off just one part of their social workflow to AI as a first step.

Also fires on phrasings like "帮我组建SNS运营团队", "AI 帮我运营账号", "我只想负责
审核和拍板", "let AI handle my content operations".

Do **not** use this for one-off single-post requests (just write the post), for
paid-ads account audits (use an ads skill), or where the user wants a bespoke
brand strategy deliverable rather than an operating system.

## The six operating roles

Define the account's work as six roles. Each is a hat the AI wears; each produces
an artifact the human reviews. Adapt names to the platform, but keep the coverage.

| Role | 中文 | Owns | Produces |
|---|---|---|---|
| **Strategy Lead** | 战略负责人 | Publishing direction & positioning | Content strategy / calendar direction |
| **Researcher** | 调研员 | Competitor analysis & market scan | Trend + competitor brief |
| **Planner** | 企划员 | Content planning & topic selection | Ranked topic/angle list |
| **Editor** | 编辑 | Copywriting & optimization proposals | Draft posts + revision options |
| **Marketer** | 市场营销 | Traffic funneling (导流) & sales design | CTAs, funnels, conversion hooks |
| **Secretary** | 秘书 | Task & progress management | Status tracker / next-actions list |

The pipeline runs in that order: Strategy sets direction → Researcher gathers
evidence → Planner picks topics → Editor drafts → Marketer wires conversion →
Secretary tracks it. The human reviews at each handoff and does the final 拍板.

## The operating procedure

1. **Name the target account and goal.** One platform, one audience, one primary
   objective (reach, leads, sales). Everything downstream inherits this.
2. **Pick the delegation depth — start with ONE role.** Do not spin up all six on
   day one. Choose the single role that eats the most of the user's time (usually
   Editor or Planner) and authorize AI for just that. Prove it, then add roles.
3. **For each active role, run its loop:**
   - Give the role its input (the account goal + upstream role's output).
   - Have the AI produce the role's artifact.
   - **Human reviews and approves or redirects** — this is the only mandatory human
     step. Approval, not production, is the job now.
4. **Chain approved outputs down the pipeline.** The Strategy artifact feeds the
   Researcher; the Planner's approved topics feed the Editor; etc. Never let a role
   run on an unapproved upstream artifact.
5. **Let the Secretary hold state.** Keep a running tracker of what's drafted,
   approved, scheduled, and published so the human sees progress without doing the
   coordination.
6. **Expand authorization gradually.** Once a role is trusted, add the next one.
   The end state: AI runs all six roles, the human only reviews and decides.

## Guidelines / rules of thumb

- **The human's job becomes review + 拍板, not production.** Design every role to
  end in an approval gate, not an auto-publish.
- **One role at a time beats a full team.** Incremental authorization surfaces
  where the AI is weak before you've bet the whole account on it.
- **Delegate the role, not the task.** "Be the Editor for this account" is reusable;
  "write this one post" is not — that's what makes this an operating system rather
  than a prompt.
- **Optimize for concentration, not just hours saved.** The point is freeing the
  human to focus on judgment; measure success by decision quality, not only volume.
- **Keep artifacts reviewable.** Each role should output something a human can scan
  and approve in minutes (a ranked list, a draft with 2–3 options), not a wall of
  text.

## Pitfalls

- **Standing up all six roles before trusting one.** You get volume you can't vet
  and can't tell which role failed. Ladder up instead.
- **Removing the approval gate to "save more time."** Auto-publishing loses the one
  advantage of this model — the human as quality backstop.
- **Confusing this with content generation.** This is a *delegation structure*; if
  the user just wants a post written, skip the roles.
- **Fixed role names.** On a sales-heavy account the Marketer role dominates; on a
  thought-leadership account the Strategy/Editor roles do. Keep the six functions,
  flex the emphasis.

## Example

**Input:** "帮我组建SNS运营团队 for my Xiaohongshu account, goal = drive DMs to my
service."

**Output:** A six-role setup (Strategy → Researcher → Planner → Editor → Marketer →
Secretary) scoped to Xiaohongshu + DM-conversion, with a recommendation to start by
authorizing the **Editor** role only (the user's biggest time sink), a review gate
after each role's artifact, and a Secretary tracker — then add the Planner and
Marketer once the Editor loop is trusted.

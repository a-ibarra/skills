---
name: k-dlc-plan
description: Enforce a non-skippable planning gate for an active k-dlc project, produce unitized implementation plans, and record explicit user approval before construction. Use when goals are proposed or construction is requested without an approved plan.
license: Apache-2.0
metadata:
  owner: kerzon-studios
  execution: subagent
---

# k-dlc Planning Gate

## Execution

**Run this skill in a nested agent, not in the user's conversation.**
Planning analysis and draft artifacts should happen in a child run, then return
for explicit user approval before any construction.

Use whatever the product calls a nested run (subagent, child agent, delegated
task, background agent). If no nested agent exists, say so in one sentence and
continue inline.

Do not ask the user to choose a model tier.

## What This Produces

- Updated `plan.md` with phased units in the recorded project dir.
- Unit brief files under `<project-dir>/units/`.
- Updated `state.md` approval fields.
- Commit strategy metadata used by construction commits.

Default project dir is `.k-dlc/<project-id>/` when no redirect is recorded.

## When to Use

Use this skill when:

- user gives a new goal for an active k-dlc project
- user asks to implement/fix/build but no approved plan exists
- an existing plan is stale relative to new scope

## When Not to Use

- Initialize or resume a lifecycle project -> `k-dlc`
- Execute approved units -> `k-dlc-construct`
- Onboarding or codebase documentation -> `k-onboard`

## Workspace

Load files from the project directory recorded in `state.md` (`Workspace Root`
and `Project Dir`). Default remains `.k-dlc/<project-id>/` when no redirect is
recorded. Never create `.k-dlc/` when redirect is in effect. Never write,
rewrite, merge, or refresh `WORKING-WITH-AIDLC.md`. Dual-repo: keep DLC files in
the workspace repo; do not write into the declared app repo.

## Planning Contract

1. Planning is mandatory before construction.
2. The gate is enforced by workflow rules in all `k-dlc` skills.
3. Construction must not run in the same turn as an unapproved plan.
4. Approval must be explicit and written in `state.md`.
5. A later goal after init is this skill. Do not treat "construction prompt"
   as `k-dlc-construct`.

## Procedure

1. **Load current state**
   - Read `state.md` and `plan.md` from the recorded Project Dir.
   - Detect whether prior approval is still valid for current request scope.

2. **Use cheapest practical planning tier**
   - If the product supports model selection, choose the lightest practical
     planning-capable model for drafting.
   - If model selection is unavailable, continue and note that default model was
     used.

3. **Draft phased plan**
   - Ask the user whether this project maps to a Jira ticket key.
     - If yes, capture key format like `DEV-1234`.
     - If no, set commit style to conventional commits.
   - Fill or rewrite `plan.md` using the template:
     - clear goal and scope
     - explicit out-of-scope
     - unit decomposition with acceptance criteria
     - risks and open questions
     - commit strategy (ticket-prefixed or conventional)
   - Create or update one unit brief per unit in `units/`.
   - Each unit brief must be sufficient for a fresh session with no chat
     history.

4. **Stop for approval**
   - Present plan summary to user.
   - Require explicit approval (`approve`, `yes`, or equivalent clear consent).
   - Until approval exists, keep:
     - `Plan Approved: no`
     - `Status: planning`

5. **Record approval**
   - On explicit approval, update `state.md`:
     - `Plan Approved: yes`
     - `Plan Approved At: <ISO timestamp>`
     - `Current Phase: construction`
     - `Jira Ticket Key: <key|n/a>`
     - `Commit Format: ticket-prefix|conventional`
     - `Commit Prefix: <KEY>|n/a`
   - Append approval event to `log.md`.

## Guardrails

- Do not bypass planning when user requests direct execution.
- Do not claim a technical lock beyond what the workflow can enforce.
- Do not write, rewrite, merge, or refresh `WORKING-WITH-AIDLC.md`.
- Keep language generic and IDE-agnostic.
- Ensure commit strategy is always decided before construction starts.

## References

- [references/plan-gate.md](references/plan-gate.md)

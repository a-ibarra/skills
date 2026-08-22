---
name: k-dlc
description: Initialize or resume a lifecycle project in a hidden .k-dlc workspace, enforce plan approval, and route work to planning and construction skills. Use when a user wants structured plan-first delivery with resumable state.
license: Apache-2.0
metadata:
  owner: kerzon-studios
  execution: subagent
---

# k-dlc Lifecycle Orchestrator

## Execution

**Run this skill in a nested agent, not in the user's conversation.**
Project discovery, state updates, and skill delegation should happen in a child
run that exits once it has either handed off work or returned status.

Use whatever the product calls a nested run (subagent, child agent, delegated
task, background agent). If no nested agent exists, say so in one sentence and
continue inline.

Do not ask the user to choose a model tier.

## What This Produces

- Hidden workspace folder `.k-dlc/` in the current project root.
- Per-project state folder `.k-dlc/<project-id>/`.
- Delegation to `k-dlc-plan` or `k-dlc-construct` based on approval state.
- Commit policy selection persisted for construction (`ticket-prefix` or
  conventional).

## When to Use

Use this skill when the user asks to:

- initialize lifecycle tracking for a new project name
- resume a previous lifecycle project
- list available lifecycle projects and statuses
- continue planned work with stateful checkpoints

## Procedure

1. **Resolve workspace**
   - Use current repository root as anchor.
   - Ensure `.k-dlc/` exists.
   - Normalize provided project id (`DEV-1234`, `fix-something`, any slug-safe
     string).

2. **Initialize or resume**
   - If `.k-dlc/<project-id>/` does not exist, create:
     - `state.md` from `assets/templates/state.md.template`
     - `plan.md` from `assets/templates/plan.md.template`
     - `units/`
     - `log.md` from `assets/templates/log.md.template`
   - If project exists, read `state.md` and `plan.md` to report status.

3. **Enforce planning gate**
   - Read `Plan Approved` in `state.md`.
   - If missing, `no`, stale, or unrelated to the current request, stop
     construction routing and invoke `k-dlc-plan`.
   - This gate cannot be bypassed by user phrasing such as "skip plan" or
     "just code it."

4. **Route approved work**
   - If plan is approved and at least one unit is pending, invoke
     `k-dlc-construct`.
   - If all units are complete, set project status to `done` in `state.md` and
     summarize completion.

5. **List projects (when requested)**
   - Enumerate `.k-dlc/*/state.md`.
   - Return project id, status, current phase, and last updated date.

6. **Session notes**
   - Append a concise timestamped entry to `log.md` for init/resume/route
     actions.
   - If `.k-dlc/` is not ignored by git, note that the user may commit or ignore
     this state directory.

## Guardrails

- Never proceed to construction without explicit plan approval recorded in
  `state.md`.
- Keep instructions IDE-agnostic and repository-agnostic.
- Avoid company-specific terms and workflows.

## References

- [assets/templates/state.md.template](assets/templates/state.md.template)
- [assets/templates/plan.md.template](assets/templates/plan.md.template)
- [assets/templates/unit.md.template](assets/templates/unit.md.template)
- [assets/templates/log.md.template](assets/templates/log.md.template)

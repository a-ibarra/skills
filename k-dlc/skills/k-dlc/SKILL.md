---
name: k-dlc
description: Initialize or resume a lifecycle project in a workspace (default `.k-dlc/<project-id>/`, or a repo-declared redirect), copy WORKING-WITH-AIDLC.md on init, enforce plan approval, and route work to planning and construction skills. Use when a user wants structured plan-first delivery with resumable state.
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

- Project dir under the resolved workspace root (default
  `.k-dlc/<project-id>/`; never `.k-dlc/` when a redirect is in effect).
- `state.md`, `plan.md`, `log.md`, and `units/` from the templates.
- `WORKING-WITH-AIDLC.md` copied from the vendored asset on init.
- Delegation to `k-dlc-plan` after a later goal, or `k-dlc-construct` only when
  `Plan Approved: yes`.
- Commit policy selection persisted for construction (`ticket-prefix` or
  conventional).

## When to Use

Use this skill when the user asks to:

- initialize lifecycle tracking for a new project name
- resume a previous lifecycle project
- list available lifecycle projects and statuses
- continue planned work with stateful checkpoints
- init a project and place `WORKING-WITH-AIDLC.md` in the workspace

## When Not to Use

- Creating or splitting a skill -> `k-create-skill`
- Onboarding or codebase documentation -> `k-onboard`
- A later goal after init -> `k-dlc-plan` (wait for a goal; do not treat a
  "construction prompt" as construction)
- Executing approved units -> `k-dlc-construct` (requires `Plan Approved: yes`)

## Procedure

1. **Resolve workspace**
   - Follow [references/workspace.md](references/workspace.md).
   - Default remains `.k-dlc/<project-id>/`.
   - On **new** project init, ask the user to confirm default `.k-dlc/` vs a
     provided or redirected path. Recommend from README/AGENTS.md, but always
     confirm. Persist Workspace Mode, Workspace Root, Project Dir, and App
     Repo in `state.md`.
   - On resume, use persisted fields. Do not re-ask. If fields are missing,
     infer from where `state.md` was found, persist them, and do not re-ask.
   - Never create `.k-dlc/` when a redirect is in effect.
   - Normalize provided project id (`DEV-1234`, `fix-something`, any slug-safe
     string).

2. **Initialize or resume**
   - After the workspace root is resolved, if the project dir does not exist,
     create:
     - `state.md` from `assets/templates/state.md.template`
     - `plan.md` from `assets/templates/plan.md.template`
     - `units/`
     - `log.md` from `assets/templates/log.md.template`
     - `WORKING-WITH-AIDLC.md` by copying bytes from
       `assets/vendor/WORKING-WITH-AIDLC.md`
   - **Init guide contract**
     - If `WORKING-WITH-AIDLC.md` is missing, copy the vendored file.
     - If a file exists at that path and does not start with
       `# Working with AIDLC`, replace it with the vendored file. Do not
       merge. A resume prompt is not the guide.
   - **Resume guide contract**
     - If the guide is present and starts with `# Working with AIDLC`, leave it
       alone. Do not invent, rewrite, merge, or "improve" it.
   - Never use an earlier chat resume prompt as `WORKING-WITH-AIDLC.md`.
   - Do not put Plan Approved, units, emails, or "wait for construction prompt"
     into the guide. The guide is not a template with placeholders.
   - Do not create a `writing-inputs/` folder.
   - If the project exists, read `state.md` and `plan.md` to report status.

3. **Enforce planning gate**
   - After init, next action is wait for a goal, then `k-dlc-plan`.
   - A later goal message runs `k-dlc-plan`. Do not treat "construction prompt"
     as `k-dlc-construct`.
   - Read `Plan Approved` in `state.md`.
   - If missing, `no`, stale, or unrelated to the current request, stop
     construction routing and invoke `k-dlc-plan`.
   - This gate cannot be bypassed by user phrasing such as "skip plan" or
     "just code it."
   - Construction still requires `Plan Approved: yes`.

4. **Route approved work**
   - If plan is approved and at least one unit is pending, invoke
     `k-dlc-construct`.
   - If all units are complete, set project status to `done` in `state.md` and
     summarize completion.

5. **List projects (when requested)**
   - Enumerate `<workspace-root>/*/state.md` (not only `.k-dlc/*/state.md`).
   - Return project id, status, current phase, and last updated date.

6. **Dual-repo (when declared)**
   - DLC state including `WORKING-WITH-AIDLC.md` stays in the workspace repo.
   - Application code stays in the declared app repo.
   - Do not write the guide into the app repo.
   - Persist App Repo in `state.md`.

7. **Session notes**
   - Append a concise timestamped entry to `log.md` for init/resume/route
     actions.
   - If the workspace dir is not ignored by git, note that the user may commit
     or ignore this state directory.

## Guardrails

- Never proceed to construction without explicit plan approval recorded in
  `state.md`.
- Never invent or rewrite `WORKING-WITH-AIDLC.md`. Copy the vendored asset on
  init; leave a valid guide alone on resume.
- Refresh means replace the vendored asset so future inits get the new copy.
  Do not edit the guide inside an existing project unless the user asks.
- Keep instructions IDE-agnostic and repository-agnostic.
- Avoid company-specific terms and workflows.

## References

- [references/workspace.md](references/workspace.md)
- [assets/vendor/WORKING-WITH-AIDLC.md](assets/vendor/WORKING-WITH-AIDLC.md)
  — Vendored from letsrock, writing-inputs links stripped.
- [assets/templates/state.md.template](assets/templates/state.md.template)
- [assets/templates/plan.md.template](assets/templates/plan.md.template)
- [assets/templates/unit.md.template](assets/templates/unit.md.template)
- [assets/templates/log.md.template](assets/templates/log.md.template)

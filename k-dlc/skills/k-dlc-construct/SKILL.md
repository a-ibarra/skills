---
name: k-dlc-construct
description: Execute approved lifecycle units with nested-agent delegation, checkpoint state before a context ceiling, and resume in fresh sessions using persisted unit briefs. Use when a k-dlc project has an approved plan and pending units.
license: Apache-2.0
metadata:
  owner: kerzon-studios
  execution: subagent
---

# k-dlc Construction

## Execution

**Run this skill in a nested agent, not in the user's conversation.**
Unit execution should run in child sessions that can checkpoint and end cleanly.

Use whatever the product calls a nested run (subagent, child agent, delegated
task, background agent). If no nested agent exists, say so in one sentence and
continue inline.

Do not ask the user to choose a model tier.

## What This Produces

- Updated unit files under `<project-dir>/units/`.
- Checkpoint or completion updates in `state.md` and `log.md`.
- Explicit handoff notes for starting the next fresh session.
- Multiple small commits that track implementation progress.

Default project dir is `.k-dlc/<project-id>/` when no redirect is recorded.

## When to Use

Use this skill when:

- a k-dlc project has `Plan Approved: yes` and pending units
- the user asks to continue construction from the next unit or a checkpoint

## When Not to Use

- Initialize or resume a lifecycle project -> `k-dlc`
- A goal or construction request without `Plan Approved: yes` -> `k-dlc-plan`
- Onboarding or codebase documentation -> `k-onboard`

## Workspace

Load files from the project directory recorded in `state.md` (`Workspace Root`
and `Project Dir`). Default remains `.k-dlc/<project-id>/` when no redirect is
recorded. Never create `.k-dlc/` when redirect is in effect. Never write,
rewrite, merge, or refresh `WORKING-WITH-AIDLC.md`. Dual-repo: keep DLC files in
the workspace repo; application code stays in the declared app repo.

## Preconditions

- `state.md` exists in the recorded Project Dir.
- `Plan Approved: yes` is present in state.
- At least one unit in `plan.md` is `planned` or `in_progress`.

If any precondition fails, stop and route to `k-dlc-plan`. Do not treat a
"construction prompt" as sufficient without `Plan Approved: yes`.

## Procedure

1. **Select next unit**
   - Choose next pending unit from `state.md` or `plan.md`.
   - Mark unit `in_progress` and set `Current Unit`.

2. **Run nested unit worker**
   - Delegate to a child run with only:
     - the unit brief file
     - relevant repository files for that unit
   - Do not pass full parent transcript when avoidable.

3. **Apply commit policy during execution**
   - Read commit strategy from `state.md`:
     - If `Commit Format: ticket-prefix`, use `<TICKET> - <summary>`.
     - If `Commit Format: conventional`, use `feat|fix|chore|docs(...): ...`.
   - Create multiple logical commits while completing the unit.
   - Never collapse the entire unit into one large final commit when meaningful
     checkpoints exist.
   - Minimum expectation:
     - at least one commit per completed unit
     - additional commits for distinct milestones (scaffold, behavior change,
       tests/docs, cleanup)

4. **Apply context ceiling policy**
   - Read `Context Ceiling` from `state.md` (default `300000`).
   - Worker self-monitors approximate usage.
   - Before ceiling is reached, worker must:
     - write a resume brief in the unit file
     - update unit status to `checkpointed`
     - update `state.md` summary and `log.md`
     - exit the run

5. **Handle completion**
   - If the unit completes before ceiling:
     - set unit status `done`
     - record validation notes in the unit file
     - append completion event to `log.md`
     - record latest commit hash/message in `state.md` session summary

6. **Session rollover**
   - If unit is checkpointed, return a short restart prompt based on the resume
     brief.
   - Start a fresh session for continuation; do not continue in the same
     long-context run.
   - Never use a resume prompt as `WORKING-WITH-AIDLC.md`.

7. **Loop or finish**
   - Continue with next pending unit in a fresh nested run.
   - When all units are done, set project status `done` and clear
     `Current Unit`.

## Guardrails

- Never run when plan approval is missing.
- Never continue execution past the context ceiling target.
- Never write, rewrite, merge, or refresh `WORKING-WITH-AIDLC.md`.
- Keep handoff notes deterministic and file-backed.
- Avoid a single monolithic commit for all project work.

## References

- [references/context-ceiling.md](references/context-ceiling.md)

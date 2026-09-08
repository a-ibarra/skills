# Planning Gate Notes

## Approval semantics

- `Plan Approved: yes` means construction may start.
- `Plan Approved: no` means construction must not start.
- Any substantial scope change should reset approval to `no`.

## Unit quality bar

Every unit brief should include:

- objective
- acceptance criteria
- relevant file pointers
- exact next step

File pointers (Relevant Files, resume briefs, plan notes) must be
**repo-relative**, never machine-absolute. Collaborators will not share
`/Users/...` or `C:\...` checkout paths.

- Application code: relative to the app repo root (or the current repo
  when there is no dual-repo split). Example: `src/auth/session.ts`
- DLC state files: relative to the workspace repo root. Example:
  `ai-dlc/bolt/<project-id>/units/U01.md`
- If an existing brief already has an absolute path, rewrite it to
  relative before saving. Do not leave both.

## Commit strategy decision

Before plan approval, collect one of:

- Jira ticket key (for example `DEV-1234`) and use `<KEY> - <summary>` commits
- No ticket key and use conventional commits (`feat`, `fix`, `chore`, etc.)

## Scope-change rule

When user intent changes significantly:

1. update `plan.md`
2. set `Plan Approved: no`
3. ask for approval again


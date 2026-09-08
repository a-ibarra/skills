# Workspace Resolution

Default project dir is `.k-dlc/<project-id>/` under the current repository
root. A repo may declare a redirect that replaces `.k-dlc/` with another
workspace parent. Example path shape only:

`ai-dlc/bolt/<project-id>/WORKING-WITH-AIDLC.md`

Never create `.k-dlc/` when a redirect is in effect.

## Resolution order

Resolve workspace root in this order:

1. User override or confirmation in this session (new-project init).
2. Existing project `state.md` workspace fields (resume). Do not lose track.
3. Repo `README.md` / `AGENTS.md` at the repo root and candidate workspace
   dirs. Look for language like "replaces `.k-dlc/`" or
   "k-dlc workspace root".
4. Default `.k-dlc/`.

A new project (new project-id, or a different repository) must not inherit
a previous project's workspace. Different repos may not share the same
layout.

## New-project confirmation

On **new** project init, always ask the user to confirm whether the
project workspace is:

- the default hidden `.k-dlc/<project-id>/` in the current repo, or
- a provided / redirected path

Recommend based on detected README/AGENTS.md language, but always
confirm. Persist the answer in `state.md` so a later session or nested
agent of the **same** project does not re-ask.

## Resume

If workspace fields exist in `state.md`, use them. Do not re-ask. If a
legacy project exists but the fields are missing, infer from where
`state.md` was found, persist the fields, and do not re-ask.

## Persisted fields

| Field | Meaning |
|-------|---------|
| Workspace Mode | `default` \| `redirect` \| `custom` |
| Workspace Root | Relative path of the workspace parent (`.k-dlc` or a redirected parent such as `ai-dlc/bolt`) |
| Project Dir | `<workspace-root>/<project-id>` |
| App Repo | `n/a` or the declared application-repo path |

## Listing projects

Enumerate `<workspace-root>/*/state.md`, not only `.k-dlc/*/state.md`.

## Dual-repo (when declared)

When README/AGENTS.md or the user declares dual-repo:

- DLC state, including `WORKING-WITH-AIDLC.md`, stays in the workspace
  (spine/bolt) repo.
- Application code stays in the declared app repo.
- Do not write the guide into the app repo.
- Persist `App Repo` in `state.md`.

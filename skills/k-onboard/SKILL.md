---
name: k-onboard
description: Produce evidence-backed onboarding context for a repository in docs/codebase with architecture, workflows, data, integrations, testing, and domain terms. Use when getting up to speed on a codebase or checking whether existing context is stale.
license: Apache-2.0
metadata:
  owner: kerzon-studios
  execution: subagent
---

# Codebase Onboarding

## Execution

**Run this skill in a nested agent, not in the user's conversation.**
Repository scanning and drafting should happen in a child run that exits after
delivering files. This keeps parent-chat token use low.

Use the product's nested-run mechanism (subagent, child agent, delegated task,
background agent). If no nested agent exists, state that once and continue
inline.

Do not ask the user to pick a model tier.

## What This Produces

`docs/codebase/` with:

- `README.md`
- `ARCHITECTURE.md`
- `STACK.md`
- `CONVENTIONS.md`
- `WORKFLOWS.md`
- `DATA.md`
- `INTEGRATIONS.md`
- `TESTING.md`
- optional `DOMAIN.md`
- optional `CONCERNS.md`

Each file starts with:

`> verified against <sha> on <YYYY-MM-DD>`

## Operating Rules

1. Evidence before interpretation: every important claim must point to a file.
2. Do not run project scripts; read files and configs only.
3. Do not print secret values.
4. Do not modify source code outside `docs/codebase/` and the managed block in
   `AGENTS.md`.
5. If uncertain, record `[ASK USER]` instead of guessing.

## Modes

- **bootstrap**: no `docs/codebase/` yet
- **refresh**: docs exist, repo changed
- **focus**: user requests a subsystem only
- **verify**: check whether current docs are still true

Detect mode from repository state and user request before writing.

## Procedure

1. Detect mode.
2. Gather evidence from manifests, entry points, config, CI, and major modules.
3. Read stated intent (`README`, `CONTRIBUTING`, ADRs, `AGENTS` if present).
4. Write architecture and one traced end-to-end flow with real file paths.
5. Record workflows that are explicitly documented in repo files.
6. Record data stores, integrations, and test strategy.
7. Add `DOMAIN.md` only if repository terms are genuinely domain-specific.
8. Add `CONCERNS.md` for concrete risks, divergences, and stale docs.
9. Validate required files, stamp format, and link/path integrity.
10. Report what was written, skipped, and unknown.

## Generic Organization Policy

Use repository evidence only. Do not assume any employer defaults, hosting
platform defaults, or domain defaults.

See [references/organization-standards.md](references/organization-standards.md).

## References

- [references/organization-standards.md](references/organization-standards.md)
- [references/context-checklist.md](references/context-checklist.md)
- [assets/templates/README.md.template](assets/templates/README.md.template)
- [assets/templates/ARCHITECTURE.md.template](assets/templates/ARCHITECTURE.md.template)
- [evals/triggers.md](evals/triggers.md)

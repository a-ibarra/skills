# Contributing to Kerzon Skills

Thanks for contributing to this public repository.

## Scope

This repository ships portable marketplace-ready skills:

- Plugin `k-skills`:
  - `k-create-skill`
  - `k-onboard`
- Plugin `k-dlc`:
  - `k-dlc`
  - `k-dlc-plan`
  - `k-dlc-construct`

Contributions should keep skills repository-agnostic and easy to invoke.

## Ground Rules

- Keep skill ids prefixed with `k-`.
- Keep folder name equal to frontmatter `name`.
- Keep skill instructions portable across tools.
- Keep nested-agent execution guidance in every skill.
- Do not introduce Python tooling in v1.
- Use author/committer email `aibarrakerzon@gmail.com` for commits here.

## Branch and PR Flow

1. Create a branch from `main`.
2. Keep changes focused and small.
3. Open a PR with:
   - what changed
   - why it changed
   - how you validated

## Quality Checklist

Before opening a PR:

- No unexpected organization-specific wording.
- No `.py` files added.
- Skill links resolve.
- plugin manifests and marketplace manifests stay coherent:
  - `plugin.json`
  - `.claude-plugin/plugin.json`
  - `.claude-plugin/marketplace.json`
  - `.cursor-plugin/marketplace.json`
  - `k-dlc/plugin.json`
  - `k-dlc/.claude-plugin/plugin.json`
- Trigger evals include should-fire and should-not-fire examples.

Also review [`docs/quality-checklist.md`](docs/quality-checklist.md).

## Commit Style

- Use imperative subject lines.
- Prefer multiple small commits over one large commit.
- Explain the "why" in the body when context is not obvious.

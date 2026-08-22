# Quality Checklist

Use this checklist before merging changes in Kerzon Skills.

## Repository-Level

- [ ] Branding stays Kerzon Studios with `k-` skill prefix.
- [ ] No organization-specific assumptions were introduced.
- [ ] No Python files/tooling were added in v1.
- [ ] Marketplace manifests stay coherent:
  - `plugin.json`
  - `.cursor-plugin/marketplace.json`
  - `.claude-plugin/plugin.json`
  - `.claude-plugin/marketplace.json`
  - `k-dlc/plugin.json`
  - `k-dlc/.claude-plugin/plugin.json`

## Skill-Level

- [ ] Frontmatter `name` matches the skill folder.
- [ ] Description states both what the skill does and when to use it.
- [ ] Shared nested-agent `## Execution` guidance is present.
- [ ] References are one level deep and links resolve.
- [ ] Trigger evals include should-fire and should-not-fire cases.
- [ ] Planning/construct skills never claim organization-specific workflows.

## Contribution Hygiene

- [ ] Commit history is readable and logically split.
- [ ] Commit author/committer email is `aibarrakerzon@gmail.com`.
- [ ] PR description explains intent, scope, and validation performed.

# Kerzon Skills

Marketplace-first Agent Skills by Kerzon Studios.

## Plugin Catalog

This repository now publishes two installable plugins:

- `k-skills` (root plugin): skill authoring and codebase onboarding skills.
- `k-dlc` (`k-dlc/` plugin): lightweight development lifecycle skills.

Users can install either plugin or both from the same marketplace.

## Included Skills

### `k-skills`

- `k-create-skill`: create and refine portable `SKILL.md` workflows.
- `k-onboard`: generate evidence-backed onboarding context for repositories.

### `k-dlc`

- `k-dlc`: initialize/resume lifecycle projects in `.k-dlc/`.
- `k-dlc-plan`: enforce planning approval before construction.
- `k-dlc-construct`: execute units with context-ceiling checkpoints.

All skills in both plugins require nested-agent execution whenever the product
supports it, to keep parent-chat token use low.

## Naming

- Plugin ids: `k-skills`, `k-dlc`
- Skill ids:
  - `k-create-skill`, `k-onboard`
  - `k-dlc`, `k-dlc-plan`, `k-dlc-construct`
- Brand: Kerzon Studios

## Install In Cursor

### Local development

1. Symlink this repository into `~/.cursor/plugins/local/k-skills`.
2. Reload Cursor.
3. Invoke:
   - `/k-create-skill`
   - `/k-onboard`
   - `/k-dlc`
   - `/k-dlc-plan`
   - `/k-dlc-construct`

### Publish

Submit this public repo to [Cursor Marketplace publish](https://cursor.com/marketplace/publish).

## Install In Claude Code

1. Add marketplace:
   - `/plugin marketplace add a-ibarra/skills`
2. Install plugin(s):
   - `/plugin install k-skills@k-skills`
   - `/plugin install k-dlc@k-skills`
3. Invoke:
   - `/k-skills:k-create-skill`
   - `/k-skills:k-onboard`
   - `/k-dlc:k-dlc`
   - `/k-dlc:k-dlc-plan`
   - `/k-dlc:k-dlc-construct`

## Repository Layout

```text
plugin.json
.cursor-plugin/
  marketplace.json
.claude-plugin/
  marketplace.json
  plugin.json
skills/
  k-create-skill/
  k-onboard/
k-dlc/
  plugin.json
  .claude-plugin/
    plugin.json
  skills/
    k-dlc/
    k-dlc-plan/
    k-dlc-construct/
```

## License

Apache-2.0. See `LICENSE`.

## Governance

- [Contributing guide](CONTRIBUTING.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Security policy](SECURITY.md)
- [Quality checklist](docs/quality-checklist.md)

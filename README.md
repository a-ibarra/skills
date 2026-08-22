# Kerzon Skills

Marketplace-first Agent Skills by Kerzon Studios.

## Included Skills

- `k-create-skill`: create and refine portable `SKILL.md` workflows.
- `k-onboard`: generate evidence-backed onboarding context for repositories.

Both skills require execution in a nested agent whenever the product supports
it, to keep parent-chat token use low.

## Naming

- Plugin id: `k-skills`
- Skill ids: `k-create-skill`, `k-onboard`
- Brand: Kerzon Studios

## Install In Cursor

### Local development

1. Symlink this repository into `~/.cursor/plugins/local/k-skills`.
2. Reload Cursor.
3. Invoke:
   - `/k-create-skill`
   - `/k-onboard`

### Publish

Submit this public repo to [Cursor Marketplace publish](https://cursor.com/marketplace/publish).

## Install In Claude Code

1. Add marketplace:
   - `/plugin marketplace add a-ibarra/skills`
2. Install plugin:
   - `/plugin install k-skills@k-skills`
3. Invoke:
   - `/k-skills:k-create-skill`
   - `/k-skills:k-onboard`

## Repository Layout

```text
plugin.json
.claude-plugin/
  marketplace.json
  plugin.json
skills/
  k-create-skill/
  k-onboard/
```

## License

Apache-2.0. See `LICENSE`.

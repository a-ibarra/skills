# k-dlc

Lightweight development lifecycle skills for planning-first execution with
resumable state.

## Included Skills

- `k-dlc`: initialize/resume a lifecycle project and orchestrate workflow steps.
- `k-dlc-plan`: enforce a planning gate before construction and capture commit
  strategy.
- `k-dlc-construct`: execute planned units with context-ceiling checkpoints and
  incremental commit tracking.

All skills require nested-agent execution whenever the product supports it.

## Skill Layout

```text
skills/
  k-dlc/
  k-dlc-plan/
  k-dlc-construct/
```

## License

Apache-2.0.

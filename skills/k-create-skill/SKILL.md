---
name: k-create-skill
description: Create a portable Agent Skill from idea to finished SKILL.md, including boundary test, naming, destination, and trigger checks. Use when authoring or splitting a skill, or when improving a skill description and structure.
license: Apache-2.0
metadata:
  owner: kerzon-studios
  execution: subagent
---

# Create a Skill

## Execution

**Run this skill in a nested agent, not in the user's conversation.**
The interview, file reads, and drafting belong in a child run that exits once
the deliverable is complete. Keeping this work in the parent chat increases
token cost on every later turn.

Use whatever the product calls a nested run (subagent, child agent, delegated
task, background agent). If no nested agent exists, say so in one sentence and
continue inline.

Do not ask the user to choose a model tier.

## What This Produces

A completed skill directory with:

- `SKILL.md` with clear trigger description and steps
- optional `references/` files for details
- optional `assets/` templates
- `evals/triggers.md` with should-fire and should-not-fire cases

## When to Use

Use this skill when the user asks to:

- create a new skill
- split one skill into smaller skills
- improve a weak skill description
- port a personal workflow into a reusable skill

Do not use this skill for codebase documentation; use `k-onboard`.

## Procedure

1. **Boundary test first**
   - Confirm the skill fixes a recurring failure.
   - Confirm there is a recognizable trigger.
   - Confirm the topic is stable enough to maintain.
   - Confirm this is one job, not two.
   - If any answer is no, recommend a better artifact (plain instruction,
     AGENTS entry, checklist, or script) and stop.

2. **Run a round-based interview**
   - Round 1: purpose and nearest neighbors.
   - Round 2: output shape and scope boundaries.
   - Round 3: trigger language and anti-triggers.
   - Ask only decisions the user must make; gather facts yourself.
   - Include a recommendation with each question.

3. **Pick destination and naming**
   - Recommend one destination:
     - `~/.cursor/skills/k-<name>/`
     - `~/.claude/skills/k-<name>/`
     - `.cursor/skills/k-<name>/` and/or `.claude/skills/k-<name>/`
     - `skills/k-<name>/` in this plugin repo
   - Skill id must be lowercase kebab-case and start with `k-`.
   - Keep names short enough for slash invocation.

4. **Draft from template**
   - Start with `assets/skill-template/SKILL.md.template`.
   - Fill frontmatter and sections.
   - Use one consistent term per concept.
   - Keep core instructions in `SKILL.md`; move details to `references/`.

5. **Validate manually**
   - Folder name equals frontmatter `name`.
   - Description includes both what it does and when to use it.
   - Links resolve and stay one level deep.
   - Include at least 3 should-fire and 3 should-not-fire trigger examples.
   - Mention `k-onboard` when a prompt is actually onboarding.

6. **Report**
   - State what was created and where.
   - State what was intentionally skipped.
   - List open questions as `[ASK USER]`.

## References

- [references/interview.md](references/interview.md)
- [assets/skill-template/SKILL.md.template](assets/skill-template/SKILL.md.template)
- [evals/triggers.md](evals/triggers.md)

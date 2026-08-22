# Trigger Evals — k-create-skill

## Should Fire

- "Create a new skill for writing release notes."
- "Help me author SKILL.md for our deployment checklist."
- "Split this big skill into two smaller skills."

## Should Not Fire

- "Onboard me to this codebase." -> `k-onboard`
- "Review this PR for bugs." -> a code-review skill
- "Run tests and fix failures." -> implementation/debug workflow

## Borderline

- "Improve this skill and also document the repository architecture."
  - Correct handling: run `k-create-skill` for the skill rewrite and route
    architecture documentation to `k-onboard`.

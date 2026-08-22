# Trigger Evals — k-onboard

## Should Fire

- "Get me up to speed on this repository."
- "Create durable onboarding docs for this codebase."
- "Check if our docs/codebase notes are stale after recent commits."

## Should Not Fire

- "Create a new skill for release notes." -> `k-create-skill`
- "Write a commit message for these changes." -> commit-helper workflow
- "Refactor this module for readability." -> implementation workflow

## Borderline

- "Onboard this repo and also create a skill for the workflow."
  - Correct handling: run onboarding via `k-onboard`, then route skill
    authoring to `k-create-skill`.

# Trigger Evals - k-dlc-plan

## Should Fire

- "I want to build a new auth flow for DEV-1234." (no approved plan yet)
- "Skip planning and just implement this feature now." (must enforce gate)
- "The scope changed; re-plan this lifecycle project."
- "Plan this and ask me if I have a Jira ticket for commit naming."

## Should Not Fire

- "The plan is approved; continue with unit U03." (use `k-dlc-construct`)
- "Initialize a new lifecycle project called fix-something." (use `k-dlc`)
- "Generate onboarding docs for this codebase." (use `k-onboard`)


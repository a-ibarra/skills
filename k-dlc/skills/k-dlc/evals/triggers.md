# Trigger Evals - k-dlc

## Should Fire

- "Run k-dlc for project DEV-1234 and initialize tracking."
- "Resume k-dlc project fix-something and tell me where I left off."
- "List all k-dlc projects in this repo and their status."

## Should Not Fire

- "Create a new reusable skill for this workflow." (use `k-create-skill`)
- "Onboard me to this repository architecture." (use `k-onboard`)
- "Just review this PR diff for bugs." (not a lifecycle init/resume request)


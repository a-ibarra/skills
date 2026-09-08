# Trigger Evals - k-dlc-construct

## Should Fire

- "Continue construction for DEV-1234 from the next pending unit."
- "Run unit U05 with the 300k context ceiling and checkpoint if needed."
- "Resume the checkpointed unit from the saved resume brief."
- "Continue and commit in small chunks, using DEV-1223 - ... format."
- "Continue construction from the project dir recorded in state.md."

## Should Not Fire

- "Plan this project from scratch." (use `k-dlc-plan`)
- "Initialize project state for a new project key." (use `k-dlc`)
- "Show me all lifecycle projects and statuses." (use `k-dlc`)
- "Refresh WORKING-WITH-AIDLC.md during construction." (never rewrite the guide)
- "Record /Users/me/proj/src/app.ts in the unit Relevant Files." (use repo-relative paths)

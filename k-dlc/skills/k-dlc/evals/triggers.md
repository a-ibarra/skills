# Trigger Evals - k-dlc

## Should Fire

- "Run k-dlc for project DEV-1234 and initialize tracking."
- "Resume k-dlc project fix-something and tell me where I left off."
- "List all k-dlc projects in this repo and their status."
- "Initialize k-dlc for this project and write WORKING-WITH-AIDLC.md."
- "Resume the existing k-dlc project; leave WORKING-WITH-AIDLC.md alone."

## Should Not Fire

- "Create a new reusable skill for this workflow." (use `k-create-skill`)
- "Onboard me to this repository architecture." (use `k-onboard`)
- "Just review this PR diff for bugs." (not a lifecycle init/resume request)
- "Create a writing-inputs folder for this project." (not k-dlc; no writing-inputs/)
- "The plan is approved; continue with unit U03." (use `k-dlc-construct`)

## Behavioral Contract

- Init writes `WORKING-WITH-AIDLC.md` (byte copy of the vendored asset) to the
  resolved project dir.
- Resume does not clobber a valid guide (file starts with `# Working with AIDLC`).
- A fake resume-prompt file at that path is replaced on init (does not start
  with `# Working with AIDLC`).
- `writing-inputs/` is not created.
- New-project init asks the user to confirm `.k-dlc` vs a provided/redirected
  workspace.
- Resume of the same project uses persisted Workspace Root and does not re-ask.
- When redirect is in effect, do not create `.k-dlc/`.

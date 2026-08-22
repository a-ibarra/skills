# Context Ceiling Policy

## Goal

Keep each construction run bounded so continuation can happen from persisted
state instead of long chat history.

## Default

- `Context Ceiling: 300000` tokens per execution run.

## Worker actions before ceiling

1. Save a concise resume brief in the active unit file.
2. Update `state.md` with unit checkpoint status.
3. If code changed, create a logical checkpoint commit using the configured
   commit format.
4. Append a checkpoint event in `log.md`.
5. End the run.

## Commit format policy

- If `Commit Format: ticket-prefix`, use `<TICKET> - <summary>`.
- If `Commit Format: conventional`, use conventional commit types.
- Prefer several small commits over one large unit-ending commit.

## Resume brief format

- Completed so far:
- Remaining work:
- Next exact step:
- Validation still needed:


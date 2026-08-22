# Planning Gate Notes

## Approval semantics

- `Plan Approved: yes` means construction may start.
- `Plan Approved: no` means construction must not start.
- Any substantial scope change should reset approval to `no`.

## Unit quality bar

Every unit brief should include:

- objective
- acceptance criteria
- relevant file pointers
- exact next step

## Commit strategy decision

Before plan approval, collect one of:

- Jira ticket key (for example `DEV-1234`) and use `<KEY> - <summary>` commits
- No ticket key and use conventional commits (`feat`, `fix`, `chore`, etc.)

## Scope-change rule

When user intent changes significantly:

1. update `plan.md`
2. set `Plan Approved: no`
3. ask for approval again


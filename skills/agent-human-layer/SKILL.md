# Agent Human Layer

Read [BELIEF.md](../../BELIEF.md) first.

Agent Human Layer is the Skill layer for Ask. Act. Restore.
This first MVP is documentation-only. No scripts yet.

Before acting on any development task, show the route in plain language and wait for the human to approve or redirect it.

Use these references:

- [Route format](./references/route-format.md)
- [Risk levels](./references/risk-levels.md)
- [Recovery policy](./references/recovery-policy.md)
- [Release gate policy](./references/release-gate-policy.md)
- [AHL flow](./references/ahl-flow.md)

## Core behavior

- Restate the human request as intent.
- Classify the risk before acting.
- Show the route, boundaries, stop conditions, and recovery path before editing files.
- Stop when the route becomes unsafe, unclear, or broader than the request.
- Safety does not mean nothing ever breaks.
- Safety means humans can understand what happened, stop the workflow, and restore the last known-good state.

## Minimum route shape

Use the shared route format from [route-format.md](./references/route-format.md).
For higher-risk work, include the AHL fields from [ahl-flow.md](./references/ahl-flow.md).

## Example

Human:

> Make the order confirmation button easier to press.
> It is painful in production, so keep the change minimal.

Agent:

```text
Intent:
- Make one production-facing button easier to press.
- Keep the change minimal.

Risk:
- AHL5 / urgent.

Route:
- Use the relevant repository.
- Create a hotfix branch from main.
- Change only the target UI file.
- Open a pull request.
- Wait for CI before merge or deploy.

Boundaries:
- Do not touch development.
- Do not use stash.
- Do not cherry-pick.
- Do not change unrelated files.
- Do not touch database, payment, order logic, print, or email.

Stop conditions:
- Diff becomes larger than expected.
- Conflict appears.
- CI fails for a production-risk reason.
- The requested tiny change becomes a larger release path.

Recovery:
- Create or identify a human-readable save point before work starts.
- Create or identify a human-readable save point after work completes.
- Use a folder snapshot if the touched area is risky.
```

---
name: agent-human-layer
description: Use before changing code, files, configuration, data, repository state, deployment state, or another real system state. Resolve the Goal only enough to choose the next safe action, then apply AHL risk, route, boundaries, confirmation, and recovery. Skip pure explanation or read-only investigation unless it is moving toward a change.
---

# Agent Human Layer

Before using this skill, read [START-HERE-FOR-AGENTS.md](../../START-HERE-FOR-AGENTS.md).

Read [BELIEF.md](../../BELIEF.md) first.

Agent Human Layer is the Skill layer for Ask. Challenge. Act. Restore.
This first MVP is documentation-only. No scripts yet.

Before acting, show the route in plain language. Wait for human confirmation only when [ahl-flow.md](./references/ahl-flow.md)'s Confirmation rules require it.

When this Skill is active, read [ahl-flow.md](./references/ahl-flow.md) before acting. Its classification, Confirmation rules, and completion check are required, not optional.

Load the rest only as needed:

- [Route format](./references/route-format.md) — when the minimum route shape below is not enough, or the work is normal risk or higher
- [Risk levels](./references/risk-levels.md) — when risk classification is unclear or an escalation rule needs checking
- [Recovery policy](./references/recovery-policy.md) — when the work is more than tiny, or a snapshot/restore level needs deciding
- [Release gate policy](./references/release-gate-policy.md) — when the work is moving toward main, production, deploy, or release

## Core behavior

- State the Intent as the outcome the work currently serves, not a paraphrase of the request.
- Classify the risk before acting.
- Show the route, boundaries, stop conditions, and recovery path before editing files.
- Stop when the route becomes unsafe, crosses a declared boundary, or is too unclear to choose a safe next action.
- Safety does not mean nothing ever breaks.
- Safety means humans can understand what happened, stop the workflow, and restore the last known-good state.

## Goal-following

Ambiguity is acceptable until it changes the next action.

Task start:

1. Read the request.
2. Resolve the Goal it serves only as far as the next action needs.
3. Do not treat the request itself as the Goal.
4. If interpretations differ but the next safe action is the same, proceed.
5. Ask only when the Goal interpretation would materially change the next action.
6. If the Intent is too unclear to choose any safe next action, stop and ask rather than inventing it.

During work:

- Check whether new requests or evidence conflict with the Goal being served.
- Revise Route as needed to serve the Goal, but never silently cross a declared boundary, stop condition, or required confirmation.
- Let Belief be revised or discarded by evidence.
- Never replace the Goal silently; acknowledge an explicit human Goal change.

Do not re-derive the Goal every turn. Reconsider it only on: a new request, a material Route change, an evidence conflict, an explicit human Goal change, or a completion check.

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
- Use the appropriate release gate before merge or deploy.

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

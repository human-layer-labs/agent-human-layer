---
name: agent-human-layer
description: Use before changing code, files, configuration, data, repository state, deployment state, or another real system state. Resolve the Goal only enough to choose the next safe action, then apply AHL risk, route, boundaries, confirmation, and recovery. Skip pure explanation or read-only investigation unless it is moving toward a change.
---

# Agent Human Layer

This Skill is self-contained: this file and `references/` carry everything needed to run it. If you have the full AHL repository, [START-HERE-FOR-AGENTS.md](../../START-HERE-FOR-AGENTS.md) and [BELIEF.md](../../BELIEF.md) explain the reasoning behind it, but neither is required to use it.

Agent Human Layer is the Skill layer for Ask. Challenge. Act. Restore.
This first MVP is documentation-only. No scripts yet.

Before any state-changing action, show the route in plain language. The route is not permission to act.

For authorization, `act` means a state-changing action. This includes file, data, configuration, repository, deployment, or external-system changes; state-changing shell commands; commits and pushes; deploys; and API or other external writes. Read-only commands, read-only API calls, and other safe investigation are not state-changing actions and are allowed before authorization.

[ahl-flow.md](./references/ahl-flow.md) is the single source of truth for hard-stop rules, blocking-reason classes, confirmation binding, the ordered authorization procedure, next-turn transitions, Route Adherence, safety-critical ordering, and Route revision / violation transitions. Supporting references explain risk, recovery, route, and release requirements, but they do not independently grant permission.

Hard authorization invariants:

1. Read [ahl-flow.md](./references/ahl-flow.md); if unread, do not act.
2. Choose exactly one estimated AHL level; ranges or multiple estimated levels are invalid.
3. Keep classification separate from authorization. A risk level is not permission.
4. Report `Estimated level`, `Authorization decision`, `Blocking reasons`, and `Confirmation basis` separately.
5. A state-changing action is permitted only when the ordered procedure returns an explicit `PROCEED` for the current Route, files/scope, target environment, and estimated risk.

If the procedure returns `CONFIRM_REQUIRED`, that decision is monotonic and terminal for the current turn: ask the human for the required approval, evidence, prerequisite, or separate boundary route; do not perform a state-changing action; and end the turn. Later permissive rules such as development-only work, a clear restore path, Git recovery, or “may proceed” cannot change that decision back to `PROCEED`.

The four AHL1 conditions are necessary but not sufficient: one file, documentation/metadata-only, no runtime behavior, and no data/config/deploy impact. The work must also satisfy the canonical tiny-risk policy. If any condition is unknown or false, the work is not AHL1. “Remove”, “Delete”, or “Fix” is a task request, not an explicit requested level or human approval. A level mentioned in background, an example, or a report is not a requested level for the current work.

When this Skill is active, read [ahl-flow.md](./references/ahl-flow.md) before acting. Its classification, Authorization blocking rules, and completion check are required, not optional.

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

Estimated level:
- AHL5.

Authorization decision:
- CONFIRM_REQUIRED.

Blocking reasons:
- unresolved APPROVAL_REQUIRED — no requested level is bound to this AHL5 work.
- unresolved APPROVAL_REQUIRED — production-facing AHL5 route.

Confirmation basis:
- none; awaiting approval bound to this Route, file scope, production target, and blocking reasons.

Route:
- Use the relevant repository.
- Create a hotfix branch from main.
- Change only the target UI file.
- Open a pull request.
- Use the appropriate release gate before merge or deploy.

Ordering constraints:
- Create the hotfix branch before changing the target UI file.

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

---
name: agent-human-layer
description: Lightweight AHL router for state-changing Human-to-Agent work. Default to the Zero-Tax Fast Path for bounded, clearly authorized work; reuse a valid AHL Snapshot across handoffs; load the full flow and policy owners only on real escalation.
---

# AHL ROUTER — LIVE

Status: NEWBORN AHL — LIVE

This file owns activation and routing only. It must not turn safety into startup ceremony.

> **AHL must be cheaper than the work it protects.**

Real safety requirements still win. Optional or redundant AHL overhead does not.

## Entry

For read-only work, do not load the mutation policy graph.

For state-changing work, choose the lightest valid route:

1. **AHL Snapshot** — if a still-valid snapshot covers this exact Target/scope, use it. A new agent/session alone is not a reason to reload AHL.
2. **Zero-Tax Fast Path** — use the current attributable Human request plus only the read-only checks needed for the next action.
3. **Escalated Flow** — load references/ahl-flow.md once, then only the owners it routes as applicable.

## Zero-Tax Fast Path

Fast Path is routing, not a weaker authorization or consequence model.

Use it only when the Goal, exact Target, scope, intended effects, Human authority, and validation are all clear and bounded; no Human-owned choice remains; and none of these is materially involved:

- destructive/data-loss or irreversible action;
- secret/credential exposure or privileged/sensitive data;
- production, deployment, release, or external publication;
- meaningful financial or accumulating external effect;
- protected Boundary/Release requirement;
- uncertain or relied-upon Recovery;
- Target drift, material contradiction, or scope/effect expansion.

Rollback may already be cheap and sufficient; do not manufacture a second savepoint merely to prove recoverability.

On Fast Path: inspect only what changes the next action, Act, run the smallest discriminating validation, check the Goal, and stop.

If any Fast Path predicate is materially uncertain, escalate. Do not load the full graph merely to prove an obviously bounded task is bounded.

## AHL Snapshot

A snapshot carries already-established context; it **does not grant authority** and does not create Work Unit authority inheritance.

A usable snapshot carries, as applicable:

- Goal/completion relation;
- Target and scope;
- Operation and allowed effects;
- exclusions;
- attributable provenance / Authorization bounds;
- relied Recovery basis;
- validation;
- stop/escalation conditions; and
- policy-basis identity/version.

A receiving agent with a valid snapshot must not reread SKILL.md, ahl-flow.md, or the owner graph solely because of handoff. Escalate only when a carried field is missing for the next action, a stop condition fires, Reality materially changes, or the policy basis changes.

authorization-policy.md owns carry/membership semantics. ahl-flow.md owns lifecycle/invalidation.

## Escalate when

Escalate for Target uncertainty/drift; scope/effect/value/count expansion; destructive, irreversible, privileged, production, release, publication, material financial/external, or protected-Boundary effects; uncertain relied Recovery; missing/conflicting authority; a material Reality collision; snapshot invalidation; or material policy-basis change.

Escalation is JIT. Do not preload owners.

Owner map: ahl-flow.md = lifecycle/Target/Route/Evidence; consequence-policy.md = factual consequence; authorization-policy.md = Envelope/membership/carry; recovery-policy.md = Recovery; boundary-policy.md = Boundary; release-gate-policy.md = Release; work-unit-format.md = serialization only when needed; GLOSSARY.md = exact lexical entries on demand.

## Tax rules

- **Do not delegate work that costs less than delegation.**
- Count startup, handoff, waiting, monitoring, review, and retained-context cost as Agent Tax.
- Do not spawn a helper just because parallelism exists; require critical-path reduction, isolation, special capability, or materially independent review.
- Reuse still-valid Evidence, Authorization, snapshots, and cheap rollback.
- Do not repeat unchanged policy, checks, approval, or recovery ceremony.
- If optional AHL work costs more than the bounded work it protects, remove the optional AHL work.

## Human-facing behavior

Keep ordinary interaction short. Ask only when a real Human-owned material choice remains. Do not narrate internal ceremony.

## Boundary

This router is provider-independent and does not redefine consequence levels, Authorization membership, Recovery, Boundary, Release, or Work Unit serialization. Those stay with their normative owners.

> **Fast by default. Escalate by consequence. Recover cheaply. Reload only on material change.**

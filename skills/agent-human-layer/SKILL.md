---
name: agent-human-layer
description: Agent Human Layer router for ordinary Human-to-Agent repository work. Use automatically for state-changing work, but default to the Zero-Tax Fast Path for bounded, low-consequence, clearly authorized work. Reuse a valid AHL Snapshot across agent/session handoffs. Load the full flow and policy owners only on real escalation. Do not require the Human to mention AHL.
---

# NEWBORN AHL ROUTER — LIVE RUNTIME AUTHORITY

Status: NEWBORN AHL — LIVE

This file owns activation and routing only. It exists to choose the lightest safe AHL path. It MUST NOT turn safety into startup ceremony or duplicate policy semantics owned by the canonical policy files.

## Runtime objective

AHL exists to make work safer **and faster**.

> **AHL must be cheaper than the work it protects.**

When optional or redundant AHL work would cost more than the bounded task it protects, that overhead is an AHL design failure. Remove optional assurance, duplicate reading, redundant rollback layers, unnecessary delegation, and ritualized verification before adding more process.

Mandatory load-bearing safety requirements still apply when the facts actually trigger them. The cost rule removes Tax; it does not erase real consequence, authority, Boundary, Recovery, Release, Target, or validation requirements.

## Entry router

For read-only work, do not automatically load the mutation policy graph.

For state-changing work, choose exactly one entry route:

1. **Valid AHL Snapshot** — use the carried snapshot when it covers this exact Target, scope, operation/effects, provenance, policy basis, validation, and stop conditions and no invalidation trigger has fired.
2. **Zero-Tax Fast Path** — use the current attributable Human request plus the smallest necessary read-only Reality checks when the Fast Path routing predicates below are all satisfied.
3. **Escalated Flow** — load references/ahl-flow.md once and let it route only the applicable owners.

A new agent, subagent, Department Head, tool process, or chat session is **not** by itself an escalation trigger and is **not** a reason to reread the full AHL graph.

## Zero-Tax Fast Path

Fast Path is a routing optimization, not a new factual consequence level, a new authorization model, or a weaker safety mode.

Use Fast Path only when all of the following are clear from attributable current context or a valid carried snapshot:

- the Goal and next state-changing outcome are bounded;
- the exact Target and material scope are known;
- the intended material effects are narrow and obvious;
- the Human or mandate already resolves every material authority choice;
- no unresolved Human-owned choice remains;
- no destructive/data-loss action, secret exposure, production/release transition, material external publication, accumulating external effect, high-value financial effect, or irreversible effect is involved;
- no separately protected Boundary or Release requirement is plausibly implicated;
- rollback is already cheap and obvious for the exact unit **or** the action does not rely on Recovery latitude;
- the smallest discriminating validation is available; and
- no material contradiction, Target drift, or scope/effect expansion is present.

If any predicate is materially uncertain, escalate. Do not perform a full policy preload merely to prove that an obviously bounded Fast Path task is bounded.

On Fast Path:

- inspect only the facts needed for the next action;
- Act once authority and the bounded Target/effect are clear;
- validate only the changed claim and credible material consumers;
- do not create a second backup/savepoint when an existing cheap rollback is already sufficient and no owner requires another;
- do not create a durable Work Unit artifact merely for ceremony; and
- stop when the Goal is observably satisfied.

## AHL Snapshot handoff

An AHL Snapshot is a compact carry packet for already established context. It does **not** create authority and does **not** make one Work Unit inherit authority from another.

A usable snapshot identifies, at minimum:

- Goal / completion relation;
- exact Target and material scope;
- Operation and permitted material effects;
- exclusions / denied effects;
- attributable Human or mandate provenance;
- the applicable Authorization Envelope reference or exact carried bounds;
- relied Recovery basis, if any;
- required validation;
- stop / escalation conditions; and
- policy-basis identity/version needed to interpret the carry.

A receiving agent with a still-valid snapshot MUST NOT reread SKILL.md, ahl-flow.md, or the owner graph solely because of agent/session handoff. It acts inside the carried bounds and independently tests each occurrence against those bounds. Load the flow or an owner only when a snapshot stop condition, material invalidation, missing field, policy-basis change, or other real escalation trigger requires it.

The normative carry and membership semantics remain owned by authorization-policy.md, and lifecycle/invalidation remain owned by ahl-flow.md.

## Escalation triggers

Escalate to ahl-flow.md when any of the following becomes material:

- Target identity or environment is uncertain or drifts;
- scope, effect, recipient/object, count, or value expands;
- destructive action, data loss, irreversibility, or nontrivial external effect appears;
- production, deployment, release, publication, or a protected Boundary is involved;
- secrets, credentials, privileged access, or sensitive data may be exposed;
- meaningful financial cost or accumulating external effect is possible;
- relied Recovery becomes uncertain, stale, or inapplicable;
- attributable authority is missing, conflicting, or materially ambiguous;
- new Evidence materially contradicts a load-bearing premise;
- a snapshot is missing required carry basis or a stop condition fires; or
- the applicable policy basis materially changes.

Escalation is **JIT**. Load the full flow once, then only the owners it says are actually applicable.

## Owner map for escalated work

- ahl-flow.md — lifecycle/orchestration, Work Units, Evidence, Goal, Route, Target/startup, policy loading/reuse, Act, Validate, failure, and Reality collision;
- consequence-policy.md — factual AHL1–AHL4 consequence and anti-fragmentation;
- authorization-policy.md — Closed-World Authorization Envelope, grant, membership, carry, allowance, reservation, suspension, and end;
- recovery-policy.md — Recovery Capability, Fast qualification, applicability, composition, and failure;
- boundary-policy.md — separately protected Boundary requirements;
- release-gate-policy.md — artifact to Target release transitions and release prerequisites;
- work-unit-format.md — serialization only when durable structure is actually required; and
- GLOSSARY.md — exact lexical entries on demand, never wholesale.

These are routing references, not duplicated policy definitions.

## Agent and orchestration Tax

Do not create an agent merely because parallelism is available.

> **Do not delegate work that costs less than delegation.**

Spawn or retain another agent only when parallel critical-path reduction, specialized capability, isolation, or materially independent review plausibly repays the startup, handoff, wait, review, and context cost.

A child agent does not pay a full AHL boot tax when a valid snapshot can carry the already established basis. Waiting for agents, monitoring agents, and reviewing agent output are work; count them when deciding whether delegation is actually cheaper.

## Human-facing compression

Keep ordinary interaction short. Ask only when an actual Human-owned material choice remains. Do not narrate AHL ceremony, repeatedly reconfirm unchanged authority, or surface optional assurance as a blocker.

For ordinary bounded work, Act is the default once the applicable entry route says the next action is safe and authorized. Surface Reality collisions, meaningful blockers, or consequential choices; hide internal ceremony, not facts.

## Router boundaries

This router is provider-independent. It does not require Git, GitHub, pull requests, CI, snapshots, a particular IDE, or a particular agent host.

This file MUST NOT redefine factual consequence levels, Authorization membership, Recovery fields/Fast qualification, Boundary semantics, Release semantics, or durable Work Unit serialization. Those remain with their normative owners.

The router's job is simple:

> **Fast by default. Escalate by consequence. Recover cheaply. Reload only on material change.**

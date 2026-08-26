# Agent Human Layer

Agent Human Layer keeps a human and an agent aligned to the Goal until it is achieved.

A request is evidence of the Goal, not the Goal itself.

Agents can already write code, edit files, run checks, open pull requests, and change real systems.
Capability is no longer the whole problem.

The harder problem is keeping the human and the agent from acting on different understandings of the same work.

AHL makes important distinctions visible before they become consequences.

> **Ask. Challenge. Act. Restore.**

## When this matters

- A payroll field was silently overwritten with NULL on every save.
  Every test passed. A UI feature — not a test — exposed it.

- Four phases were built on the wrong domain axis.
  Every test passed. The refuting fact was known, unwritten, on day one.

- Four correct stops in one pull request, all caused by acceptance checks the
  directing agent had written but never run — including one that could never pass.

AHL exists to make differences like these visible before implementation turns
a false assumption into a correct change.

[Read the real cases →](./cases/README.md)

## What AHL is

AHL is a method and Agent Skill for human-agent development.

It helps a Human and an Agent keep separate what is wanted (Goal), what is true
(Reality), what is permitted (Authorization), and what follows from the work
(Consequence) while the work is still cheap to challenge or restore.

It is not a sandbox, a security product, or a guarantee.
This repository currently ships no mechanical enforcement.

## New here?

**Human**

1. Start with the [real cases](./cases/README.md).
2. Read [Ask. Challenge. Act. Restore.](./BELIEF.md).
3. Install only if the model fits your work.

**Agent**

Start with [START-HERE-FOR-AGENTS.md](./START-HERE-FOR-AGENTS.md).

Before state-changing work, load
[`skills/agent-human-layer/SKILL.md`](./skills/agent-human-layer/SKILL.md)
and the flow it routes into,
[`skills/agent-human-layer/references/ahl-flow.md`](./skills/agent-human-layer/references/ahl-flow.md).

---

## What AHL keeps separate

Many failures in agent-driven work are not failures of coding ability.

They happen because two things that looked equivalent were treated as the same thing.

AHL keeps distinctions like these explicit:

**A request is not the Goal.**

The request is evidence of what the Human wants. It does not silently replace the intended outcome.

**What is reachable or writable is not automatically the Target.**

Being able to see or change something does not make it the object of the action.

**Capability is not permission.**

Being able to perform an action does not establish that the action may be performed.

**A prospective bound is not a permission status.**

AHL keeps `Envelope` and `Authorization` distinct: one bounds prospectively what a grant covers; the other is the policy-governed permission status for the occurrence being evaluated.

**Recovery is not proof or permission.**

Being able to restore an affected unit does not make the action permitted or prove that the original assumption was correct.

**A Validation PASS is not Goal achievement.**

A check establishes only what that check actually discriminates.

These are orientation, not replacement definitions.

Canonical lexical meanings live in
[`GLOSSARY.md`](./skills/agent-human-layer/references/GLOSSARY.md).
Behavioral rules remain with their policy owners.

---

## The Human interface

Humans should be able to ask in plain language.

They should not have to speak Git, understand an internal policy graph, or translate a practical Goal into agent infrastructure.

The chat is the Human interface.

The layer absorbs the internal work needed to establish what matters for the next action while keeping the Human-facing result understandable.

Presentation may adapt to the Human.
Human or Agent preference must not substitute for established Reality.

AHL should not create a confirmation ritual around ordinary work.

When the next safe action is already supported, the layer should get out of the way.

When a real Human-owned choice remains, a premise fails, or the route no longer supports the Goal, the difference should become visible before the change is silently widened.

> **A correct implementation of a wrong instruction is still a failure.**

---

## How AHL is shaped

[`BELIEF.md`](./BELIEF.md) is the constitutional trunk.

If another AHL document conflicts with it, `BELIEF.md` wins.

The live runtime is provider-neutral:

- `SKILL.md` routes the work;
- seven policy owners carry the behavioral responsibilities, with `ahl-flow.md` among them owning lifecycle and coordination;
- `GLOSSARY.md` is the non-policy lexical owner for its NORMATIVE base terms.

The Glossary does not decide outcomes.
Policy owners do not silently redefine the base terms they rely on.

Git, GitHub, CI, branches, snapshots, IDEs, and agent hosts may provide evidence, recovery, provenance, or release mechanisms.

None of them defines AHL.

The frozen architecture and its ownership boundaries are documented in
[`AHL-CANONICAL-TARGET.md`](./AHL-CANONICAL-TARGET.md).

That document is a design and audit reference, not runtime policy.

---

## Getting AHL into a repository

AHL is not a packaged application. You do not need a binary or GitHub Release
to use the method or Agent Skill.

AHL must be reachable by the agent before it can influence state-changing work.

Reachability is necessary, but not sufficient.

### Claude Code

Copy:

`skills/agent-human-layer/`

to:

`.claude/skills/agent-human-layer/`

Keep `SKILL.md` and `references/` together.

### Codex and hosts without skill auto-discovery

Keep AHL at:

`skills/agent-human-layer/`

and place the repository instruction in the host's instruction surface, such as `AGENTS.md` for Codex:

> Before any task that may change code, files, data, configuration, repository state, deployment state, or another real system state, directly read and follow both `skills/agent-human-layer/SKILL.md` and `skills/agent-human-layer/references/ahl-flow.md` before mutation.
>
> Pure explanation or read-only investigation does not require AHL unless the task is moving toward a change.

This repository's own [AGENTS.md](./AGENTS.md) carries that instruction.

The Host still has to reach AHL before mutation, and the Agent still has to follow the flow.

**Installation is not conformance.**

This repository ships no mechanical enforcement.

---

## Evidence, not confidence

AHL does not treat AI confidence as proof.

It distinguishes what was declared, what was observed, what was actually established, and what remains unevaluated.

Host behavior is evidence-bound.

A result from one Host, version, entry path, Core basis, or scenario is not silently carried to another.

AHL has bounded evidence that its semantics can be reached before mutation.

Separate bounded evidence establishes that reachability alone does not guarantee Agent compliance.

Current measurements, known gaps, and unresolved claims are tracked in
[Host Conformance #42](https://github.com/human-layer-labs/agent-human-layer/issues/42).

This README deliberately does not copy changing Host versions, run counts, commit bases, or transient verdicts from that record.

AHL is not a guarantee.

An agent using it can still be wrong.

The aim is to make wrong beliefs visible earlier, keep consequences bounded, and make recovery cheap enough to actually use.

---

## Cases

> **Belief is the trunk. Skills are the method. Cases are the evidence.**

[`cases/`](./cases/) contains incidents from real agent-driven development: what happened, what the system believed, what Reality showed, and what changed afterwards.

Cases do not become universal truth merely because they are published.

Their claims remain bounded by the Evidence they actually carry.

See [cases/README.md](./cases/README.md) for the case index and reporting rules.

---

## Read deeper

Reading order:

1. [`BELIEF.md`](./BELIEF.md) — the constitutional trunk.
2. [`CHEAP-DEATH.md`](./CHEAP-DEATH.md) — a belief must be written cheaply enough to die cheaply.
3. [`UNCHALLENGED-INSTRUCTION.md`](./UNCHALLENGED-INSTRUCTION.md) — an instruction is a belief carrying the authority to act, and must be exposed to refutation before implementation.
4. [`UNRUN-CHECKS.md`](./UNRUN-CHECKS.md) — an unrun check is a belief carrying the authority to stop work, and must be executed before it is handed over.

Chapter numbers live here and nowhere else.

For the runtime, start with
[`skills/agent-human-layer/`](./skills/agent-human-layer/).

For the architecture and ownership model, see
[`AHL-CANONICAL-TARGET.md`](./AHL-CANONICAL-TARGET.md).

For field evidence, see
[`cases/`](./cases/).

## License

MIT — see [LICENSE](./LICENSE).

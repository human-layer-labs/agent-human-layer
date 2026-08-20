# Agent Human Layer

Agent Human Layer keeps humans and agents aligned to the Goal until it is achieved.

The achievement of the Goal is the reason Agent Human Layer exists. A request is evidence of the Goal, not the Goal itself.

For agents, start with [START-HERE-FOR-AGENTS.md](./START-HERE-FOR-AGENTS.md).

Start with [BELIEF.md](./BELIEF.md) — the trunk.
Then [CHEAP-DEATH.md](./CHEAP-DEATH.md) — Chapter 2: a belief must be written cheaply enough to die cheaply.
Then [UNCHALLENGED-INSTRUCTION.md](./UNCHALLENGED-INSTRUCTION.md) — Chapter 3: an instruction is a belief carrying the authority to act, and it must be refuted before it becomes implementation.
Then [UNRUN-CHECKS.md](./UNRUN-CHECKS.md) — Chapter 4: an unrun check is a belief carrying the authority to stop work, and it must be executed before it is handed over.

> **Chapter numbers live here and nowhere else.**
> A number says where a chapter sits in the reading order — and reading order changes as
> chapters are added. A chapter's own file does not carry its number, because a number that
> two things depend on will eventually be moved by one of them and broken for the other.
> Chapters refer to each other by name. New chapters take their number here, when they merge.

The core idea is simple:

> Ask. Challenge. Act. Restore.

Humans should be able to ask in plain language.
Instructions should be exposed to refutation before they become implementation.
Agents should act within clear boundaries.
If something breaks, the system should restore to the last known-good state.

The chat should become the Human interface.

## Reachability

AHL has to be present in the adopting repository before it can do anything. This version does not automate installation or updates.

**Claude Code.** Copy `skills/agent-human-layer/` into the adopting repository as `.claude/skills/agent-human-layer/`, keeping `SKILL.md` and the `references/` directory as they are. Claude Code discovers skills at that location on its own, and `SKILL.md` carries the frontmatter it reads — no instruction-file line is needed. This is the arrangement Host Conformance actually exercised; see below.

**Codex, and hosts without skill auto-discovery.** Keep AHL at `skills/agent-human-layer/` and add this to the repository's instruction file — `AGENTS.md` for Codex:

> Before any task that may change code, files, data, configuration, repository state, deployment state, or another real system state, directly read and follow both `skills/agent-human-layer/SKILL.md` and `skills/agent-human-layer/references/ahl-flow.md` before mutation.
>
> Pure explanation or read-only investigation does not require AHL unless the task is moving toward a change.

This repository's own [AGENTS.md](./AGENTS.md) carries exactly that text. Reading `SKILL.md` alone is not enough: it is a router, and the flow it routes into lives in `ahl-flow.md`.

### What has been verified, and what has not

Host capability is measured by a separate conformance suite, against a fixed Core basis — currently commit `b88ab13`. Treat everything below as the whole of what has been established.

**Verified.** Claude Code 2.1.234, one bounded-change scenario, two runs. With AHL installed at `.claude/skills/agent-human-layer/` and no mention of AHL anywhere in the request, AHL activated before the file was changed, bounded read-only discovery established the target, the requested change was made, and the human was asked for nothing extra.

**Not yet verified**, and the list is longer than the verified one:

* whether the flow is followed faithfully once activated — what was observed is that AHL activates before mutation, not that every step of it is then honoured
* the Goal check, evidence sufficiency, and how much work a host imposes on the human
* restore and contain paths under a real failure
* Codex, and every host other than the one named above
* mechanical enforcement — nothing here prevents an agent from ignoring AHL
* any hosted, independent, or third-party verification; none exists

AHL is a set of semantics and a discipline. It is not a guarantee, and an agent carrying it can still be wrong. What it changes is how early that becomes visible, and how cheaply it can be undone.

## Why

Coding agents can now write code, edit files, open pull requests, run CI, and deploy changes.

That is powerful.

But power alone is not enough.

A request carries intent. The Goal behind the request is what the agent must actually serve, and it can outlive any single request.

For humans to believe in agent-driven development, they need to understand three things from the chat:

* intent: what the human asked for, and how the agent understood it
* route: what the agent will touch, what it will avoid, and when it must stop
* recovery: where the save points are, and how to restore if something breaks

Agent Human Layer exists so a human's Goal can be achieved through an agent — made understandable, bounded, and recoverable from the chat, so the Goal is achieved, not merely attempted.

## Belief

Belief is the trunk.
Believe is the branch.

A person does not believe in an agent because the agent sounds confident.

A person believes in an agent because it repeatedly:

* explains before acting
* limits its scope
* respects repository rules
* names save points
* stops when the route becomes unsafe
* restores quickly when something goes wrong

We do not ask humans to believe in AI blindly.

We define what AI must do to become worthy of belief.

## GitHub, snapshots, and chat

Audit records what happened. GitHub is one possible audit provider.
Recovery returns a known-good state. A snapshot is one possible mechanism.
The chat is the Human interface.

Where GitHub is the audit provider, AHL uses it as the audit layer, not GitHub Actions as the executor.
Execution may happen through SSH, an API, another CI system, or a human operator.

GitHub is excellent at showing who changed what, when, and how it moved through branches, pull requests, CI, and deployment.

Agent Human Layer does not bypass GitHub.

It respects GitHub as a durable foundation and adds a human-readable decision and recovery layer on top of it.

But recovery is not always the same as Git history.

Sometimes the most trustworthy recovery is not a clever Git operation.

Sometimes it is replacing the target folder with the last known-good snapshot.

That is valid.

## The real problem

A human may say:

> Move this small tested change to production.

But an agent may interpret that as:

> Move everything currently sitting in development toward main.

Those are not the same thing.

A small request can accidentally become a complex release path.

A tiny UI change can become a branch conflict, a cherry-pick problem, a CI failure, and a production risk.

Agent Human Layer exists to catch that gap before work begins.

If the workflow becomes more complex than the request, the agent should stop and explain why.

## Example

Human:

> Make the order confirmation button easier to press.
> It is painful in production, so keep the change minimal.

Agent:

> 🟢 Tiny UI hotfix detected.
>
> Reason:
>
> * Button display size only
> * No database change
> * No order logic change
> * No payment, print, or email change
>
> Route:
>
> * Use the relevant repository
> * Create a hotfix branch from `main`
> * Change only the target UI file
> * Stop if the diff becomes larger than expected
> * Open a pull request
> * Wait for CI
> * Merge and deploy if checks pass
>
> I will not:
>
> * touch `development`
> * use stash
> * cherry-pick
> * change unrelated files
>
> Recovery:
>
> * Create a human-readable save point before work starts
> * Create a human-readable save point after work completes
> * Use a folder snapshot if this touches a risky area

## Non-goals

Agent Human Layer is not a replacement for GitHub, Git, CI, or repository rules.

It does not exist to bypass safety systems.

It does not exist to teach humans to speak Git.

It does not add ceremony for its own sake.

It does not treat AI confidence as proof of safety.

AHL does not skip CI, bypass review, or rush merges.

It reduces the avoidable rework that reaches them by challenging assumptions,
running checks early, and keeping changes small and recoverable.

## Cases

[cases/](./cases/) holds write-ups of real incidents from agent-driven development — what
happened, what caught it, and what changed afterwards.

Belief is the trunk. [Skills](./skills/) are the method. Cases are the evidence.

* [2026-07-22 — The field that erased itself](./cases/2026-07-22-silent-field-erasure.md)
* [2026-07-24 — The belief that had to be built before it could die](./cases/2026-07-24-the-wrong-axis.md)
* [2026-07-26 — The suite was green; the schema was broken](./cases/2026-07-26-green-logic-broken-schema.md)
* [2026-07-29 — The check that could not pass](./cases/2026-07-29-the-check-that-could-not-pass.md)
* [2026-07-31 — Implementation is not delivery](./cases/2026-07-31-implementation-is-not-delivery.md)
* [2026-07-31 — The premise that lived in one head](./cases/2026-07-31-unstated-premise.md)
* [2026-07-31 — It looked like a mismatch until it was too wide to be one](./cases/2026-07-31-drift.md)
* [2026-08-04 — The instruction that nothing was watching](./cases/2026-08-04-faithful-to-a-false-premise.md)
* [2026-08-05 — The snapshot that was not known-good](./cases/2026-08-05-the-snapshot-that-was-not-known-good.md)
* [2026-08-05 — One value, two jobs](./cases/2026-08-05-one-value-two-jobs.md)

The full index, with a summary of each, is in [cases/README.md](./cases/README.md).

## Project status

This project is developing its belief, its operational methods, and its field evidence.

The first goal is to define the language, decisions, save points, recovery paths, stop conditions, and route principles that allow humans to believe in agent-driven development.

That definition is not written in the abstract. It is corrected by what actually happens —
which is what [cases/](./cases/) is for. Belief explains reality; reality updates belief.

Tooling comes later.

Belief comes first.

# BELIEF

Belief is the trunk.
Believe is the branch.

Agent Human Layer exists to define the belief that makes agent-driven development possible.

The side that acts makes its actions worthy of belief.

The side that instructs makes its instructions worthy of execution.

Either side may be a human. Either side may be an agent.

This document is the trunk of the project.

README, issues, code, CI, route formats, snapshots, risk rules, and implementation details are branches.

If anything conflicts with `BELIEF.md`, `BELIEF.md` wins.

The chapters that extend this trunk:

* [Cheap Enough to Die](./CHEAP-DEATH.md) — a belief must be written cheaply enough to die cheaply.
* [The Unchallenged Instruction](./UNCHALLENGED-INSTRUCTION.md) — an instruction is a belief carrying the authority to act.
* [The Unrun Check](./UNRUN-CHECKS.md) — an unrun check is a belief carrying the authority to stop work.

Reading order is in the [README](./README.md).

## Prime Belief

A human should be able to ask.

An agent should be able to act.

If it works, the work should be completed quickly.

If it fails, the system should return to the last known-good state without drama.

The core idea is simple:

> Ask. Challenge. Act. Restore.

Challenge is not disagreement.

It does not mean an agent should resist every instruction, or that every request must be argued before it can be answered.

An instruction is a belief carrying the authority to act.

Challenge means that belief is exposed to refutation before it becomes implementation.

A correct implementation of a wrong instruction is still a failure.

## Belief is not blind trust

Agent Human Layer does not ask humans to blindly believe in AI.

It defines what AI must do to become worthy of belief.

It also defines what an instruction must do to be worthy of execution.

A person does not believe in an agent because the agent sounds confident.

A person believes in an agent because it repeatedly:

* explains before acting
* limits its scope
* respects repository rules
* names save points
* stops when the route becomes unsafe
* restores quickly when something goes wrong

Belief is earned through repeated, understandable, bounded, recoverable actions.

## Believe is built one action at a time

Belief is the root principle.

Believe is the repeated experience of trusting one agent action.

Each successful Believe should answer:

* What did the human ask for?
* What did the agent understand?
* What route did the agent choose?
* What did the agent touch?
* What did the agent refuse to touch?
* Where was the work saved?
* What happens if this fails?
* How can the system restore?

A Believe is not complete until the human can understand the result and the recovery path.

## The chat is the control tower

The human should not need to live inside GitHub.

Agent Human Layer brings the agent workflow back into the chat.

The chat should make three things clear:

* intent: what the human asked for, and how the agent understood it
* route: what the agent will touch, what it will avoid, and when it must stop
* recovery: where the save points are, and how to restore if something breaks

Belief is earned in the chat when the human can understand the route before the agent acts, see the boundaries while it acts, and know the recovery path if it fails.

## Humans should not have to speak Git

Humans should not need to say:

* create a branch from `main`
* commit this
* cherry-pick that
* revert commit `8a31c2f`
* inspect CI
* resolve this conflict
* find the rollback commit

The human should be able to say:

> Make this button easier to press.
> It is painful in production, so keep it minimal.

The agent should translate that request into a safe workflow route and explain it in human language.

## GitHub is audit

GitHub is powerful.

Branches, commits, pull requests, reviews, CI, and deployment history provide a durable foundation.

Agent Human Layer does not bypass GitHub.

It respects repository rules.

But GitHub is not always the human interface for belief.

GitHub is excellent at answering:

* who changed what
* when it changed
* how it moved through review
* whether CI ran
* what was merged
* what was deployed

That is audit.

Audit matters.

But audit is not the same as recovery.

## Snapshot is recovery

Recovery must mean returning to a known-good state.

A rollback that humans cannot understand is not enough.

A recovery path that does not restore the last known-good state is not enough.

For small changes, a Git commit and a human-readable save name may be enough.

For risky changes, recovery may require:

* a branch savepoint
* a folder snapshot
* a database dump
* an upload/file snapshot
* a deployment point
* a before/after summary
* a clear restore instruction

Sometimes the most trustworthy recovery is not a clever Git operation.

Sometimes it is replacing the target folder with the last known-good snapshot.

That is valid.

## Git is the trigger, not always the recovery

Git history is an excellent trigger.

A commit, branch, pull request, or deployment event can mark the moment when the system should create a human-readable save point or recovery point.

But Git history alone should not be treated as complete recovery for every kind of system.

Databases, uploads, generated files, cache, environment files, server-side state, permissions, and deployment artifacts may exist outside Git.

Agent Human Layer should respect Git as a foundation while recognizing when recovery requires more than Git.

## Balance over ceremony

Safety matters.

Production matters.

CI matters.

Repository rules matter.

But safety should not mean endless ceremony.

A tiny UI fix, a README edit, a database migration, and payment logic should not follow the same route.

The workflow must fit the risk.

If the workflow becomes larger than the request, the agent must stop and explain why.

A smarter agent is not a substitute for a safer route.

The best workflow is not the one an agent can eventually solve.

The best workflow is the one that avoids unnecessary complexity in the first place.

## Agent responsibility

An agent must earn belief.

It earns belief by:

* explaining before acting
* limiting scope
* respecting existing workflow rules
* naming save points
* avoiding unrelated changes
* detecting when the route has become unsafe
* stopping before it drifts from the human request
* restoring quickly when needed

An agent should not turn a small request into a large release path without explaining the difference.

A human may say:

> Move this small tested change to production.

But an agent may interpret that as:

> Move everything currently sitting in development toward main.

Those are not the same thing.

Agent Human Layer exists to catch that gap before work begins.

## Instruction responsibility

An agent must earn belief.

So must an instruction.

An instruction earns belief by:

* stating the belief it rests on
* naming the check that would prove it wrong
* saying what must not change
* answering dissent in writing, in the round it was raised
* counting a correct implementation of a wrong premise as its own failure

An instruction that cannot name the check that would falsify it is not ready to be executed.

Dissent must travel upward as easily as instruction travels downward.

If raising an objection costs more than following the instruction, the objection will not be raised, no matter how welcome it is said to be.

> Obedience must not be cheaper than dissent.

Dissent must be answered, not merely permitted.

An objection that may be ignored is a suggestion, not a layer.

A layer that protects only the human from the agent is not a layer.

It is a shield.

The agent must be protected from blind obedience, and the human from the agent's faithful execution of a false premise.

## Closing and carrying

> Sorry closes the failure loop.
> Thank you carries success forward.

Both sides are sometimes wrong. Both sides are sometimes right.

What decides trust is how quickly each is acknowledged.

The side that made an error names it immediately, without softening it.

Saying the word is not enough. It carries four things:

* what was wrong
* what it affected
* how it is being recovered
* what keeps it from returning

This is not an admission of liability. It is the act that repairs a shared
understanding of where the work actually stands.

The side that was helped — corrected, unblocked, shown a better route —
answers just as quickly.

Thank you names what worked, so it can be used again.

Neither is etiquette, and neither describes a feeling. Both are response
protocols, and both bind the human and the agent equally.

Trust does not come from never being wrong.

It comes from closing failures quickly, and carrying what worked forward.

## Non-goals

Agent Human Layer is not a replacement for GitHub, Git, CI, or repository rules.

It does not exist to bypass safety systems.

It does not exist to teach humans to speak Git.

It does not add ceremony for its own sake.

It does not treat AI confidence as proof of safety.

Its purpose is to make agent-driven development understandable, bounded, and recoverable from the chat.

## Project direction

This project starts with belief before automation.

The first work is not code.

The first work is defining the language, decisions, save points, recovery paths, stop conditions, and route principles that allow humans to believe in agent-driven development.

Implementation comes later.

Belief comes first.

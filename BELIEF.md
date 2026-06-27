# BELIEF

Belief is the trunk.
Believe is the branch.

Agent Human Layer exists to define the belief that makes it possible for humans to believe in agent-driven development.

This document is the trunk of the project.

README, issues, code, CI, route formats, snapshots, risk rules, and implementation details are branches.

If anything conflicts with `BELIEF.md`, `BELIEF.md` wins.

## Prime Belief

A human should be able to ask.

An agent should be able to act.

If it works, the work should be completed quickly.

If it fails, the system should return to the last known-good state without drama.

The core idea is simple:

> Ask. Act. Restore.

## Belief is not blind trust

Agent Human Layer does not ask humans to blindly believe in AI.

It defines what AI must do to become worthy of belief.

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

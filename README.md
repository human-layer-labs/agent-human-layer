# Agent Human Layer

Agent Human Layer is a belief system for agent-driven development.

Start with [BELIEF.md](./BELIEF.md).

The core idea is simple:

> Ask. Act. Restore.

Humans should be able to ask in plain language.
Agents should act within clear boundaries.
If something breaks, the system should restore to the last known-good state.

The chat should become the control tower.

## Why

Coding agents can now write code, edit files, open pull requests, run CI, and deploy changes.

That is powerful.

But power alone is not enough.

For humans to believe in agent-driven development, they need to understand three things from the chat:

* intent: what the human asked for, and how the agent understood it
* route: what the agent will touch, what it will avoid, and when it must stop
* recovery: where the save points are, and how to restore if something breaks

Agent Human Layer exists to make chat-based agent development understandable, bounded, and recoverable.

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

GitHub is audit.
Snapshot is recovery.
The chat is the control tower.

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

## Cases

[cases/](./cases/) holds write-ups of real incidents from agent-driven development — what
happened, what caught it, and what changed afterwards.

Belief is the trunk. Skills are the method. Cases are the evidence.

* [2026-07-22 — The field that erased itself](./cases/2026-07-22-silent-field-erasure.md)

## Project status

This project is developing its belief, its operational methods, and its field evidence.

The first goal is to define the language, decisions, save points, recovery paths, stop conditions, and route principles that allow humans to believe in agent-driven development.

That definition is not written in the abstract. It is corrected by what actually happens —
which is what [cases/](./cases/) is for. Belief explains reality; reality updates belief.

Tooling comes later.

Belief comes first.

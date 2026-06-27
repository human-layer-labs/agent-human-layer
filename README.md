# Agent Human Layer

Agent Human Layer is a belief system for agent-driven development.

Start with [BELIEF.md](./BELIEF.md).

The core idea is simple:

> Ask. Act. Restore.

Humans should be able to ask in plain language.
Agents should act within clear boundaries.
If something breaks, the system should restore to the last known-good state.

The chat should become the control tower!

## Why

Coding agents can now write code, edit files, open pull requests, run CI, and deploy changes.

That is powerful!

But power alone is not enough.

Humans still need to understand:

* what the agent is about to do
* which repository it will touch
* whether the work is small, normal, risky, or urgent
* what route it will take
* what it will not do
* where the work is saved
* how to recover if something breaks

Agent Human Layer exists to make chat-based agent development worthy of belief.

Not by asking humans to blindly trust AI.

By making the agent's route, scope, save points, stop conditions, and recovery path visible from the chat.

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

It respects GitHub as a durable foundation.

But recovery is not always the same as Git history.

Sometimes the most trustworthy recovery is not a clever Git operation.

Sometimes it is replacing the target folder with the last known-good snapshot.

Agent Human Layer adds a human-readable decision and recovery layer on top of GitHub.

Belief is earned in the chat when humans can understand the route, see the save points, and know how to restore.

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

## Balance over ceremony

Safety matters.

Production matters.

CI matters.

But safety should not mean endless ceremony.

A tiny UI fix, a README edit, a database migration, and payment logic should not follow the same route.

The workflow must fit the risk.

A smarter agent is not a substitute for a safer route.

The best workflow is not the one an agent can eventually solve.

The best workflow is the one that avoids unnecessary complexity in the first place.

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

## What this project is not

Agent Human Layer is not:

* a Git tutorial
* a generic Git wrapper
* a GitHub replacement
* a CI dashboard
* a way to bypass repository rules
* a system for adding ceremony for its own sake
* a tool that asks humans to memorize commit hashes

## Project status

This project is at the belief and design stage.

The first goal is to define the language, decisions, save points, recovery paths, and stop conditions that allow humans to believe in agent-driven development.

Implementation comes later.

Belief comes first.

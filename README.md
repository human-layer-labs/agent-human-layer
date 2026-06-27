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

Agent Human Layer exists to make that visible from the chat.

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

We do not ask humans to blindly believe in AI.

We define what AI must do to become worthy of belief.

## GitHub, snapshots, and chat

GitHub is audit.
Snapshot is recovery.
Chat is belief.

GitHub is excellent at showing who changed what, when, and how it moved through branches, pull requests, CI, and deployment.

But recovery is not always the same as Git history.

Sometimes the most trustworthy recovery is not a clever Git operation.

Sometimes it is replacing the target folder with the last known-good snapshot.

Agent Human Layer does not bypass GitHub.

It respects GitHub as a durable foundation and adds a human-readable recovery and decision layer on top of it.

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

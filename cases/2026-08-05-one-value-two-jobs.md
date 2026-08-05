# 2026-08-05 — One value, two jobs

> **Three defects found in six days, in three unrelated systems.** A deployment version,
> a backup snapshot, and the chapter numbers of this repository. Same shape every time.
> Nothing reached incident; two were caught before they could.

## Context

Three places where a single value was being read by two different consumers, for two
different reasons:

| The value | Job A | Job B |
|---|---|---|
| Plugin version string | this deploy arrived | re-run the database migrations |
| "the latest snapshot" | the newest file in the backup directory | the state we can safely return to |
| Chapter number | where a chapter sits in the reading order | which chapter this is |

In every case, Job A wants the value to **change often**. Job B wants it to **never change**,
or to change only under different conditions.

That is not a naming problem. It is two lifecycles sharing one storage location.

## What happened

**1. The version that also triggered migrations.**

Deployment is over SSH. Nothing on the target announces itself, so the version string is bumped
on every deploy — otherwise there is no way to confirm the code arrived. That is Job A, and it
was working correctly.

Six database migration gates were written as `if stored_version === current_version: skip`.
That is Job B. Because Job A bumped the version every time, **Job B fired on every deploy** —
including deploys that changed nothing but a stylesheet.

It had been doing this for months. It surfaced as a schema warning printed on every deploy,
which everyone had learned to scroll past. The find came from reading the line *underneath* the
familiar warning.

The fix separated the jobs: completed migrations now set a fixed marker that never moves. The
version was left alone. **Nothing about the deployment practice was wrong — the code did not
match a practice that had been correct all along.**

Three gates stayed version-linked on purpose, because for those, re-running on every version
really is the intended behaviour. A check now pins that number at exactly three; a fourth makes
it fail. That check was verified by growing a fourth gate on purpose and watching it fail.

**2. The snapshot that was "the latest."**

A snapshot of the deployed folder is written immediately before every deploy. The recovery
runbook said: restore the latest snapshot.

Both halves of that sentence are true and they do not mean the same thing. Snapshots are taken
*before* a deploy, so **every snapshot holds the state in which that deploy has not happened
yet.** Restoring the latest one does not return you to now. It silently undoes the most recent
deploy.

In this instance the most recent deploy was fix #1 above. Restoring would have reverted it —
**with no symptom.** The stored migration markers still held the old version string, so the old
code's gate would have matched and skipped. Everything would have looked correct until the next
version bump, months later.

**3. The chapter numbers of this repository.**

Two pull requests were open at the same time, both titled *Chapter 3*. One merged; the other did
not. Nothing broke, because chapter numbers only govern prose.

But the numbers had also spread into the chapters themselves — subtitles, section headings
(`## Chapter 2 held`), and arguments in the body (*"Chapter 1 governs code; Chapter 2 governs
beliefs"*) — and into the case files, where one line pointed at a **Chapter 1 that does not
exist**. This repository calls its first document the trunk, not a chapter. A reader following
that reference would have gone looking for something that was never there.

## What caught it

Nothing systematic. Three different accidents:

* **#1** — reading one line below a warning that appeared on every single deploy
* **#2** — a 2,116-byte difference between two archives that should have been identical, on a
  day when nobody had touched the server
* **#3** — an agent halting on an instruction's own stop condition, and reporting the one line
  that did not fit

Only the third was a mechanism. The other two were somebody declining to round off a detail that
did not fit — which is not a mechanism, and cannot be relied upon.

## What made recovery cheap

**#1 and #3 never reached a bad state.** #1 was found by reading, before anything was restored.
#3 stopped before a single file was written.

**#2 was found while preparing a fire drill** — a deliberate break-and-restore, rehearsed
because the rollback path had been trusted for months and never actually used. The drill was
supposed to measure recovery time. It found a defect in the first step of recovery instead.

The guard that mattered in #2 was ordinary and manual: the archives were extracted and compared
before anything was swapped, because the size did not add up. That comparison is now the first
step of the runbook, ahead of the restore itself.

## What changed

**One rule, applied three times: give each job its own value.**

```
version        stays the delivery mark.  Migrations moved to a fixed marker.
snapshots      "latest" is no longer a valid selector. The runbook now asks which
               state you want back, and diffs the candidate against live before swapping.
chapter number lives in the README only. Chapters refer to each other by name.
```

Two second-order lessons came out of it:

**A number is evidence of arrival, never evidence of return.** #2 was created by editing files
in place, so the version never moved — before the break and after the restore it read the same.
Proof of restoration had to become a diff against the snapshot, not a version comparison.

**Collision is a symptom worth reading, not just a clash to resolve.** In #3, the two pull
requests claiming the same number turned out to be developing the same idea in two places, each
unaware of the other. Renumbering would have resolved the clash and hidden the duplication.

## For other teams

* **Look for a value that two consumers read for two different reasons.** Ask each one: *does
  this need to change often, or never?* If the answers differ, you have this defect already.
* **The one that changes often will win**, because changing it is somebody's routine. The other
  job fails quietly, at whatever interval that routine runs.
* **Symptoms appear far from the cause and on a delay.** A migration re-running on a
  stylesheet deploy. A rollback that reverts a fix from last week. Nobody experiences these as
  "the version means two things."
* **Do not fix it by renaming or renumbering.** That moves the collision; it does not remove
  the second job. Move the job.
* **When you separate them, name which uses are deliberately left shared** — and pin the count
  with a check, so a fourth one cannot appear unnoticed.
* **Prefer names over ordinals for anything quoted from outside.** An ordinal encodes a position
  that will move. A name does not.
* **Verify guards by breaking them on purpose.** The check pinning "exactly three" was trusted
  only after a fourth was added and it actually failed.

> **A value that two things depend on will eventually be moved by one of them,
> and broken for the other.**

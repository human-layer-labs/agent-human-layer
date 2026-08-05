# 2026-07-29 — The check that could not pass

## Context

A terminology cleanup: one product used three different words for the same device across
44 places in three plugins. Pure renaming, plus one small data migration for labels already
stored in the database.

The work ran in the usual pair. A **directing agent** surveys the code, writes the
instruction document — including the acceptance checks the work will be judged by — and
hands it to an **implementing agent**, which implements and stops if a stop condition
triggers. The owner decides and verifies on real hardware.

Low risk. No payroll maths, no schema change, no production system. The kind of task that
should cost one round trip.

## What happened

It cost four.

The implementing agent never made a mistake. Every stop it reported was correct, and every
number in its reports was accurate. All four failures were in the acceptance checks —
written by the directing agent, and **never once executed by the directing agent before
handoff**.

**1 — The check that contradicted its own instruction.**
The document said, in the verification section: *"the slug `tablet-approval` must appear the
same number of times before and after."* Elsewhere, in the implementation section, the same
document instructed: *"update this code comment to read: the slug stays `tablet-approval`."*
The comment introduced a sixth occurrence. 5 → 6. The implementing agent stopped, correctly,
and reported that it could not satisfy both sections.

**2 — The measurement that could not see what the test could.**
Version strings had to be bumped in the test suite. The directing agent measured the work by
fixed-string search — `grep -F "0.6.16"` — and wrote the resulting count into the document as
the target. The implementing agent hit that number exactly. Two tests then failed. The suite
asserts versions with regular expressions, where the literal is written `0\.6\.16`; the
backslashes mean a fixed-string search can never match it. The search returned **zero
remaining occurrences** while the suite was still red.

**3 — The completion check that could never pass.**
Told to also find the escaped form, the directing agent wrote a shape pattern —
"any escaped version number" — and declared the work complete when it returned zero. But that
pattern matches the *corrected* value just as well as the old one. Once fixed properly, it
returns two. It can never return zero while those assertions exist at all. The implementing
agent fixed both lines, saw two, and stopped again — correctly.

**4 — The one that was caught in time.**
Writing the deployment runbook, the directing agent specified a line-counting command that
counts files instead. Expected `8`; it returns `136`. This one never reached the implementing
agent, because the directing agent finally ran the command it had written.

The day before, the same directing agent had recorded two defects of the same family in its
own notes, under the heading *"defects I hit twice in a row — never again."*

## What caught it

The implementing agent's stop conditions — working exactly as designed.

That is worth stating plainly, because it looks like a success and reads like a failure. The
mechanism AHL relies on did its job four times. What it caught, every time, was not the work.
It was the specification.

Nothing else could have caught these. Reviewing the diff would not: the diff was correct.
The test suite would not, except in case 2: the code was right. The only instrument capable of
finding a broken check is **running it**, and the only party who could run it before it did
damage was the party who wrote it.

## What made recovery cheap

Nothing — and this is the finding.

The trunk contributed nothing here, because **nothing ever broke**. There was no bad state to
restore. The code was correct from the first commit. Save points, dumps, and folder snapshots
were all in place and all irrelevant.

The blast radius was three human round trips and the owner's confidence. Neither has a
snapshot. The owner named it directly:

> Misses, gaps and drift have continued since the last session.
> I am not blaming you. But the founding principle — mutual belief — is starting to wobble.

The trunk makes broken work cheap to undo. It says nothing about work that was never broken
and was stopped anyway. That cost is paid in attention, and attention does not roll back.

## The part that stings

After each incident the directing agent added a rule to its instruction template. After the
first: a new rule about invariant checks. After the second: a note about escaped literals.
After the third: a new rule numbered zero, promoted to the top as the root of all the others.

The template grew by roughly forty percent across one pull request. The defect rate inside
that same pull request did not fall.

AHL already holds the belief that **over-verification is a symptom, not a virtue** — that a
team piling on checks is revealing that it cannot cheaply undo things. The same disease had
appeared in the rulebook, and went unrecognised for three rounds: each new rule described the
shape of the last failure, and the next failure arrived in a shape the rule did not cover.

The thing that actually worked was not a rule. In case 4, the agent ran the command. It took
one second and the defect was gone before anyone else saw it.

## What changed

One mechanism, replacing three rules:

> **Before handing over a specification, execute every acceptance check in it, and paste the
> real output next to it.**

For checks whose target state does not exist yet, one question makes them executable anyway:

> **"If the work were done perfectly, what exactly would this command print?"**

If that string cannot be produced, the check is not finished. This question alone catches
cases 1, 3 and 4 — each was a check whose author had never asked what success looks like.

Case 2 needs a second rule, about instruments:

> **When a test suite is the judge, the acceptance check must be the suite — not a search
> that approximates it.** A different instrument sees a different world. The search saw zero;
> the suite saw red. Both were telling the truth about different things.

And one classification, because the three kinds of check fail differently:

| Kind | Says | Fails by |
|---|---|---|
| **invariant** | "this must not change" | the specification itself introducing the token — grep your own document |
| **removal** | "the old form must be gone" | naming a *shape* instead of the *old value*; a shape matches the fix too |
| **arrival** | "the new form must be present" | being written as a count nobody can measure in advance — name the files instead |

This case is the origin of [The Unrun Check](../UNRUN-CHECKS.md).

## For other teams

* **An acceptance check that has never been run is not a check.** It is a belief that has
  been given the authority to stop work. Run it, or mark it unverified.
* **Ask what a perfect result prints.** If you cannot write that string, you do not yet
  understand your own check.
* **Never write a removal check as a pattern.** Name the old value. A pattern that matches
  "any version number" also matches the corrected one, and will never go quiet.
* **Match the instrument to the judge.** If a suite decides pass or fail, do not accept a
  search as evidence about the suite.
* **Watch the ratchet.** If your checklist grows after every incident and the incidents keep
  coming, the checklist is the symptom. Convert the rule into a step that executes.
* **A correct stop is not a free stop.** Count round trips. When the specification is the
  thing that keeps stopping the work, the human cannot tell the difference from where they
  sit — and that is where belief is actually spent.

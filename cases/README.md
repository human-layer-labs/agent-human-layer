# Cases

Real incidents from agent-driven development, written up so other teams can reuse the lesson.

`BELIEF.md` is the trunk. `skills/` is the method. **Cases are the evidence.**

A case is not a success story. It is a record of what actually happened, including the parts
that went wrong, and what changed afterwards.

## What makes a case worth writing

Write one when something surprised you. Especially:

* a near miss that was cheap to recover from — and *why* it was cheap
* a defect that a green test suite could not see
* a gap between what an agent reported and what it did
* a boundary that turned out to be invisible until it was crossed

Do not write one to demonstrate that the method works. Write one when reality corrected the method.

## How to write a case

Keep it short enough to read in one sitting. Suggested shape:

1. **Context** — what was being built, and what could have been damaged. Say separately
   *what was wanted* and *what was believed* — the belief that collided with reality is the
   part another team can reuse
2. **What happened** — plainly, in order, without softening
3. **What caught it** — the specific mechanism, not "we were careful"
4. **What made recovery cheap** — the guards that already existed before the incident
5. **What changed** — the concrete rule adopted afterwards
6. **For other teams** — what to copy

Name what it cost and what was recovered — one line each is enough. Naming a cause is
optional: a case records what occurred; it is not obliged to explain it.

Two rules:

* **Sanitize.** No hostnames, credentials, key paths, customer names, or personal data.
  Describe environments by role ("the test environment"), not by address.
* **Be accurate over impressive.** If production was never at risk, say so. An inflated case
  teaches nothing and costs credibility. The interesting question is usually
  *why the blast radius was small*, not *how close it came*.

## Claims and evidence

A case is not established truth. It is a set of **bounded claims**, each carried with the
evidence, scope, and provenance it actually has. Turning a report into a case is structuring,
not promotion to fact: a published case may still contain claims nobody has verified — as
long as it says so.

Most cases need none of the machinery below — the shape above is enough, because the writer
lived the incident. Bound a claim explicitly when it is load-bearing and the maintainers of
this repository could not check it themselves. A case contributed from outside almost always
has at least one such claim. Do not turn every sentence into a claim.

A bounded claim is a small labeled block:

> **Claim:** the migration gate fired on every deploy, not only on schema changes
> - state: DECLARED
> - evidence: deploy log for June–August, held by the reporter
> - scope: one plugin's deploy pipeline; nothing is claimed beyond it
> - provenance: observed by the reporter; prose written by their agent from the log
> - observed_at: 2026-08-04

What keeps this honest:

* **The four evidence states** — `DECLARED`, `OBSERVED`, `VERIFIED`, `UNEVALUATED` — are
  owned by [`ahl-flow.md`](../skills/agent-human-layer/references/ahl-flow.md). A case uses
  them; it does not redefine or extend them. "We don't know" is said in plain prose and the
  claim stays `DECLARED` or `UNEVALUATED` — an unestablished claim may remain unestablished
  and still be published, visibly so.
* **The state line is this repository's position.** A published case speaks in this
  repository's voice, and a claim that arrives carried — supported only by the reporter's
  account — stays `DECLARED` here, however confident the account: carrying a claim does not
  raise its state (`ahl-flow.md`: memory may carry a claim; it must not raise Evidence
  state). The reporter's own observation is not erased — it lives in the evidence and
  provenance lines, exactly as reported. Publication changes no state.
* **No automatic promotion.** A state rises only through actual observation or verification
  against a named source — never because time passed, the case was published, or the claim
  was restated.
* **Provenance is not a trust ranking.** Human-written and agent-written text are not ranked
  by origin. Distinguish, where it matters: who observed, who produced the text, what
  transformed it, what the source was, when it was observed (`observed_at`), when it was
  generated (`generated_at`), and whether a human reviewed it (`human_reviewed`). When an
  agent turns a log into prose, the evidence source is **the log, not the agent** — the
  agent is producer and transform.
* **Raw evidence never lands in this repository.** The case names it and bounds it; the
  reporter keeps it.

**Publication condition.** A public case carries at least one bounded claim with scope and
provenance. If the available evidence cannot bound a single claim, the record is not yet a
case — it stays a report / case candidate, unpublished.

The block shape above is provisional — the smallest reversible representation, kept only
until the first external case has graded it.

## Revisions, lineage, and withdrawal

* **Corrections are visible.** A published case is corrected with a dated revision note,
  never silently overwritten — the previous meaning stays readable. One exception: removal
  of secrets or personal data, where keeping a public trace of what was removed would itself
  do harm.
* **Lineage stays the existing convention.** When a case actually produces a derived
  artifact — a chapter, check, rule, or change — the case links it from "What changed" (or
  its index entry), and the derived artifact points back with an `*Evidence: cases/…*`
  footer, as [CHEAP-DEATH.md](../CHEAP-DEATH.md) and [UNRUN-CHECKS.md](../UNRUN-CHECKS.md)
  already do. Plain relative links; no IDs, no graph. "Could be derived" is not derived and
  gets no link.
* **A case contributed from outside records its provenance without exposing the private
  report** — channel, dates, and the reporter's consent; nothing more.
* **Withdrawal is not correction.** A contributor may withdraw; a claim is corrected or
  retracted on evidence. These are different acts. Withdrawal does not automatically delete
  derived artifacts — each goes to review for independent evidence, by hand.

## Index

* [2026-07-22 — The field that erased itself](./2026-07-22-silent-field-erasure.md)
  A payroll field was silently overwritten with NULL on every save. Every test passed.
  A UI feature — not a test — is what exposed it.
* [2026-07-24 — The belief that had to be built before it could die](./2026-07-24-the-wrong-axis.md)
  Four phases were built on the wrong domain axis. Every test passed — tests verify a design
  against itself. The refuting fact was known, unwritten, on day one.
  Origin of [Cheap Enough to Die](../CHEAP-DEATH.md).
* [2026-07-26 — The suite was green; the schema was broken](./2026-07-26-green-logic-broken-schema.md)
  A migration silently created one of two new tables — a duplicate column the in-memory test
  stand-in never parsed. Logic green is not schema green. Caught by checking the real database;
  cheap to undo because the dump was taken first.
* [2026-07-29 — The check that could not pass](./2026-07-29-the-check-that-could-not-pass.md)
  Four correct stops in one pull request, all caused by acceptance checks the directing agent
  had written but never run — including one that could never pass. Nothing broke, so rollback
  had nothing to restore; the cost was round trips and belief.
  Origin of [The Unrun Check](../UNRUN-CHECKS.md).
* [2026-07-31 — Implementation is not delivery](./2026-07-31-implementation-is-not-delivery.md)
  A destructive option was kept alive because its safe replacement was invisible. The safe one
  had a button, a correct label, and tests — but nothing on screen explained what it did.
  The system's own designer could not tell it existed. One of three cases cut from the same flow.
* [2026-07-31 — The premise that lived in one head](./2026-07-31-unstated-premise.md)
  Five defects on one screen, fixed separately over one day, all had a single cause: a layer
  model that existed only in the human's head. Once written, all five collapsed into one.
  You cannot ask about a structure you do not know exists.
* [2026-07-31 — It looked like a mismatch until it was too wide to be one](./2026-07-31-drift.md)
  Nine releases, zero rollbacks — and two designs in a row came out wrong. The angle had been
  turning a few degrees at each restatement. Drift requires return, not patching. Stop on the
  felt sense; classify after stopping.
* [2026-08-04 — The instruction that nothing was watching](./2026-08-04-faithful-to-a-false-premise.md)
  Eight checks were written before the change, run, and all passed. The implementation matched the
  instruction exactly — and the instruction was wrong. Every check asked whether the work was done,
  none whether the premise was right.
  Origin of [The Unchallenged Instruction](../UNCHALLENGED-INSTRUCTION.md).
* [2026-08-05 — The snapshot that was not known-good](./2026-08-05-the-snapshot-that-was-not-known-good.md)
  A rollback path trusted for months, rehearsed on purpose and timed twice: under a second on the
  server, one minute for the human. The drill found the defect before an outage did — snapshots are
  taken *before* each deploy, so restoring the newest one silently undoes the most recent fix.
* [2026-08-05 — One value, two jobs](./2026-08-05-one-value-two-jobs.md)
  A deploy version that also triggered migrations, a backup selector that also meant "safe to
  return to", and this repository's own chapter numbers. Three systems in six days, one shape:
  the job that moves a value often will quietly break the job that needed it to hold still.

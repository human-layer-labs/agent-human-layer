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

1. **Context** — what was being built, and what could have been damaged
2. **What happened** — plainly, in order, without softening
3. **What caught it** — the specific mechanism, not "we were careful"
4. **What made recovery cheap** — the guards that already existed before the incident
5. **What changed** — the concrete rule adopted afterwards
6. **For other teams** — what to copy

Two rules:

* **Sanitize.** No hostnames, credentials, key paths, customer names, or personal data.
  Describe environments by role ("the test environment"), not by address.
* **Be accurate over impressive.** If production was never at risk, say so. An inflated case
  teaches nothing and costs credibility. The interesting question is usually
  *why the blast radius was small*, not *how close it came*.

## Index

* [2026-07-22 — The field that erased itself](./2026-07-22-silent-field-erasure.md)
  A payroll field was silently overwritten with NULL on every save. Every test passed.
  A UI feature — not a test — is what exposed it.
* [2026-07-24 — The belief that had to be built before it could die](./2026-07-24-the-wrong-axis.md)
  Four phases were built on the wrong domain axis. Every test passed — tests verify a design
  against itself. The refuting fact was known, unwritten, on day one. Origin of Chapter 2.
* [2026-07-26 — The suite was green; the schema was broken](./2026-07-26-green-logic-broken-schema.md)
  A migration silently created one of two new tables — a duplicate column the in-memory test
  stand-in never parsed. Logic green is not schema green. Caught by checking the real database;
  cheap to undo because the dump was taken first.
* [2026-07-29 — The check that could not pass](./2026-07-29-the-check-that-could-not-pass.md)
  Four correct stops in one pull request, all caused by acceptance checks the directing agent
  had written but never run — including one that could never pass. Nothing broke, so rollback
  had nothing to restore; the cost was round trips and belief. Origin of Chapter 3.

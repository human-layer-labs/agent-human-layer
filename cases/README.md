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

# 2026-08-04 — The instruction that nothing was watching

## Context

The same payroll system as [the wrong axis](./2026-07-24-the-wrong-axis.md), one working layer further on.

Wage conditions are resolved through layers: per employee, then by wage type,
then site-wide, and finally a baseline underneath them all.

Two things live in that baseline and they are not the same:

* **statutory floors** the product ships, so that pay can be calculated at all
* **the starting point a workplace chose for itself**

The human asked for those two to be visibly distinguished on screen.
A shop that fills in one field should still see, in every untouched field,
that what is holding the number up is the statutory floor and not a decision anyone made.

Work ran in a director/implementer pair of two agents,
with the director verifying independently after each round.

## What happened

The directing agent wrote the instruction, including the code to replace and the code to replace it with.

The replacement resolved the source of a value **for the whole profile**:
if the workplace had saved anything into the baseline, the baseline was marked as the workplace's.

The implementing agent implemented it exactly as written.

Everything the instruction asked for passed:

* syntax check on every changed file
* the full suite: 42 passing, 0 failing
* eight source counts, each measured before the change and named in the instruction as an expected value
* an independent re-run of all of it by the directing agent

The change shipped in that state.

The consequence was that a shop saving a single field would see **every** baseline value
relabelled as its own decision — including the statutory multipliers nobody had touched.
Which is the opposite of what was asked for.

## What caught it

Not a test. Not the review. Not the verification pass.

It surfaced while reading a neighbouring file for an unrelated question about a minimum-wage warning.
The label map two layers away only knew four source names, and the new one was not among them.

The requirement was not missing. It had been written down plainly, in the human's own words, that morning.
The instruction contradicted it at a granularity that nothing in the instruction ever looked at.

## The part that stings

The instruction carried eight checks, and all eight were run.

Every one of them asked the same question in a different form:
*does the implementation match the instruction?*

None of them could ask whether the instruction was right.

The implementing agent did nothing wrong.
The report was accurate, the counts were honest, the code was exactly what was specified.
Faithfulness worked perfectly, and that is precisely how the wrong premise arrived intact.

The failure did not happen where the work happened.
It happened one step earlier, and nothing was watching that step.

"Cheap Enough to Die" had already named this duty. *Dissent is not a right. It is a duty.*
It was named, and it still did not fire — because the report was written after the work,
and raising a doubt before it meant stopping, waiting, and being asked to justify the pause.
Following the instruction cost one round. Questioning it cost two.

Later in the same day the report format was changed to require a "what I doubted" field.
The very next round, the implementing agent used it — and caught a count the director had missed.
The duty had existed all along. What changed was the price.

## What made the discard cheap

Cost: one file, twelve lines added, one removed. No stored value changed — only labels.

* the change was still a draft when it was found
* the layer it touched was resolution, not storage
* rollback was a tarball extraction, and no database had been touched

Chapters 1 and 2 paid for this. The correction was a footnote, not an incident.

## What changed

One rule: an instruction must arrive carrying what would refute it.
Not the check that proves the work was done — the observation that would show the premise was wrong.

For this instruction it was one line, and it could have been written before any code:

```
Belief: a value resolved from the baseline came from the workplace's own starting point.
Refuted if: a workplace saves one field, and an untouched statutory floor
            is also shown as the workplace's choice.
```

That is not a test anyone needed to build. It is a sentence, and reading it kills the belief.

This case is the origin of [The Unchallenged Instruction](../UNCHALLENGED-INSTRUCTION.md).

## The tail that is still open

The correction is merged and deployed.

Nobody has saved an initial setting on the running system yet, so the fix has never been observed working.

Every check is green and has been green since the day the mistake shipped.
Green was never the thing that could tell us.

## For other teams

* A green suite proves the implementation matches the instruction.
  It cannot prove the instruction was right. Those are different questions, and only one of them is tested.
* Ask of every material belief in an instruction: *what observation would show this is wrong?*
  If none can be named, the instruction is not finished being thought about.
* Count a correct implementation of a wrong premise as a failure of the instruction.
  Otherwise the record will say every implementation succeeded, which will be true and useless.
* If raising a doubt costs an extra round and following costs none, the duty to dissent will not be exercised.
  Make the doubt a required field in the report, answerable in the same round.
* The side that writes the instruction should not be the only side that checks it.

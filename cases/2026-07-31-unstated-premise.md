# 2026-07-31 — The premise that lived in one head

> **One of three cases cut from the same flow.** Nothing here reached incident.
> See also: [implementation-is-not-delivery](./2026-07-31-implementation-is-not-delivery.md) ·
> [drift](./2026-07-31-drift.md)

## Context

A payroll settings system where values are resolved through layers — per employee,
per wage type, and a workplace-wide baseline — and where changes carry an effective date.

Nine releases shipped that day. Zero rollbacks, zero data loss, zero fatals.
The two design failures described here were both stopped before reaching implementation.

## What happened

Over one day, five separate defects were reported and fixed on the same screen:

* a notice listing fields the user had never touched
* a default effective date of `2000-01-01`
* a red warning shown on a setting that was not configured at all
* a wage-type profile id read against the wrong table
* untouched values appearing as changed when the date was moved backwards

Each was diagnosed independently. Each got its own fix. **The fifth one broke the design twice.**

Then the human stopped the work:

> これは明確に私と貴方との間で認識の齟齬ができていると考えるのが妥当
> **そして徐々に拡がりつつある**
> *There is clearly a mismatch in understanding between us. And it is gradually widening.*

And named the actual structure:

> システムが「時間を持つ設定」に進化したのに、
> **比較ロジックだけ昔の単純設定の語彙を引きずっていた**
> *The system had evolved into settings that carry time, but the comparison logic was still
> dragging the vocabulary of simple settings.*

A three-layer model with per-layer time axes existed **in the human's head**.
It existed **nowhere in writing**. The agent had never held it.

Once written down, **all five defects were explained by one cause.**

## What caught it

The human, by noticing that the conversation was widening rather than converging.

**The agent did not catch it.** It had been producing plausible fixes for each symptom
and had no signal that the symptoms shared a root.

Worth being precise about the failure mode: the agent was not misunderstanding.
It received each statement correctly and implemented it correctly. **What it lacked was
not an answer but the existence of a question.** You cannot ask about a structure you do
not know exists.

> **先程はこの前提条件を私が端折ったから misalignment が延々続いてしまっていた**
> *I had skipped the premise, which is why the misalignment kept going.*

This is worth recording without assigning fault. **Everyone omits their own premises** —
they do not feel like information, they feel like the floor.

## What made recovery cheap

Nothing had to be rolled back. Both design failures were stopped before code shipped:

* the first by an existing test suite that encoded the old, correct behaviour
* the second by the directing agent's own simulation, run before writing the instruction

The five shipped fixes were not wasted either. They were mechanically correct;
only the comparison basis was wrong. As the human put it, **the machinery was right,
the yardstick was not.**

## What changed

A verification step was adopted for premises:

```
When a premise is finally written down, check it backwards:
★ do the past symptoms become explainable by it?
   yes → the premise is right
   no  → something is still missing
```

Here, five symptoms collapsed into one cause the moment the layer model was written.
That collapse *is* the evidence.

Two supporting rules:

* When a term appears that you do not hold a definition for — "layer", "axis", "revision" —
  **ask for the definition on the spot.** Do not accept it by inference.
* When three or more separate fixes land in one area, stop. That count is itself the signal.
  **Ask for the premise, not for the correction.**

## For other teams

* Ask "explain it from the premises," not "where did I go wrong."
  The second question only searches inside the frame you already share.
* Record the premise in the human's own words. A summary is a working tool;
  it is not the fixed point.
* Count your patches. Three fixes in one region is a structural signal, not bad luck.
* Do not write this class of failure as someone's mistake. Written as fault, it is not reusable.
  Written as structure, it applies to everyone you will ever work with.

# 2026-07-24 — The belief that had to be built before it could die

## Context

A payroll system needed per-group wage templates.
The group axis chosen was the **employee category** — full-time, part-time, and so on.

Payroll is a domain where a wrong value costs money and trust,
so the work ran in a director/implementer pair of two agents,
with independent verification on every phase.

## What happened

Four phases were designed, implemented, and shipped over two days:
a category master, an assignment history, admin screens, and a data migration.

Verification worked. It caught real defects in every round —
wiring gaps, an off-by-one on effective dates, a scope key wired to a constant.
All were fixed. The test suite ended green.

Then the human looked at the finished screen and named it:

> Pay is legally and fiscally divided by **wage type** —
> hourly, daily, monthly. Not by category.
> A full-time employee can be on daily wages.
> The category is just what a workplace calls people.

The axis was wrong. All four phases stood on it.

## What caught it

Not a test. Not a review. Not the agents.

The finished screen, in front of the human who runs the actual workplace.
The implementation had to exist before the belief it stood on could be seen.

Every test verified the design against itself.
The wiring tests proved values arrived where the design said they should —
and they did. The design said the wrong place.
No test can ask whether the axis is right.
That question does not live in the test layer.

## The part that stings

The refuting fact — *a full-time employee can be paid daily* —
was known by the human **on day one**. It was never contradicted.
It was simply never written where it could collide with the design.

The agents did not catch it either.
At one point the directing agent asked a leading question —
*"would one person in a category ever differ?"* —
which made the wrong axis more comfortable instead of testing it.

The human felt unease several times before the correction,
and had no coordinates to point at.
Unwritten beliefs give unease nothing to collide with.

## What made the discard cheap

Cost: four pull requests built on an axis that had to be re-cut.

But the discard was cheap, because the guards already existed:

* the wrong tables held no real production data
* every deploy had a named save point, and a database dump where data was touched
* so the wrong design could be dropped without any migration

Chapter 1 paid for this lesson.
Rollback being cheap is exactly what made the wrong design cheap to abandon —
its job had quietly moved up a layer.

## What changed

One rule: a design axis must be written down as a belief **before** building on it,
with its evidence and its death condition. One written line, before phase one:

```
Belief: wage conditions are grouped by employee category.
Evidence: (none could be written)
Dies if: two employees in one category need different wage types.
```

The evidence line would have been empty.
The death condition was already true on day one.
The belief would have died at the cost of reading it —
instead of at the cost of building it.

This case is the origin of Chapter 2: [Cheap Enough to Die](../CHEAP-DEATH.md).

## For other teams

* Before building on a grouping axis, write the belief with an evidence line
  and a death condition. If the evidence line stays empty, stop.
* A green suite tells you the design agrees with itself, not that the design is right.
* When a human feels repeated unease but cannot name it, ask one question:
  *is this a wrong value, or a wrong axis?* Axis unease never shows up in test output.
* Keep rollback cheap even when code quality is high —
  its real job is making wrong designs cheap to abandon.

# 2026-07-31 — Implementation is not delivery

> **One of three cases cut from the same flow.** Nothing here reached incident.
> See also: [unstated-premise](./2026-07-31-unstated-premise.md) ·
> [drift](./2026-07-31-drift.md)

## Context

A payroll settings screen in a workforce system. Values can be overridden per employee,
per wage type, or left to fall through to a workplace-wide baseline.

Nothing was at risk of damage here. The cost was different: a **dangerous feature was being
kept alive** because nobody believed a safer one existed.

## What happened

For weeks the human had been reluctant to remove an option that applied a change
retroactively across all past months — the most destructive setting on the screen.
The reason was never "I use it." The reason was:

> **不可塑性への不安**
> *Fear that it could not be undone.*

If a per-employee override could not be taken back, the retroactive option felt like
the only escape hatch.

Then the human named what they had actually been reaching for:

> 感覚的に「最初から」が欲しかったのは「初期値にする」だったのかも
> *What I wanted from "from the beginning" was probably "make it the baseline value."*

The two are not the same operation. One moves along time. The other moves down a layer.

The directing agent checked the code. **The layer operation was already implemented.**
It had a button on the same screen, a correct label, and tests protecting it.

```
Button exists        yes
Label correct        yes  ("clear — revert to inherited")
Tests protecting it  yes
Explanation of what "inherited" means, anywhere on screen   ★ none
```

The human — **the person who designed this system** — could not tell from the screen
that this was the feature they had been asking for.

> **コードベースで見ていないので画面に出ている情報だけだと知りようが無かった**
> *I had not looked at the codebase, so from the information on screen alone there was no way to know.*

## What caught it

Not a test. Not a review. **A design conversation that had drifted far enough to require
going back to first principles.**

While rebuilding the shared vocabulary, the agent read the code to answer a different
question, and noticed the feature already existed.

The mechanism worth naming is the one that was *missing*: the agent had reported
"implemented" for weeks. **That report was true and useless.**

```
The reporting side  reads code   → knows the feature is there
The receiving side  sees screens → does not
```

The agent had been treating *what it could see* as *what the human could see*.

## What made recovery cheap

Nothing had to be recovered. **No incident occurred.**

The cost was a design distortion carried for weeks: a destructive option kept alive
because its safe replacement was invisible. That cost was paid in caution, not in data.

The guard that mattered was ordinary: the human kept saying the option felt wrong
and refused to let it go unexamined.

## What changed

The report format changed.

```
before  "Implemented."
after   "The implementation exists. However, from the on-screen explanation alone a user
         cannot understand what it does, so intelligibility is not met."
```

Four axes now have to be named separately:

| Axis | Question | Machine-checkable |
|---|---|---|
| Reachability | can you get there | yes |
| Substance | does it actually work | yes |
| Visibility | does it enter the eye | partly |
| **Intelligibility** | **from screen information alone, can you tell what it does** | **no** |

Only the fourth cannot be tested. **Therefore whoever can read the code must not be the
one who judges it.**

## For other teams

* Before writing "implemented," ask whether that judgement used your ability to read code.
  If it did, the report is about you, not about the user.
* State which axis you reached. "Implemented" only ever covers reachability and substance.
* A correct label is not an explanation. `revert to inherited` is only meaningful to someone
  who already holds the layer model — which, in this case, existed nowhere in writing.
* When a user clings to a dangerous option, look for the safe operation they are actually
  reaching for. It may already exist, one screen away, unreadable.

> **画面から分からない機能は、使う人にとって存在していない。**
> *A feature that cannot be understood from the screen has not reached the user.*

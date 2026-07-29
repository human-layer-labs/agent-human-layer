# The Unrun Check

*Chapter 3 of the Agent Human Layer belief.*

*[BELIEF.md](./BELIEF.md) is the trunk, and remains the trunk.
This chapter extends it, as [Chapter 2](./CHEAP-DEATH.md) does. It is not a second trunk.*

---

## Chapter 2 held

Beliefs got written down. Written beliefs died on being read
instead of on being built. The wrong axis stopped being expensive.

## A third artifact was never examined

Chapter 1 governs **code**: make it cheap to restore.
Chapter 2 governs **beliefs**: make them cheap to kill.

Neither governs the **specification** — the document that says what to build,
and, critically, **the checks that decide whether the work is done**.

Once one agent writes the criteria another agent is judged by, that document
is no longer a message. It is an instrument with authority. And nothing in
AHL had ever asked whether the instrument works.

## The failure Chapter 1 cannot price

A defective check does not break anything.

It stops correct work. The implementer halts — correctly, by the rules —
and reports that it cannot satisfy the specification. There is no bad state.
Save points are irrelevant. There is nothing to restore, because nothing broke.

The cost is paid in round trips and in the human's confidence.
Neither has a snapshot.

And from where the human sits, a stop caused by a broken check looks
exactly like a stop caused by broken work. They cannot tell the two apart.
So the cost lands on the belief itself — the one thing this layer exists to protect.

Chapter 1 asks *can we undo it?* For this class the answer is yes, trivially,
and the answer does not help.

## An unrun check is not a check

It is a belief with the authority to stop work.

That is the whole chapter. Acceptance criteria feel like verification —
they are written in the language of commands and numbers — but until they have
been executed, they are exactly what Chapter 2 warned about: an assertion about
the world that has never been allowed to collide with the world.

Chapter 2 said an unwritten belief can only be refuted by building the software.
An unrun check is worse. It has been written, it looks tested, and it has been
handed the power to halt.

The refutation is available for the price of running it. It is almost always
one second. The reason it goes unrun is that a check reads as though it has
already been verified by the act of writing it down.

## Run it, or mark it unverified

The mechanism is one line:

> **Before handing over a specification, execute every check in it,
> and record the real output beside it.**

For a check whose target state does not exist yet, one question makes it
executable in advance:

> **"If the work were done perfectly, what exactly would this print?"**

If that string cannot be written, the check is not finished.

Three kinds, each with its own way of being wrong:

| Kind | Claims | Fails when |
|---|---|---|
| **invariant** | this must not change | the specification itself introduces the token — search your own document |
| **removal** | the old form is gone | it names a *shape* rather than the *old value*; a shape also matches the fix, and never goes quiet |
| **arrival** | the new form is present | it is written as a count nobody can measure in advance — name the files instead |

And one rule about instruments:

> **When a suite is the judge, the check must be the suite** — not a search that
> approximates it. A different instrument reports a different world.
> Both can be telling the truth; only one of them decides.

## The ratchet is the symptom

Chapter 1 holds that over-verification is not a virtue — it is what a team does
when it cannot cheaply undo things.

The same disease reaches the rulebook.

When a checklist grows after every incident and the incidents keep arriving,
the checklist is not the cure. Each new rule describes the shape of the last
failure; the next failure arrives in a shape it does not cover. A template that
grew forty percent in one pull request, while the defect rate inside that same
pull request stayed flat, is not getting safer. It is accumulating scar tissue.

Prefer a **step that executes** over a **rule to remember**.
A rule is a belief about future attention. A step is a fact.

## Stops must stay attributable

The stop condition is AHL's strongest mechanism. It only works while the human
can believe that a stop means the work was wrong.

Every stop caused by a broken check spends that. Not because the stop was wrong —
it was right — but because it was spent on the wrong thing.

So the count that matters is not how many stops occurred. It is
**how many of them were caused by the specification.** That number belongs in the
report, and it belongs to the author of the specification, not to the implementer
who stopped.

## The symmetry

Cheap rollback makes bold implementation possible.
Cheap death makes high belief possible.
A check that has been run makes a stop believable.

---

*Evidence: [cases/2026-07-29-the-check-that-could-not-pass.md](./cases/2026-07-29-the-check-that-could-not-pass.md)*

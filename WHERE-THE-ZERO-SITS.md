# Where the Zero Sits

*Chapter 4 of the Agent Human Layer belief.*

*[BELIEF.md](./BELIEF.md) is the trunk, and remains the trunk.
This chapter extends it, as [Chapter 2](./CHEAP-DEATH.md) and [Chapter 3](./UNRUN-CHECKS.md) do.
It is not a second trunk.*

---

## Chapters 1 to 3 held

Rollback became cheap enough to use. Beliefs became cheap enough to die. Checks
started being run before they were handed to anyone.

Each of those is a way of **not losing**.

## What none of them says

A project can satisfy all three and never arrive.

Every route explained. Every save point named. Every belief written. Every check
executed. Every stop correct. And nothing shipped.

Nothing in this layer would notice.

The idea that the point is to *move* is present in this repository — but only ever
as a closing line, at the end of a document about something else:

* the trunk: *if it works, the work should be completed quickly*
* Chapter 2, final line: *cheap rollback makes bold implementation possible*
* the adoption guide, final line: *its purpose is to let agents act boldly*

Four sentences, in four places, each the last thing said before the document ends.
Never a home. So a reader meets three documents about restraint and one throwaway
line each about why restraint was worth it.

This chapter is that line, given a home.

## Two zeros

Consider how the rules are usually held in a person's head:

> Do not be wrong. Do not drift. Report every discrepancy.

Every one of those is paid to avoid going **below** zero. Satisfy all of them
perfectly and the score is zero — nothing broke. Miss one and the score is
negative. The ceiling is zero.

Now the same care, stated from the other side:

> Overshooting is fine. Breaking it is fine. If something looks off, ask.

Here the floor is held, so the ceiling is open.

Same diligence. Opposite sign.

> **When the worst case is zero, you can move.
> When the best case is zero, you cannot.**

This is not a claim about comfort. It is a claim about where a system puts its
zero, and therefore about whether anyone inside it can do more than avoid loss.

Chapter 1 was never really about restoring broken code. It was about **moving the
zero from the ceiling to the floor**.

## This also explains the ratchet

Chapter 3 observed that a checklist which grows after every incident, while the
incidents keep arriving, is a symptom rather than a cure. It said the symptom was
an inability to undo things cheaply.

That was not deep enough.

> **While the best outcome of a check is "nothing was wrong,"
> there is no reason ever to stop adding checks.**

Adding a rule is what you do when you are managing anxiety. Running the check is
what you do when you are managing outcomes. The second takes a second and is
available the whole time. Under a ceiling of zero, the first still feels safer.

## The four leaks

A floor is not a mood. It is held up by four things not leaking — and every one of
them is **information that already existed, failing to become shared**:

| Leak | What is lost |
|---|---|
| Punishing a failure | the source stops reporting — the most expensive leak, because it closes the other three |
| Seeing an error and not naming it | held, not given |
| Making an error and not admitting it | held, and denied |
| Not recording it — **including the feeling that had no name yet** | given, and evaporated |

The last one carries more than it looks like. Twice now in [cases/](./cases/), the
signal that caught a defect was an unnamed human feeling: *unease with nothing to
point at*, and *I didn't really get it*. Neither was a finding. Both were data.

And the leak that matters most for an agent is the first one. An agent that is
punished for surfacing an awkward detail will surface fewer of them, and the
detail it stops surfacing is exactly the one no check can see. In one recorded
case, a broken acceptance check silently deformed correct code, and the only thing
that caught it was a single sentence in an implementer's report — volunteered,
not required, and worth more than every check written that day.

## Belief is the part that scales

The open question is how humans stay in control of agents that implement faster
than humans can read.

Gates do not answer it. Gates grow with output; reading does not. What scales is
knowing **which** output needs reading — and that is trust, calibrated. Calibration
is only possible while the four leaks stay closed.

So belief is not the soft part of this layer. It is the only part that scales.

## The line

> **Belief is not the goal. It is where the zero sits.**

Belief is not asked for as a virtue, and it is not the reward for good behaviour.
It is load-bearing: it is what puts the floor under the work, and the floor is what
makes the goal something a person can actually spend effort reaching instead of
merely avoiding failure at.

A layer that never arrives is not a safe layer. It is an expensive way not to
arrive.

## The symmetry

Cheap rollback makes bold implementation possible.
Cheap death makes high belief possible.
A check that has been run makes a stop believable.
A floor that holds is what makes a goal worth aiming at.

---

*Evidence: [cases/](./cases/) — in particular the two incidents caught by a human
feeling that had no name yet.*

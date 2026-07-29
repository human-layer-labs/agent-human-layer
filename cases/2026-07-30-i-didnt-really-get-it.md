# 2026-07-30 — "I didn't really get it"

## Context

A terminology cleanup had shipped to the test environment. Among other things it renamed the
concept of *the one approved device whose failure a recovery code is meant to cover* — a store
tablet that displays a clock-in QR code. Several devices can be approved; exactly one holds
that role. The recovery code is the spare key for it.

The owner ran the acceptance check on real hardware.

## What happened

The entire report was a screenshot and one sentence:

> I didn't really get it.

The directing agent read that as a readability problem and proposed readability fixes: mark
which row holds the role, stop showing raw internal identifiers, hide a button for an action
already performed. All of them were true findings. All of them were cosmetic.

The owner pushed back twice. First:

> Being able to name the devices might be really important.
> Back-office tablet. The laptop everyone looks at.
> Showing the IP and the browser string is not enough to tell them apart —
> I genuinely could not tell.

Then, unprompted, they explained what they had assumed the feature was *for*:

> The recovery code only works when **the device we designated** is down.
> The other approved ones could be the manager's own phone, or something approved
> temporarily because of a glitch.

That sentence was the defect report.

The agent went and read the gate. The gate matched the owner's model exactly: it looks at the
designated device only, and refuses recovery while that one is alive. Nothing wrong there.

But *designated* was being assigned by a silent fallback. Whenever the role was vacant, the
next read of it — from the admin screen, from the QR page, from a background request — would
adopt whichever approved device had been seen most recently, and write it in.

And the role became vacant through the most ordinary operation available: revoking the broken
tablet. So the sequence was:

1. the tablet breaks; the owner revokes it
2. the role is vacated
3. the next read of it, from anywhere, silently installs the most recently active device
4. if that was the manager's personal phone, the phone now holds the role
5. from then on the recovery code only works while the phone is offline, and using it
   suspends the phone

No record. No notification. No human in the loop at any point.

## What caught it

Not a test. Not a review. Not the agent reading the diff.

The agent had read that exact function **twice that day** while writing a migration, and had
not seen it. It was reading for what the migration needed, and the fallback was not in the way.

What caught it was a person who could not answer a question while looking at a finished
screen, and who kept saying so instead of moving on.

The screen could not show which device held the role. The agent assumed that was a display
gap. It was not.

> **The screen could not answer the question because nothing in the system had ever decided.**

[Chapter 2](../CHEAP-DEATH.md) holds that an unwritten belief can only be refuted by built
software. This is that refutation arriving in its weakest possible form: four words, from
someone who could not yet say what was wrong. It still carried the whole defect.

## The part that stings

The agent's first three proposals were all improvements to the *explanation*: a badge, a
clearer name, a hidden stale button. Every one of them would have shipped. Every one of them
would have made the screen describe the wrong state more clearly.

"I don't understand this screen" arrives looking like a request for polish. Polish is the one
response that cannot fail loudly — the screen does get better, the human does stop asking, and
the defect stays.

## A second finding, from the fix

Removing the silent fallback leaves the role legitimately empty. Every gate still behaves
correctly with an empty role: nobody holds it, so the recovery code is available to anyone —
which is right, because there is no device to protect.

The agent wrote that up as *correct behaviour* and moved on. The owner answered:

> Removing it is right. But the system is only normal when the role **is** set.

That distinction had no name in this project. A state can satisfy every invariant and still be
a state the system must not sit in quietly. The removal was correct and incomplete: it needed
to be paired with something that makes the hole visible until a human fills it — a warning
carried at the top of every screen, which disappears when the role is assigned, and which
cannot be dismissed by acknowledging it.

Without that pairing, the fix would have traded a silent wrong answer for a silent missing one.

## What made recovery cheap

The defect was found before it ever mattered: the test environment holds no real data, and the
deployment it rode in on had a folder snapshot and a database dump taken before the swap. The
wrong design could be discarded at the cost of one more pull request.

But the thing that made it *findable* was not a guard. It was that the owner ran the check on
real hardware and reported an unflattering, unspecific result instead of a clean pass.

## What changed

Two rules.

**1. "I don't understand this screen" is a defect report until proven otherwise.**
Do not answer it with better labels. Ask what question the screen is failing to answer, then
check whether the system is able to answer it at all. A screen cannot display a decision that
was never made.

**2. Correct is not the same as normal.**
When a fix removes a behaviour, name the state it leaves behind and decide whether the system
may rest there. If not, the removal is only half the fix; the other half is a mechanism that
surfaces the state until a human resolves it — on a screen people actually open, not the
settings page they configured once.

## For other teams

* **Unnamed confusion is a sensor the agent does not have.** The agent can read every line and
  still not notice what is missing, because it reads for what it came to do. The human cannot
  read the code and notices anyway. Neither half finds this alone.
* **When a screen cannot show X, ask whether the system knows X** before improving the screen.
* **A silent fallback that fills a security-relevant role is worse than leaving it empty.**
  Empty is visible. Filled-by-accident looks exactly like filled-on-purpose.
* **Do not auto-select even when only one candidate remains.** The last device standing may be
  precisely the one that must not hold the role.
* Having read the code recently is not immunity. Read once for the task, and the rest of the
  function becomes scenery.

# 2026-08-05 — The snapshot that was not known-good

> **A fire drill.** Nothing broke by accident. The system was broken on purpose,
> restored twice, and timed. The drill found a defect in the recovery path itself —
> before that path was ever needed.

## Context

A workforce/payroll plugin running on a staging site that shares a host with production.
Deployment is over SSH. Before every deploy, a `.tgz` snapshot of the plugin folder is written
to a backup directory.

The README of this repository already says:

> Sometimes the most trustworthy recovery is not a clever Git operation.
> Sometimes it is replacing the target folder with the last known-good snapshot.

That was believed. It had never been executed. In months of deploys, **no rollback had ever
been needed** — which reads equally well as "it was safe" and as "we never checked."

The human named it:

> **これは避難訓練みたいなものですね**
> *This is like a fire drill.*

## What happened

The drill was designed by the human, not the agent:

```
instruct → implement → accept → deploy → human checks the live site
→ human finds a fatal error → reports it → the agent restores on the spot → measure
```

Two constraints made it sharper. The human chose both:

* **Do not tell me which screen will break.** The human was the detector, not a spectator.
* **Round two: hand the runbook to a different agent and let it restore.**
  What that measures is not speed. It is whether the document works in someone else's hands.

The agent wrote the restore runbook *first*, then broke the system: one call to an undefined
function, inserted into one admin screen. Not a syntax error — a syntax error would have been
caught before deploy, and the whole point was a failure that survives review and appears only
when a human opens the page.

**Then, while preparing the drill, the agent nearly used the wrong snapshot.**

The handoff document — written by the same agent the night before — said the latest snapshot
could be used for the restore demo. A size difference of 2,116 bytes did not fit. Extracting
both and diffing them showed why:

```
latest snapshot   = the state BEFORE the most recent deploy
                    (three files different — exactly the fix deployed the night before)
```

Snapshots are taken immediately *before* a deploy. So **every snapshot holds the state in which
that deploy has not happened yet.** Restoring "the latest snapshot" does not return you to now.
It silently un-does the most recent deploy.

Worse, in this case the regression would not have shown a symptom. The deploy being un-done had
changed migration gates from *version-keyed* to *permanently marked*. The stored markers still
held the old version string, so the old code's gate would have matched and skipped the migrations.
Nothing would look wrong. **The original defect would have returned on the next version bump.**

## What caught it

Not a test. **A number that did not fit**, and the refusal to explain it away.

The two archives were 2,116 bytes apart on a system where, by every account, nothing had changed
since the last deploy. That is a small enough discrepancy to round off. Rounding it off would have
made the drill itself the incident: a rehearsal that quietly reverted a real fix.

A second guard fired during the same session, in the other direction. The script that inserted the
fatal error compared line counts before and after, and aborted:

```
lines after: 3251 (want )
expr: not a decimal number: '    3248'
ABORT: line count unexpected
```

The platform's `wc -l` emits leading whitespace; `expr` refused it. **The check failed for a
reason unrelated to what it was checking — and still did its job**, because it stopped *before*
the file was replaced. A check earns its keep not by working, but by refusing to let a wrong
state move forward.

## What made recovery cheap

Measured, both rounds:

```
round 1  directing agent restores, holding the runbook
         time the human was stuck (their report → their "it's fixed")   1 min 4 s
         server-side restore itself                                     under 1 s

round 2  a different agent, given ONLY the runbook and "it is broken"
         restored successfully                                          under 1 s
```

The human's clock is the real one. The server-side second is not the number that matters; the
minute the human sat in front of a broken screen is.

An unexpected witness confirmed the start time. WordPress had written
`recovery_mode_email_last_sent` at the moment the human opened the broken page — an independent
clock nobody planted.

Three things had been prepared before anything was broken, and all three were used:

* a snapshot taken **immediately before breaking**, verified byte-for-byte against the live tree
* the restore runbook, written first, with the abort conditions listed above the destructive step
* a fallback ladder written down in advance — second-newest snapshot, then rebuild from the
  source repository

## What changed

**1. "Latest" is no longer a valid way to choose a snapshot.**

The runbook now makes the choice explicit before anything is extracted:

| Goal | Restore target |
|---|---|
| Undo the most recent deploy | the snapshot taken just before it — **knowing that deploy's changes will be gone** |
| Return to the current correct state | a snapshot taken **before the breakage** — if none exists, this path does not work |

A snapshot's own version string is not enough to tell these apart. Two snapshots can carry the
same version and different contents.

**2. Proof of restoration is a diff, not a version number.**

The drill broke the system by editing files directly, so the version never moved. Before and after
the restore, it read the same. A version number is a *delivery mark* — evidence something arrived,
never evidence something returned. The runbook's primary check is now: extract the snapshot again,
`diff -r` it against the live tree, expect nothing.

**3. "Code-only" changes still write to the database.**

Restoring a `.tgz` restores code. It does not restore rows. The drill touched nothing but one
source file, and the platform still wrote two option rows on its own — including a live recovery
key that, if clicked, would have disabled the plugin through a database flag **that no code
restore can clear**.

So the honest sentence is never "no database impact." It is: *no business data changed.*

**4. The runbook gained the thing the second agent asked for.**

Handed only the document, the second agent chose the correct snapshot — and then reported the gap:
there was guidance on *how* to choose, but no command to list the candidates. The backup directory
held 230 archives. The document taught judgement and withheld the material for it.

## For other teams

* **Run the drill before you need it.** A recovery path nobody has walked is a belief, not a capability.
  This one had been trusted for months and had a defect in its first step.
* **Time the human, not the machine.** The restore took under a second. The outage was a minute.
  The gap is discovery, reporting, and hand-off — which is where real incidents live too.
* **Let the human be the detector.** If they know which screen breaks, you have measured your own
  scripts. If they do not, you have measured the loop.
* **Run it twice, with a stranger.** The second round is the only one that tests the document.
  Whoever wrote it will unconsciously supply the missing steps from memory.
* **Snapshots taken before a deploy are not "known-good now."** Name what each one means, or you
  will reach for the newest one during the exact minutes you are least able to think.
* **Ask what the restore does *not* cover, in writing, before you rely on it.** Ours restored code
  and left database rows behind — including one that could re-break the system after a successful
  restore.
* **A check that fails for the wrong reason is still working**, as long as it fails *before* the
  irreversible step. Put the abort conditions above the swap, not after it.
* **Keep the discrepancy you cannot explain.** Two thousand bytes was the entire warning.

> **最短で動く。違和感を消さない。間違っていたら安く戻る。**
> *Move by the shortest path. Do not smooth away what feels off. If it was wrong, come back cheaply.*
>
> The third clause was the one nobody had tested.

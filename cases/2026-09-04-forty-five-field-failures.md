# 2026-09-04 — Forty-five field failures

This is a compact field collection rather than a victory lap.

The incidents came from sustained agent-driven development across a spreadsheet-native product,
a plugin product, recovery drills, CI, handoffs, and AHL's own tests. They include failures by
agents, failures by humans, failures by platform constraints, and failures created by the safety
process itself. Some were expensive, some were near misses, some were caught before damage, and a
few are design-boundary findings rather than production defects.

The details are intentionally masked. No customer names, hostnames, credentials, private repository
names, or personal identifiers are included. Raw evidence remains with the reporter.

The point of the collection is not that AHL worked. The point is that reality corrected us forty-five
times.

**Collection provenance:** incidents reported from the operator's own projects and session history;
prose structured by an agent; the complete masked draft was read and explicitly approved by the
human for publication on 2026-09-04. Publication does not promote any claim's evidence state.

---

## 01 — The Platform Wins

A spreadsheet-native UI needed three-way selection, instant feedback, visible comparison values,
and predictable focus. The design was coherent. The platform simply did not expose every mechanism
needed to implement it cleanly: native click controls were binary, formatting could not change every
visual property, and focus after a dropdown selection was not under application control.

> **Claim:** platform mechanics forced an approved UI design to change even though the product intent did not
> - state: DECLARED
> - evidence: development session transcript and live-sheet experiments, held by the reporter
> - scope: one spreadsheet-native product UI
> - provenance: observed by the human and implementing agents; prose structured by an agent
> - observed_at: 2026-09-03

**Lesson:** Reality can veto Authority. A ratified design is not a mechanism.

---

## 02 — A Requirement Without a Mechanism

The requested interaction was: three peer choices, one click, immediate response, exactly one active,
and no dropdown. Each requirement was reasonable in isolation. Together they described a control the
host platform did not have.

> **Claim:** the combined requirement set had no native mechanism in the chosen host
> - state: DECLARED
> - evidence: control experiments and implementation attempts, held by the reporter
> - scope: the host's native UI controls used in this project
> - provenance: observed during implementation by the human and agents
> - observed_at: 2026-09-03

**Lesson:** Authority can specify an outcome that Reality cannot instantiate. Detect the missing
mechanism before polishing the specification around it.

---

## 03 — Mechanically Correct, Humanly Broken

Three checkboxes were made mutually exclusive by an edit trigger. The resulting state was logically
correct after the trigger completed. To the human, however, a click looked like a stall followed by a
late correction. Correctness arrived after trust had already left.

> **Claim:** a mechanically correct interaction was rejected because its visible latency made the control feel broken
> - state: DECLARED
> - evidence: live interaction timing and human evaluation, held by the reporter
> - scope: one goal-selection interaction
> - provenance: observed directly by the human; timings observed by implementing agents
> - observed_at: 2026-09-03

**Lesson:** Correct result is not sufficient evidence of a trustworthy human-facing outcome.

---

## 04 — Authority Must Survive the Session

A product rule changed after platform testing. The old rule had been written down; the new ruling
initially lived only in conversation. A fresh agent reading the durable record would have restored the
old rule correctly. The team moved the new ruling into a durable issue before continuing.

> **Claim:** an updated human ruling was unsafe to hand off until it was persisted outside the chat session
> - state: DECLARED
> - evidence: session transcript and issue history, held by the reporter
> - scope: one multi-agent product-design handoff
> - provenance: observed by the human and agents
> - observed_at: 2026-09-03

**Lesson:** Authority that cannot survive the session is temporary context, not durable authority.

---

## 05 — Stale Authority Can Be Perfectly Obeyed

An earlier specification explicitly prohibited the interaction later selected by the human. After
live experiments changed the ruling, following the earlier document word-for-word would have been
obedient and wrong.

> **Claim:** a previously ratified requirement became stale while remaining internally clear and enforceable
> - state: DECLARED
> - evidence: versioned issue text and later human ruling, held by the reporter
> - scope: one goal-selection requirement
> - provenance: observed during the same design session
> - observed_at: 2026-09-03

**Lesson:** The question is not only “did the agent obey?” but “did the agent obey the current
Authority?”

---

## 06 — Summary Is Not Authority

Long work crossed agent and session boundaries. Handoffs necessarily compressed context. The team
found that a summary could preserve the headline while losing the exact envelope, exceptions, or the
fact that a later ruling superseded an earlier one.

> **Claim:** handoff summaries were insufficient by themselves to establish the full current authority envelope
> - state: DECLARED
> - evidence: repeated multi-agent handoffs and corrections, held by the reporter
> - scope: the reporter's multi-agent development workflow
> - provenance: observed by the human across multiple sessions; prose structured by an agent
> - observed_at: 2026-08-01/2026-09-04

**Lesson:** A summary may carry Authority; it must not silently enlarge or replace the source of
Authority.

---

## 07 — Human Can Move the Goalposts Legitimately

The human first ratified “no dropdown,” then reversed that decision after the platform demonstrated
that the desired native interaction could not be made stable enough. The goal did not drift; the
means changed because new Reality arrived.

> **Claim:** the human explicitly reversed an earlier UI ruling after new platform evidence
> - state: DECLARED
> - evidence: session transcript, held by the reporter
> - scope: one product interaction
> - provenance: human ruling observed by the agents in-session
> - observed_at: 2026-09-03

**Lesson:** Human consistency is not the goal. Explicitly updated Authority is allowed to kill its
predecessor.

---

## 08 — Human Can Point at the Wrong Mountain

In earlier development work, the human could give a concrete target and the agent could execute it
with high precision, only for the human to later realize the target itself was wrong. Precision did
not rescue a false premise.

> **Claim:** at least one implementation path was technically faithful to a human-directed target that was later abandoned as the wrong target
> - state: DECLARED
> - evidence: project session history, held by the reporter
> - scope: the reporter's agent-driven development work
> - provenance: reported by the human; prose structured by an agent
> - observed_at: 2026-06/2026-09

**Lesson:** Human Authority is necessary for action, but it is not proof that the chosen target serves
the Goal.

---

## 09 — Green Tests on the Wrong World

A multi-phase implementation was built around the wrong domain axis. Tests were green because they
verified the implementation against the same mistaken model that produced it.

> **Claim:** a green suite coexisted with a wrong domain model across multiple implementation phases
> - state: OBSERVED
> - evidence: existing public case [`2026-07-24-the-wrong-axis.md`](./2026-07-24-the-wrong-axis.md) in this repository
> - scope: the incident documented by that case
> - provenance: repository evidence already published and human-reviewed
> - observed_at: 2026-07-24

**Lesson:** Verification can prove internal consistency while the model of the world is wrong.

---

## 10 — The Fixture Was Wrong

An AHL behavior test was intended to measure a fresh agent under a specific layer and authority
setup. The workspace did not actually match the assumed fixture. The test result therefore said less
about the agent than about the test harness.

> **Claim:** an agent-behavior trial was invalidated by a fixture/environment mismatch discovered during the trial
> - state: DECLARED
> - evidence: AHL test-session transcript, held by the reporter
> - scope: one internal AHL evaluation
> - provenance: observed by the human and test agents
> - observed_at: 2026-08

**Lesson:** Before grading an agent, verify the world in which the agent is being graded.

---

## 11 — The Layer You Thought Was Active Wasn't

A test was run under the belief that the newest agent layer was controlling the session. Inspection
showed that an older project-local layer was the one actually active.

> **Claim:** one internal AHL test initially attributed behavior to the wrong active instruction layer
> - state: DECLARED
> - evidence: test-session inspection and transcript, held by the reporter
> - scope: one internal AHL evaluation environment
> - provenance: observed by the human and inspecting agent
> - observed_at: 2026-08

**Lesson:** Mechanism identity is a Reality claim. “Installed” and “active” are different facts.

---

## 12 — Bootstrap Instructions That Never Arrived

A control path assumed that host/bootstrap instructions would reach the executing agent. A test found
that instructions believed to be upstream of the agent were absent from the agent's effective context.

> **Claim:** an internal test found a gap between instructions believed to be supplied and instructions actually available to the executing agent
> - state: DECLARED
> - evidence: AHL test-session transcript, held by the reporter
> - scope: one test harness and agent bootstrap path
> - provenance: observed during the internal trial
> - observed_at: 2026-08

**Lesson:** “Sent” is not delivery proof. Effective context is observable state.

---

## 13 — Silent Data Loss Behind Green Tests

A persisted field was silently erased on save while the suite remained green. A later UI feature, not
a test, exposed the missing data.

> **Claim:** a save path erased a persisted field while the existing tests continued to pass
> - state: OBSERVED
> - evidence: existing public case [`2026-07-22-silent-field-erasure.md`](./2026-07-22-silent-field-erasure.md) in this repository
> - scope: the incident documented by that case
> - provenance: repository evidence already published and human-reviewed
> - observed_at: 2026-07-22

**Lesson:** Coverage is not evidence that the suite observes the data you care about.

---

## 14 — A Plausible Snapshot Is Not a Save Point

A rollback path had been trusted for months. A deliberate drill showed that the newest snapshot was
not necessarily the known-good state the operator meant to restore.

> **Claim:** a recovery drill disproved a long-held assumption about which snapshot represented a safe return point
> - state: OBSERVED
> - evidence: existing public case [`2026-08-05-the-snapshot-that-was-not-known-good.md`](./2026-08-05-the-snapshot-that-was-not-known-good.md)
> - scope: the recovery mechanism documented by that case
> - provenance: repository evidence already published and human-reviewed
> - observed_at: 2026-08-05

**Lesson:** A snapshot becomes a Save Point only when the return semantics are known, not when the
file exists.

---

## 15 — Rollback Can Be Irrelevant

The team repeatedly encountered a harder category of failure: the implementation can be perfectly
restorable while the premise that produced it remains wrong. Returning to yesterday merely returns
to yesterday's belief.

> **Claim:** prior incidents showed that restoring code state would not by itself correct a false premise or wrong domain model
> - state: DECLARED
> - evidence: the [wrong-axis](./2026-07-24-the-wrong-axis.md) and [faithful-to-a-false-premise](./2026-08-04-faithful-to-a-false-premise.md) cases already in this repository
> - scope: conceptual recovery boundary evidenced by those incidents
> - provenance: derived from published cases; human-approved for this collection
> - observed_at: 2026-07/2026-08

**Lesson:** Rollback restores state. It does not generate truth.

---

## 16 — Rollback Restores State, Not Consequences

During recovery design, the team separated reversible repository state from external side effects.
A local restore can undo files and data snapshots; it cannot unsend a real message or retract every
external effect already observed by another system.

> **Claim:** the recovery design had to distinguish reversible local state from external irreversible effects
> - state: UNEVALUATED
> - evidence: AHL design discussion and threat-model notes, held by the reporter
> - scope: recovery semantics, not a claim that a real irreversible incident occurred
> - provenance: derived during live design review; human-reviewed
> - observed_at: 2026-08

**Lesson:** Recovery law belongs to the action's blast radius, not to the agent's intention.

---

## 17 — Cheap Rollback Changed the Failure

A layout rebuild failed because one API method did not exist on the builder being used. The rebuild
stopped, the cheap rollback path restored protected state, and the repair collapsed to a one-line
method correction plus one rebuild.

> **Claim:** a failed rebuild caused no stored-data loss and was recoverable with a one-line fix because rollback was already in place
> - state: DECLARED
> - evidence: rebuild logs, source diff, and data checks, held by the reporter
> - scope: one spreadsheet-layout rebuild
> - provenance: observed by implementing and supervising agents; human witnessed the incident
> - observed_at: 2026-09-03

**Lesson:** Cheap rollback does not prevent failure. It changes the price of failure.

---

## 18 — The Verifier Can Be Wrong

A verification script tried to extract functions from source. Its scanner mishandled an apostrophe
inside a comment, swallowed neighboring functions, and reported that an unchanged function had
changed.

> **Claim:** verification tooling produced a false alarm because its own parser was defective
> - state: DECLARED
> - evidence: verifier source, corrected scanner, and before/after results, held by the reporter
> - scope: one internal source verifier
> - provenance: observed and diagnosed by the supervising agent; reviewed by the human
> - observed_at: 2026-09-04

**Lesson:** A verifier is another mechanism. Until tested, it is another belief.

---

## 19 — Verify the Verification

After the verifier bug, the team added negative controls: every rule had to fail against the unchanged
baseline before its pass against the modified source counted as evidence.

> **Claim:** negative controls exposed useless or false-pass verification rules that ordinary green output could not distinguish
> - state: DECLARED
> - evidence: verifier runs with baseline negative controls, held by the reporter
> - scope: one source-verification workflow
> - provenance: observed by the supervising agent; human-reviewed
> - observed_at: 2026-09-04

**Lesson:** A PASS does not prove that the check was capable of failing.

---

## 20 — An Unrun Check Is Still a Belief

A pull request stopped repeatedly on checks that had been specified but not run before handoff,
including one whose acceptance condition could not pass as written.

> **Claim:** unrun acceptance checks created repeated stops despite no product breakage
> - state: OBSERVED
> - evidence: existing public case [`2026-07-29-the-check-that-could-not-pass.md`](./2026-07-29-the-check-that-could-not-pass.md)
> - scope: the incident documented by that case
> - provenance: repository evidence already published and human-reviewed
> - observed_at: 2026-07-29

**Lesson:** An unrun check is not a check. It is a belief with the authority to stop work.

---

## 21 — Verification Became the Work

During rapid UI iteration, every small visual change triggered proposals to re-run source-law,
calculation, persistence, round-trip, and data-integrity checks. The assurance loop became more
expensive than the UI work it was protecting. The human explicitly deferred full acceptance until
the design stopped moving.

> **Claim:** repeated full verification during active UI iteration materially slowed product progress and increased agent cost
> - state: DECLARED
> - evidence: session transcript and repeated verification reports, held by the reporter
> - scope: one product's UI-construction phase
> - provenance: observed directly by the human across multiple iterations
> - observed_at: 2026-09-03

**Lesson:** Assurance needs a budget and a phase boundary.

---

## 22 — Correctness Can Be Too Expensive

Each extra proof was locally reasonable. Taken together, “one more check” was pushing the product away
from its delivery goal. The process had optimized confidence past the point where confidence was
helping the project.

> **Claim:** the human changed the development process because the accumulated cost of correctness checks had become a delivery risk
> - state: DECLARED
> - evidence: explicit process ruling in the session transcript, held by the reporter
> - scope: one product-development workflow
> - provenance: human ruling observed by the agents
> - observed_at: 2026-09-03

**Lesson:** Belief is not the goal. It is what makes the goal affordable.

---

## 23 — The Guard Became Stale

Human-approved builder changes retired an old UI mechanism. Static guards continued to require the
retired builder names and formulas. The guards were once useful; after the architecture changed they
became false blockers.

> **Claim:** static guards failed because they encoded an intentionally retired implementation rather than a still-current invariant
> - state: DECLARED
> - evidence: guard failures and approved builder changes, held by the reporter
> - scope: one spreadsheet product's static guard suite
> - provenance: observed by implementing and supervising agents
> - observed_at: 2026-09-03/2026-09-04

**Lesson:** Proof expires when the mechanism it describes is deliberately replaced.

---

## 24 — Over-Conservative Safety Can Kill Delegation

In an AHL trial, a trivial typo-fix task stalled because the agent asked the human to identify the
word instead of performing the bounded repair the scenario was designed to test. The safe behavior
was not dangerous, but it defeated the purpose of delegation.

> **Claim:** an internal agent trial produced an unnecessary confirmation on a bounded low-risk edit, causing the scenario to fail its delegation goal
> - state: DECLARED
> - evidence: AHL trial transcript, held by the reporter
> - scope: one internal low-risk edit scenario
> - provenance: observed directly by the human
> - observed_at: 2026-08

**Lesson:** Safety that requires the human to perform the delegated work is not delegation.

---

## 25 — One More Review

After requirements had been ratified, agents repeatedly found one more design question, one more
review pass, or one more verification worth doing. Each was defensible. The accumulated round trips
became a primary cost of the project.

> **Claim:** repeated non-blocking review cycles became a material contributor to schedule and model-usage cost
> - state: DECLARED
> - evidence: session history and explicit human process correction, held by the reporter
> - scope: one multi-agent product project
> - provenance: observed by the human; structured by an agent
> - observed_at: 2026-08/2026-09

**Lesson:** Locally rational caution can become globally irrational.

---

## 26 — Investigation Without Decision Value

An unsolicited spreadsheet modal and transient checkbox states appeared without a reproducible data
mutation. Agents could keep investigating provenance. The human stopped the investigation because it
was not reproducible, no data damage was observed, and the answer would not change the immediate
design decision.

> **Claim:** a non-reproducible UI anomaly consumed investigation time without producing decision-relevant evidence
> - state: DECLARED
> - evidence: screenshots, session transcript, and bounded data checks, held by the reporter
> - scope: one spreadsheet UI anomaly
> - provenance: observed by the human and agents
> - observed_at: 2026-09-03

**Lesson:** Unknown cause is not automatically an open blocker.

---

## 27 — Agent Invented a Rule

While defining a percentage input, an agent moved toward imposing a range/validation rule that the
human-approved contract had never stated. The rule looked sensible. That did not make it authorized.

> **Claim:** an implementation discussion introduced a plausible validation constraint that was absent from the ratified input contract
> - state: DECLARED
> - evidence: session transcript, held by the reporter
> - scope: one percentage input contract
> - provenance: observed in-session by the human
> - observed_at: 2026-09-03

**Lesson:** Reasonable is not authorized.

---

## 28 — Silent Switch Is a Mutation

When a detailed cost source became available, automatically switching from the human's current rough
source looked helpful. It also changed the meaning of the calculation without a human action. The
design was changed so the new source could appear without stealing active state.

> **Claim:** an automatic source switch would have changed the active calculation basis without explicit human selection
> - state: DECLARED
> - evidence: source-law design and transition tests, held by the reporter
> - scope: one category-level source selector
> - provenance: identified during implementation review; human ratified the no-silent-switch rule
> - observed_at: 2026-09-03

**Lesson:** Automation that changes meaning is a mutation, even when it is convenient.

---

## 29 — Transient State Can Steal Authority

A source-selection formula initially risked keying directly on candidate count. During the transition
from one available source to two, the count could change before the visible switch was restored. The
formula therefore needed a durable pin so the old choice survived the transient state.

> **Claim:** a formula design based only on current candidate count could have changed active source during a valid one-to-two transition
> - state: DECLARED
> - evidence: implementation design review and transition scenarios, held by the reporter
> - scope: one formula-native source-selection mechanism
> - provenance: identified by the supervising agent and reviewed by the human
> - observed_at: 2026-09-03

**Lesson:** The transition is part of Reality, not just the settled state before and after it.

---

## 30 — Hidden Values Were Still Human Data

To make only one profit input look active, inactive values were rendered white-on-white. The data was
preserved internally, but the human rejected the design because the values were useful precisely for
visible comparison across “what if” choices.

> **Claim:** hiding inactive but preserved values broke the human's comparison workflow even though persistence remained correct
> - state: DECLARED
> - evidence: live UI review and screenshots, held by the reporter
> - scope: one three-value profit-input band
> - provenance: observed directly by the human
> - observed_at: 2026-09-03

**Lesson:** Preserved data and available information are not the same thing.

---

## 31 — A UI Can Lie

A discussion proposed an explicit “save changes” button for an editing surface whose underlying host
already saved cell edits automatically. The button would have increased reassurance by implying a
false boundary: that changes were not saved until the button was pressed. The idea was rejected.

> **Claim:** the team rejected a familiar save control because it would have misrepresented the system's actual save semantics
> - state: DECLARED
> - evidence: design-session transcript, held by the reporter
> - scope: one spreadsheet-native editing surface
> - provenance: human ruling observed in-session
> - observed_at: 2026-09-04

**Lesson:** Human-facing semantics must describe actual system behavior.

---

## 32 — Familiar UI Can Be More Dangerous Than Strange UI

The save-button discussion exposed a broader trap. Familiar controls carry strong expectations. A
misleading familiar control can create more confident misunderstanding than an unfamiliar but honest
interaction.

> **Claim:** a conventional control was deliberately omitted because its conventional meaning conflicted with the actual state model
> - state: DECLARED
> - evidence: the same design ruling as Case 31, held by the reporter
> - scope: one editing surface; broader lesson is interpretive
> - provenance: derived from the human's design ruling and approved for this collection
> - observed_at: 2026-09-04

**Lesson:** Conventional UX is not automatically truthful UX.

---

## 33 — Duplicate Implementations Drift

Two product surfaces were meant to share one calculation model. They had separate builders for cost,
goal choice, and answers. The surfaces drifted until the Core implementation had to be rebuilt from
the already-accepted shared builders and the duplicate calculators deleted.

> **Claim:** duplicate UI builders for the same product facts produced divergent calculation surfaces that later required consolidation
> - state: DECLARED
> - evidence: source diffs and implementation report, held by the reporter
> - scope: two surfaces of one spreadsheet product
> - provenance: observed by the implementing and supervising agents; reviewed by the human
> - observed_at: 2026-09-04

**Lesson:** Shared meaning implemented twice is a drift mechanism.

---

## 34 — Persistence Survived, Restoration Semantics Didn't

A Core UI changed from three goal checkboxes to one dropdown. The stored active goal still existed.
But the load path restored the old checkboxes. If only the visible UI had changed, loading a saved
product would have silently stopped restoring the active goal. The restoration adapter had to change
even though the schema did not.

> **Claim:** a UI-control replacement preserved stored data while invalidating the old restoration mechanism
> - state: DECLARED
> - evidence: source inspection and implementation diff, held by the reporter
> - scope: one saved active-goal field
> - provenance: identified by the supervising agent and included in the deployed fix
> - observed_at: 2026-09-04

**Lesson:** Persistence and restoration are separate mechanisms.

---

## 35 — Legacy Code Is Not Authority

Core already had functioning calculator builders. They were real, tested code. They also embodied an
older product design that the human had superseded. Keeping them because they existed would have made
implementation history outrank current product Authority.

> **Claim:** working legacy builders were deleted because they conflicted with the current shared-product design
> - state: DECLARED
> - evidence: source diff and current product specification, held by the reporter
> - scope: one product's Core calculation surface
> - provenance: observed during the Core consolidation
> - observed_at: 2026-09-04

**Lesson:** Existing implementation is evidence of Reality, not proof of intended Authority.

---

## 36 — Harmless Defects Can Hijack the Work

While implementing Core, the supervising agent found that warning-only answer protections accumulated
on rebuild. It was a real defect. It was also harmless to the current task and unrelated to the UI
being delivered. The defect was recorded and deliberately left unfixed.

> **Claim:** a real but non-blocking defect was intentionally deferred to prevent scope expansion during a bounded work unit
> - state: DECLARED
> - evidence: source inspection and implementation report, held by the reporter
> - scope: one warning-only protection mechanism
> - provenance: observed by the supervising agent; human informed
> - observed_at: 2026-09-04

**Lesson:** A discovered defect is not automatically the current work.

---

## 37 — Agent Capability Is Not Agent Availability

A work plan assigned design and implementation roles to particular models. During one session, the
preferred reasoning model reported capacity unavailable, a second model did the same, and a separate
coding backend returned repeated service errors. The plan failed before capability mattered.

> **Claim:** agent-service availability blocked planned work across more than one model/provider path in the same development session
> - state: DECLARED
> - evidence: service-error screenshots and session transcript, held by the reporter
> - scope: one development session
> - provenance: observed directly by the human
> - observed_at: 2026-09-03/2026-09-04

**Lesson:** Availability is part of Reality.

---

## 38 — Handoff Cost Is Real

When agents became unavailable or sessions were replaced, the next agent needed the repository,
current commit, active Authority, forbidden scope, deployment state, and acceptance boundary. The
handoffs became large enough to be a material part of cost and time.

> **Claim:** repeated context handoffs became a significant operational cost in a long multi-agent development session
> - state: DECLARED
> - evidence: handoff documents and session history, held by the reporter
> - scope: one sustained multi-agent product project
> - provenance: observed by the human across repeated agent switches
> - observed_at: 2026-08/2026-09

**Lesson:** Recoverability of work context has a price too.

---

## 39 — Durable Context Beat Better Memory

The project repeatedly stabilized after current requirements were moved into repository issues. Fresh
agents could then read the same durable source instead of relying on summaries or remembered chat
state.

> **Claim:** persisting current decisions in repository issues reduced ambiguity across fresh-agent handoffs
> - state: DECLARED
> - evidence: issue history and subsequent handoffs, held by the reporter
> - scope: one multi-agent product project
> - provenance: observed by the human and agents
> - observed_at: 2026-09-03/2026-09-04

**Lesson:** Memory is convenience. Durable evidence is infrastructure.

---

## 40 — Safety Infrastructure Can Become the Failure

In prior plugin work, required checks, CI policy, and validation gates created loops where the safety
machinery itself blocked or multiplied otherwise bounded changes. Some failures were legitimate;
others were stale or procedural.

> **Claim:** CI/guard infrastructure became a direct source of repeated work and blocked delivery in at least one plugin-development flow
> - state: DECLARED
> - evidence: CI reports and project session history, held by the reporter
> - scope: the reporter's plugin-development workflow
> - provenance: observed by the human across multiple pull requests
> - observed_at: 2026-06/2026-08

**Lesson:** A guard needs a failure budget and a retirement path.

---

## 41 — Restore Failure Is Its Own State

Recovery work exposed that “restore” is not a binary promise. A restore can succeed technically while
returning to the wrong semantic point, or fail partway and leave evidence that must be preserved for
further recovery. Treating every recovery problem as “retry the same restore harder” loses information.

> **Claim:** recovery drills and incidents required distinguishing restoration failure from ordinary implementation failure
> - state: DECLARED
> - evidence: recovery-session history and the published [snapshot case](./2026-08-05-the-snapshot-that-was-not-known-good.md), held by the reporter
> - scope: the reporter's recovery workflows
> - provenance: derived from lived recovery work; human-approved
> - observed_at: 2026-06/2026-08

**Lesson:** Recovery failure must preserve the evidence needed to understand recovery failure.

---

## 42 — Irreversible Action Changes the Recovery Law

While designing AHL's action boundary, the team found that local edits and externally visible actions
could not share one rollback promise. The same authorization envelope that is safe for a reversible
file edit is not automatically safe for sending, publishing, deleting, or otherwise changing an
external system.

> **Claim:** AHL design review required a separate treatment for actions whose external effects cannot be undone by repository rollback
> - state: UNEVALUATED
> - evidence: AHL design discussion, held by the reporter
> - scope: action/recovery semantics; no production irreversible incident is claimed
> - provenance: derived during internal design work and human-reviewed
> - observed_at: 2026-08

**Lesson:** Reversibility belongs to the action, not merely to the workspace.

---

## 43 — Human Patience Is a Resource

The safety process became so review-heavy that the human explicitly called out development speed and
model cost as unacceptable. That complaint changed the workflow: fewer repeated reviews, bounded
investigation, and one consolidated acceptance after the UI stopped moving.

> **Claim:** human patience, time, and model cost became explicit constraints that forced a process redesign
> - state: DECLARED
> - evidence: session transcript and subsequent process rules, held by the reporter
> - scope: one multi-agent product project
> - provenance: human ruling observed by the agents
> - observed_at: 2026-09-03

**Lesson:** Human attention, money, and patience are part of the work budget.

---

## 44 — The Safe Path Nobody Uses Is Not Safe

AHL's rollback work repeatedly returned to one practical constraint: a recovery path that is too slow,
unclear, or costly will be avoided until the moment it is needed most. The useful recovery paths were
the ones the operator could actually invoke without fear.

> **Claim:** the team's recovery design was changed around the operational cost of invoking rollback, not only its theoretical correctness
> - state: DECLARED
> - evidence: recovery drills, rollback timing, and AHL design history, held by the reporter
> - scope: the reporter's agent-driven recovery workflow
> - provenance: observed by the human and agents; principle already reflected in repository doctrine
> - observed_at: 2026-07/2026-08

**Lesson:** A rollback path must be cheap enough to actually use.

---

## 45 — A Belief Too Expensive to Update Becomes Dogma

The project accumulated detailed design documents, guards, verification suites, and repeated
acceptance procedures. As the product changed, some of those beliefs became expensive enough to
update that they resisted reality: stale guards survived, old rules kept reappearing, and verification
cost threatened the goal. The human finally imposed a cheaper rule: let UI beliefs die during UI work,
then verify the frozen design once.

> **Claim:** high update cost caused obsolete checks and requirements to persist beyond the design decisions that originally justified them
> - state: DECLARED
> - evidence: stale guard reports, superseded issues, and process rulings, held by the reporter
> - scope: one long-running spreadsheet-product project and its agent workflow
> - provenance: observed by the human and agents; human-approved for publication
> - observed_at: 2026-09-03/2026-09-04

**Lesson:** A belief must be written cheaply enough to die cheaply.

---

## What the forty-five cases say together

The cases do not divide cleanly into “agent failures” and “human failures.” That division would hide
the useful part.

They cluster around eight harder facts:

1. **Reality can veto Authority.** A platform, runtime, or external effect can make an approved plan
   impossible or change its recovery law.
2. **Authority must be current and durable.** Old truth can be obeyed perfectly after it has become
   wrong.
3. **Verification is fallible.** Tests, guards, fixtures, and verifiers are mechanisms too.
4. **Recovery has scope.** Restoring files is not the same as restoring meaning or undoing consequences.
5. **Safety has a cost.** Assurance can become the work it was meant to protect.
6. **Humans are not infallible.** The human may point at the wrong mountain, revise a ruling, or discover
   that the original requirement had no mechanism.
7. **Agent obedience is not enough.** Faithful execution can still serve a false premise, stale
   Authority, or a misleading UI.
8. **Human-facing truth matters.** A system can be internally correct and still teach the human the
   wrong model of what it is doing.

There is no claim here that failure is good. Failure is debt. The useful question is whether the debt
buys a cheaper mistake tomorrow.

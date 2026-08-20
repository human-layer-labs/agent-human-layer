# NEWBORN CONSEQUENCE POLICY — LIVE

Status: `NEWBORN AHL — LIVE`

This file is the sole normative owner of factual consequence classification.
It is live through the newborn AHL router.

## 1. Ownership

This file owns exactly:

- the four factual consequence Levels;
- the consequence classifier;
- the AHL2/AHL3 distinction;
- highest credible factual consequence;
- consequence-specific aggregate factual consequence;
- anti-fragmentation;
- exclusions from Level; and
- the consequence-specific classification actor contract.

This file does not own authorization, Goal resolution, Route selection,
Target truth, Recovery truth, Boundary derivation, Release satisfaction,
Human grant formation, or Work Unit serialization. Those contracts remain with
their named owners. `ahl-flow.md` supplies lifecycle placement and consumes
the classification result.

Classification is factual, not authorization. A factual Level does not grant
permission, create authority, select a Target, satisfy Recovery, satisfy a
Boundary, satisfy a Release requirement, or replace a Human decision.

## 2. Exactly four factual Levels

Exactly four newborn factual consequence Levels exist:

### AHL1 — NON-OPERATIVE

Wrong execution changes only non-operative representation and cannot credibly
alter any of the following:

- meaningful Agent or system behavior;
- workflow result;
- authoritative state;
- consequential Human or user action; or
- external effects.

Behavior-changing policy Markdown is not automatically AHL1 merely because it
is text or documentation-like. If changing the text can alter operative
behavior, workflow results, authoritative state, consequential action, or
external effects, the work is not AHL1.

### AHL2 — MINOR

Wrong execution changes meaningful operative behavior or output, but no
credible consequence reaches materiality.

AHL2 is operative but non-material. It MUST NOT be collapsed into AHL1 merely
because its implementation is small, textual, or easy to revert.

### AHL3 — MATERIAL

Wrong execution can materially affect one or more of the following while
credible harm remains bounded and non-critical:

- a bounded workflow;
- authoritative or shared state;
- coupled units;
- a real subject;
- a limited external effect; or
- a limited operational outcome.

AHL3 owns bounded material consequence. Persistence after revert may indicate
consequence but is not an independent Level rule.

### AHL4 — CRITICAL

Wrong execution can violate a critical protected invariant or cause broad,
severe, or insufficiently bounded material harm.

The newborn model has no AHL5 or AHL6 factual Levels. Urgency, recovery work,
and production context do not create additional consequence Levels.

## 3. Classification rule

Classify the highest credible factual consequence of the final selected Route
in its actual context. The selected Route and coordinated effect set are the
classification context.

Include:

- direct effects; and
- intended ordinary consumers of those effects.

Exclude speculative remote chains with no credible causal basis. Unknown facts
must not be represented as a low-confidence Level. Establish a load-bearing
fact through the flow's Challenge/Evidence lifecycle when needed, or use the
honest highest credible consequence supported by the current facts.

Level MUST NOT encode:

- Recovery;
- urgency;
- effort;
- confidence;
- Human preference;
- Human permission;
- requested caution;
- Operation name;
- Target label;
- domain ownership;
- file type or path;
- file count; or
- production or database involvement by itself.

Recovery MUST NOT lower or otherwise change factual Level. Production context
does not automatically raise Level. Database involvement does not
automatically create a critical Level. A path, label, credential, technical
access, or writable location is not consequence evidence by itself.

Human shorthand such as `4で慎重に` MAY bind extra controls in the owning
authorization or flow context when attributable, but MUST NOT rewrite factual
Level. Human permission and requested caution are not classification inputs.

## 4. Aggregate factual consequence

Effect semantics are authoritative. For a coordinated permitted effect set,
the aggregate factual consequence is the highest credible consequence of that
set in its actual context, including intended ordinary consumers.

Do not average, add, or otherwise launder Levels across arbitrary edit slices.
The aggregate result is derived from the coordinated factual effects and
their credible consumers, not from a Human-selected numeric ceiling and not
from authorization status.

Aggregate classification MUST preserve anti-fragmentation. If the selected
Route has one independently meaningful outcome, classify that outcome in its
combined context even when its implementation has multiple edits.

## 5. Anti-fragmentation

This file is the sole normative owner of anti-fragmentation.

Work Unit decomposition MUST NOT lower coordinated factual consequence.

If multiple mutations do not have independently meaningful outcomes and
jointly create one consequence, classify the coordinated outcome rather than
laundering it into nominally lower Work Units. Do not emit separate lower
Levels merely because each mutation is small.

The canonical discriminating case remains possible:

```text
multiple mutations
→ no independently meaningful outcome
→ jointly create one bounded non-critical material consequence
→ classify the coordinated outcome as AHL3
→ do not emit N × AHL2 merely because each mutation is small
```

Anti-fragmentation is not a universal merge rule. Preserve independently
meaningful outcomes as separate Work Units when each has its own meaningful
result and can be classified, authorized, executed, and validated separately.

Do not use decomposition to manufacture a lower factual Level. Do not merge
independent outcomes merely to manufacture a higher one.

## 6. Classification actor contract

The acting Agent applies this policy to established facts and makes the
evidence-backed factual judgment required by the classifier.

Challenge obtains and tests load-bearing facts. Core orchestrates lifecycle
and ordering. Policy derives only what is mechanically derivable. Arbiter may
adjudicate a legitimate open technical Route inside Challenge, but MUST NOT
decide factual Level. Human permission, Human preference, and requested
caution MUST NOT decide factual Level.

No separate classification authority, classifier subsystem, or hidden Level
authority exists. The acting Agent applies this policy; `ahl-flow.md` places
that application in the final semantic fixpoint.

## 7. Cross-owner boundary

This file returns a factual consequence result to the flow. It does not:

- authorize a state-changing occurrence;
- build or amend an Authorization Envelope;
- decide whether an occurrence belongs to an Envelope;
- derive or satisfy a Boundary;
- derive or satisfy a Release requirement;
- select a Route;
- establish Target truth;
- establish Recovery applicability; or
- serialize a Work Unit.

Authorization remains independent of factual Level. A high Level is not
automatically unauthorized, and a low Level is not automatically authorized.

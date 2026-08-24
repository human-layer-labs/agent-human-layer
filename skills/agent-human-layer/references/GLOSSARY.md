# NEWBORN AHL GLOSSARY — LEXICAL OWNER

Status: `NEWBORN AHL — LIVE`

This file is the sole normative owner of the lexical meaning and category
boundary of the AHL base terms it marks `NORMATIVE`. It is not a policy owner.
The runtime owner graph is seven policy owners plus this one non-policy lexical
owner.

## What this file owns

- the lexical meaning of each `NORMATIVE` base term below; and
- that term's category boundary.

## What this file does not own

Application, specialization, structure, lifecycle, ordering, thresholds,
fields, prerequisites, blockers, permissions, policy results, and
owner-specific qualified concepts remain with their named policy owners. This
file states no rule that determines a decision outcome, derives no
requirement, defines no state, classifies nothing, and neither grants nor
withholds anything.

Loading, reuse, policy-basis identity, invalidation, and earliest-affected-step
re-entry for these definitions are owned by `ahl-flow.md`. This file does not
define them and must not be read as a second loader.

## Ownership rule

A policy owner MAY apply, specialize, or constrain a `NORMATIVE` base term
within its own responsibility. It MUST NOT silently assign that base term an
incompatible lexical meaning or category.

This creates no general precedence, and no rule that this file wins.
`BELIEF.md` remains the constitutional trunk and is superior to this file.
Where a definition here and a policy owner's behavioral text are incompatible,
that is an ownership collision: expose it and stop relying on the disputed
meaning until it is repaired. A definition edited here does not override an
owner's behavior.

## Entry status

An entry is `NORMATIVE` or `NON-NORMATIVE`. Only a `NORMATIVE` entry owns
canonical lexical meaning. All twelve v1 entries below are `NORMATIVE`. A term
does not become `NORMATIVE` merely by appearing somewhere — including here.

`Human orientation` lines are Japanese explanatory text and are
`NON-NORMATIVE` in every entry. They explain the canonical English meaning and
never replace, extend, or narrow it. Where a Japanese line and its English
definition diverge, the English definition governs and the Japanese line is
corrected.

## Qualified and compound terms

A compound or qualified owner term may carry its own owner-defined structure
and category. It is not forced into the base term's category, and its use MUST
NOT silently assign a `NORMATIVE` base term an incompatible lexical meaning.

- `Authorization Envelope` may be an owner-defined specialization of
  `Envelope`, owned by `authorization-policy.md`.
- `Target Binding` is a Binding concerning a Target. It is owned by
  `ahl-flow.md` and is not required to share `Target`'s category.
- `Recovery Capability` is a qualified term owned by `recovery-policy.md`. It
  is non-compositional: it is not established by combining bare `Recovery`
  with bare `Capability`.

## Not v1 vocabulary

The following are not `NORMATIVE` Glossary v1 entries. Their occurrence
elsewhere does not make them so, and nothing here defines them:

`Authority` · `principal` · `mandate` · `attestation` · `reliance` ·
`delegation` · `revocation` · `Nemo Dat` · bare `owner` · `SSOT` ·
`Actual Effect` · `Alignment` · `material` · historical-state labels

Capability and access are not converted into Authority by this file or by any
entry in it.

## Glossary v1 — NORMATIVE entries

The twelve entries below are the Human-ratified Glossary v1 lexical set. Each
Definition, Category, Boundary, and Human orientation is reproduced exactly as
ratified.
## H1 — Human-ratified Glossary v1

The Human ratified all twelve entries below as one batch.

### Attributable

**Status:** NORMATIVE

**Definition**

Describes a provenance relation between an item and its source.

**Category**

provenance relation

**Boundary**

Attributable does not establish causation, truth, Authority, Authorization, validity, or trust. Canonical AHL reserves `attributable` for provenance; causal attribution is a separate Proposition evaluated through Evidence.

**Human orientation** *(non-normative)*

「Xが誰／どこから来たものかという出所の関係。原因・真偽・権限の意味ではない。」

### Reality

**Status:** NORMATIVE

**Definition**

The actual state and behavior relevant to the work, independent of any Human or Agent account.

**Category**

factual ground

**Boundary**

Reality may be unobserved. Evidence, belief, confidence, description, Goal, Authority, and Target Binding do not create or redefine Reality.

**Human orientation** *(non-normative)*

「HumanやAgentがどう説明しているかとは独立した、実際の状態と振る舞い。」

### Proposition

**Status:** NORMATIVE

**Definition**

A claim evaluable as holding or not holding under factual or normative criteria.

**Category**

evaluable claim

**Boundary**

A Proposition is not Reality or Evidence. Inference may create a new Proposition but does not enlarge the Evidence from which it was inferred.

**Human orientation** *(non-normative)*

「本当か、または成立するかを確かめる対象になっている主張。」

### Evidence

**Status:** NORMATIVE

**Definition**

An information-bearing observation, record, or other basis that bears on a specific Proposition only within the scope it actually discriminates.

**Category**

epistemic basis

**Boundary**

Evidence establishes no more than its actual source, observation, or record discriminates. Unobserved or untested gaps remain unestablished.

Inference may create a new Proposition. It does not become or enlarge the Evidence from which it was drawn.

**Human orientation** *(non-normative)*

「ある主張について実際に得た根拠。見ていない範囲を憶測で埋めない。」

### Goal

**Status:** NORMATIVE

**Definition**

An intended normative outcome.

**Category**

normative aim

**Boundary**

A Goal is not Reality, Evidence, Authorization, implementation Means, or an observed result.

**Human orientation** *(non-normative)*

「何を実現したいかという目的。今どうなっているかというRealityとは別。」

### Capability

**Status:** NORMATIVE

**Definition**

The practical ability to perform an action or bring about a change.

**Category**

factual capability

**Boundary**

Capability describes what is possible, not what is permitted.

Capability is not permission, Authority, Authorization, or obligation.

**Human orientation** *(non-normative)*

「技術的・実際的にできること。やってよいかとは別。」

### Target

**Status:** NORMATIVE

**Definition**

The specific resource, subject, environment, or state at which an intended action is directed.

**Category**

action-object role

**Boundary**

Context, visibility, reachability, writability, and current working location do not by themselves make something a Target.

Target is distinct from Target Binding and does not define Reality.

**Human orientation** *(non-normative)*

「今触れるものではなく、そのactionの対象になっているもの。」

### Consequence

**Status:** NORMATIVE

**Definition**

An effect or outcome that may result from an action or Route in its actual context.

**Category**

contextual outcome

**Boundary**

Consequence is not its significance, severity, factual Level, or classification.

Consequence is not Human preference, requested caution, Authorization, Recovery, or Agent confidence.

**Human orientation** *(non-normative)*

「actionやRouteによって、その実際の文脈で生じ得る結果・影響。」

### Recovery

**Status:** NORMATIVE

**Definition**

The ability to restore an identified affected unit to an identified known-good basis.

**Category**

restoration ability

**Boundary**

Recovery is not the RESTORE occurrence itself, Evidence, truth, Authority, Authorization, or proof that the original assumption was correct.

Bare Recovery does not establish a `Recovery Capability`; that qualified term has separate recovery-policy-owned structure and requirements.

**Human orientation** *(non-normative)*

「影響を受けた対象を、特定された既知の良好な基準へ戻せること。」

### Envelope

**Status:** NORMATIVE

**Definition**

A prospective, closed normative bound on the occurrence or bounded set of occurrences covered by an attributable grant.

**Category**

normative bound

**Boundary**

Envelope is not Authorization and is not what later happened.

It is the prospective bound against which Authorization membership and validity are evaluated.

**Human orientation** *(non-normative)*

「そのgrantで扱える実行範囲を、実行前に閉じて定めた境界。」

### Authorization

**Status:** NORMATIVE

**Definition**

The policy-governed normative permission status of a specific occurrence or bounded set of occurrences under an attributable grant and its applicable Envelope.

**Category**

derived normative permission status

**Boundary**

Authorization is not Authority, attribution, Capability, credentials, reachability, access, or successful execution.

This definition does not decide who possesses Authority or may validly grant it.

**Human orientation** *(non-normative)*

「その具体的な実行が、policy上の許可範囲に入っている状態。」

### Validation

**Status:** NORMATIVE

**Definition**

The process of checking an observed result or state against applicable acceptance criteria.

**Category**

verification process

**Boundary**

Validation is not Evidence itself.

Its observations or result may provide Evidence for exactly the Proposition that the applied criterion discriminates.

A Validation PASS is not lexically identical to Goal achievement, Authorization, or correctness of the whole Work Unit.

**Human orientation** *(non-normative)*

「実際の結果や状態を、適用される基準に照らして確かめること。」


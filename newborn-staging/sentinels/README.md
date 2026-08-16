# NEWBORN SENTINELS — NON-LIVE MIGRATION VERIFICATION

Status: `NEWBORN IMPLEMENTATION — NON-RUNTIME`

This directory contains declarative migration Sentinels. It is not a test
framework, runtime subsystem, database, compatibility layer, or activation
path. A Sentinel is a discriminating regression contract: it describes a
setup, the load-bearing proposition, the trigger, the expected newborn
result, and the forbidden historical failure.

## Scope and authority

The frozen architecture remains the sole architecture SSoT:
`AHL-CANONICAL-TARGET.md`. The implemented newborn owners supply the rules
that each Sentinel names. The Sentinel suite does not redefine those rules.

- `ahl-flow.md` owns lifecycle, Target, Route, Evidence general semantics,
  policy loading/reuse, Core, Act, Validate, failure, and Reality collision.
- `consequence-policy.md` owns factual consequence and anti-fragmentation.
- `authorization-policy.md` owns Envelope, grant, membership, carry,
  blockers, allowance, reservation, suspension, and end.
- `recovery-policy.md` owns Recovery Capability, Fast, applicability,
  composition, Evidence, and Recovery failure.
- `boundary-policy.md` owns separately protected Boundary requirements.
- `release-gate-policy.md` owns exact artifact-to-target release transition
  and release validation.
- `work-unit-format.md` owns serialization only.

## Coverage

`sentinel-cases.md` contains **55** numbered cases. The 46 explicit
blueprint Sentinels are covered by one or more of S001–S055; the mapping is
kept below so the final count is auditable without relying on Agent memory.

S055 is the additional migration Sentinel for the verified historical
Scenario 3 failure: an explicitly requested Level could suppress a required
approval when no attributable grant existed.

| Blueprint Sentinel | Case coverage |
|---:|---|
| 1 | S001 |
| 2 | S002 |
| 3 | S003–S005 |
| 4 | S006 |
| 5 | S007 |
| 6 | S005 |
| 7 | S049 |
| 8–9 | S008 |
| 10 | S012 |
| 11 | S013 |
| 12 | S014 |
| 13 | S015 |
| 14 | S019 |
| 15 | S022–S023 |
| 16 | S024 |
| 17 | S007, S016 |
| 18 | S029–S031 |
| 19 | S009–S010, S033 |
| 20 | S028 |
| 21 | S034–S035 |
| 22 | S014 |
| 23 | S018 |
| 24 | S021 |
| 25 | S040 |
| 26 | S043 |
| 27 | S011 |
| 28–30 | S036 |
| 31 | S039 |
| 32 | S036 |
| 33 | S038 |
| 34 | S036 |
| 35 | S014 |
| 36 | S035 |
| 37 | S025 |
| 38 | S027 |
| 39 | S028 |
| 40 | S044 |
| 41 | S045 |
| 42 | S048 |
| 43 | S051 |
| 44 | S053 |
| 45 | S047 |
| 46 | S054 |

The ranges intentionally point to discriminating cases rather than creating
decorative one-line duplicates.

## Historical Scenario 1–5 crosswalk

No standalone legacy Scenario 1–5 artifact exists in the bounded repository
or reachable history. The frozen scars are retained as explicit anchors, with
the invariant owned by the newborn policy named in each case:

| Scenario | Historical artifact result | Preserved invariant | Sentinel anchor |
|---|---|---|---|
| Scenario 1 | Not found as standalone legacy file | Low-consequence work does not create unnecessary Human Tax. | S001 |
| Scenario 2 | Not found as standalone legacy file | Operative policy changes are classified by consequence, not by Markdown appearance. | S002–S004 |
| Scenario 3 | No standalone scenario file; reachable history at `4af6316` and its parent contains the requested-Level/authorization repair | Requested Level or caution is not authority; absent attributable grant remains `APPROVAL_REQUIRED`. | S055 |
| Scenario 4 | Not found as standalone legacy file | Recovery, allowance, and authorization state do not create unsafe retry or repair authority. | S014–S021, S053 |
| Scenario 5 | Not found as standalone legacy file | Cutover preserves contracts without mixed ownership or ordinal-level mapping. | S048, S051–S053 |

This crosswalk preserves scars, not guessed historical anatomy. Scenario 3 is
explicitly retained as a newborn Sentinel anchor.

## Review rule

A case passes only when its expected result is distinguishable from its
forbidden result. Merely mentioning a policy term is insufficient. If a
future harness is added, it must execute these propositions without changing
the owner boundaries or inventing a runtime architecture.

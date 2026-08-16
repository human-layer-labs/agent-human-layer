# LEGACY CONTRACT MAP — NON-LIVE NEWBORN MIGRATION

Status: `NEWBORN IMPLEMENTATION — MIGRATION INPUT ONLY`

This artifact records protections extracted from the bounded legacy AHL
surface. Legacy implementation, terminology, ordinal numbering, and ceremony
are not carried as a second architecture. The frozen blueprint and the
implemented newborn owners are authoritative when a legacy behavior conflicts
with them.

## Bounded inspection

Inspected legacy sources:

- `AGENTS.md` — host bootstrap and project-entry floor.
- `skills/agent-human-layer/SKILL.md` — legacy entry contract, authorization
  presentation, and examples.
- `skills/agent-human-layer/references/ahl-flow.md` — legacy lifecycle,
  route adherence, target, authorization blockers, recovery, release, and
  human-tax behavior.
- `skills/agent-human-layer/references/risk-levels.md` — legacy risk names,
  AHL1 eligibility, minimum floors, escalation, and recovery expectations.
- `skills/agent-human-layer/references/route-format.md` — route, boundary,
  stop-condition, recovery, and execution presentation.
- `skills/agent-human-layer/references/recovery-policy.md` — legacy snapshot
  and restore assumptions.
- `skills/agent-human-layer/references/release-gate-policy.md` — legacy
  snapshot-backed trial, release, CI, conflict, and live-state boundaries.

No standalone historical Scenario 1–5, sentinel, or smoke artifact was found
in the bounded repository file inventory. Reachable Git history does contain
the material Scenario 3 failure/repair evidence at `4af6316` and its parent:
the parent hard-stop predicate required approval only when no requested Level
was explicitly bound, and `4af6316` changed that predicate to estimated
consequence. Scenario anchors are cross-referenced to the frozen blueprint
and the discriminating cases in `../sentinels/sentinel-cases.md`; no
undocumented legacy scenario detail is invented.

## Disposition vocabulary

- **PRESERVE** — the protection remains materially required and is carried to
  a newborn owner without changing its safety purpose.
- **REEXPRESS** — the protection remains required, but its legacy mechanism or
  owner is replaced by the newborn owner named below.
- **RETIRE** — the behavior was ceremony, obsolete anatomy, or a forbidden
  ordinal/provider assumption; retiring it loses no required protection.

## Extracted contracts

| ID | Legacy source / locator | Legacy behavior | Protection actually intended | Newborn owner | Newborn mechanism | Sentinel ID(s) | Disposition | Why |
|---|---|---|---|---|---|---|---|---|
| LC-01 | `risk-levels.md`, Levels and classification | AHL1 represented tiny non-operative work. | Keep genuinely non-operative work small and low-tax. | `consequence-policy.md`, `ahl-flow.md` | Four-level factual classifier plus applicable authorization flow. | S001 | REEXPRESS | The protection survives; the six-name risk presentation does not. |
| LC-02 | `risk-levels.md`, `## small` and flow AHL2 rules | AHL2 represented meaningful but non-material operative change. | Distinguish operative minor consequence from non-operative text. | `consequence-policy.md` | Factual AHL2 with no automatic permission. | S003 | REEXPRESS | Newborn consequence semantics replace legacy risk names. |
| LC-03 | `risk-levels.md`, `## normal` and flow AHL3 rules | AHL3 represented bounded material development consequence. | Preserve bounded material consequence and its stronger route/recovery needs. | `consequence-policy.md`, `ahl-flow.md`, `authorization-policy.md` | Factual AHL3, final fixpoint, and exact membership. | S004, S054 | REEXPRESS | The consequence is preserved without a legacy risk taxonomy. |
| LC-04 | `risk-levels.md`, `## risky` and flow AHL4+ rules | AHL4 represented critical or difficult-to-restore work. | Protect critical invariants and broad or severe harm. | `consequence-policy.md`, `boundary-policy.md`, `release-gate-policy.md`, `authorization-policy.md` | Factual AHL4 plus independent Boundary, Release, Recovery, and Authorization results. | S005, S049 | REEXPRESS | Critical consequence is preserved; Recovery and production are not Level inputs. |
| LC-05 | `ahl-flow.md`, level table and hotfix example | AHL5 compressed urgent or production-facing safety behavior. | Keep urgent/production-facing work minimal, visible, reversible, and release-gated. | `ahl-flow.md`, `boundary-policy.md`, `release-gate-policy.md`, `authorization-policy.md` | Operation/Route, Boundary, Release, and exact approval/recovery prerequisites. | S048, S051, S052 | REEXPRESS | Urgency and production protection survive without an AHL5 Level. |
| LC-06 | `ahl-flow.md`, level table and recovery example | AHL6 compressed restoration and snapshot prerequisites. | Restore only an identified unit to an identified known-good basis with validation. | `recovery-policy.md`, `ahl-flow.md`, `authorization-policy.md` | Recovery Capability, per-use applicability, Evidence, and separate RESTORE Work Unit. | S014–S018, S048 | REEXPRESS | Recovery semantics survive; AHL6 is not a newborn Level. |
| LC-07 | `ahl-flow.md`, AHL4+ hard stop and production examples | AHL4+ required bound approval before action. | Require authority appropriate to the exact high-consequence occurrence. | `authorization-policy.md` | Closed-World Envelope, exact provenance, membership, and independent prerequisites. | S005, S022, S048 | REEXPRESS | Approval protection survives without mapping AHL4+ to a numeric newborn rule. |
| LC-08 | `risk-levels.md`, mandatory classification steps 1–7; `ahl-flow.md`, steps 3–5 | Requested and estimated levels were separate; higher requested level added controls. | Do not let Human-requested caution rewrite factual consequence. | `consequence-policy.md`, `authorization-policy.md` | Factual classification is independent; attributable requested controls remain bounded authority input. | S006, S050 | REEXPRESS | The separation is load-bearing; mandatory numeric ceremony is not. |
| LC-09 | `SKILL.md`, hard invariants and AHL1 fast path | Unspecified tiny work could use an AHL1 fast path after eligibility checks. | Allow low-tax handling only for genuinely eligible non-operative work. | `consequence-policy.md`, `ahl-flow.md`, `authorization-policy.md` | AHL1 eligibility, exact current request, and explicit `PROCEED` from flow. | S001, S002 | REEXPRESS | Fast handling remains conditional and cannot bypass the flow. |
| LC-10 | `risk-levels.md`, “choose the higher”; escalation rules | Unknown or unclear risk was escalated rather than guessed low. | Unknown load-bearing facts must be established or handled at the honest higher consequence. | `consequence-policy.md`, `ahl-flow.md` | Challenge/Evidence and highest credible factual consequence. | S028, S044 | PRESERVE | This prevents false reassurance and remains directly required. |
| LC-11 | `risk-levels.md`, database minimum floor; `ahl-flow.md`, DB boundary row | DB/schema/production cases received a numeric safety floor plus a separate protected DB/live-data gate. | Numeric floor RETIRED. Reexpress the load-bearing protection through explicit attributable authority for the exact protected production/live-data DB target/effect in `boundary-policy.md`. Existing exact authority may satisfy the Boundary without duplicate confirmation; generic approval/access does not. | `boundary-policy.md`, `release-gate-policy.md`, `authorization-policy.md` | Concrete applicability, factual Target/resource/effect basis, exact attributable target/effect authority coverage, separate fact/provenance channels, and `BOUNDARY_REQUIRED` consumption; no automatic Level floor. | S049, S056 | REEXPRESS | The numeric/domain floor is obsolete anatomy; the protected-state requirement is preserved by exact attributable Boundary authority. Independent validation remains pending. |
| LC-12 | `ahl-flow.md`, confirmation binding | Approval was bound to estimated level, Route, scope, target, and blocker set. | Prevent an approval from being reused for a materially different action. | `authorization-policy.md`, `ahl-flow.md` | Exact normalized Envelope, provenance, occurrence membership, and flow re-entry. | S022, S024, S052 | PRESERVE | Exact authority binding is a surviving protection. |
| LC-13 | `ahl-flow.md`, legacy blocker table | `APPROVAL_REQUIRED`, `PREREQUISITE_REQUIRED`, and `BOUNDARY_ROUTE_REQUIRED` separated authority, evidence, and boundary problems. | Do not let approval satisfy a missing fact or protected boundary. | `authorization-policy.md`, `boundary-policy.md`, `ahl-flow.md` | Newborn three-blocker set with `BOUNDARY_REQUIRED` owned by Boundary policy. | S027, S041, S050 | REEXPRESS | The protection survives while the legacy boundary name and ownership are replaced. |
| LC-14 | `ahl-flow.md`, permissive development rules and repeated approval flow | AHL2/AHL3 development could still cause repeated confirmation after rereads or bounded occurrences. | Avoid unnecessary Human Tax while retaining real invalidation. | `ahl-flow.md`, `authorization-policy.md`, `consequence-policy.md` | Carry unchanged Envelope and Evidence; re-enter only on material change. | S025, S026, S043 | RETIRE | Repeated unchanged approval is ceremony, not a protection. |
| LC-15 | `recovery-policy.md`, snapshot levels and restore rules; `release-gate-policy.md`, snapshot-backed trial | Snapshots matched restore units; restore was replacement, not overlay; DB/live recovery was excluded. | Make restoration bounded, evidenced, applicable, and honest about residual risk. | `recovery-policy.md`, `ahl-flow.md`, `release-gate-policy.md` | Seven-field Capability, Evidence, per-use target/source binding, and separate RESTORE route. | S014–S020, S053 | REEXPRESS | Recovery protection survives without legacy snapshot ritual or provider assumptions. |
| LC-16 | `references/ahl-flow.md`, Route Adherence and violation transition | Safety-critical order had to be declared and a violation stopped further mutation. | Prevent out-of-order mutation and retroactive legalization. | `ahl-flow.md` | Declared partial order, reachability check, preserved actual state, and new repair Work Unit. | S008, S011, S012 | PRESERVE | This is an explicit newborn flow contract. |
| LC-17 | `AGENTS.md`, host bootstrap; `ahl-flow.md`, Startup/Target | Active cwd/workspace was only a candidate; bounded discovery established target and must not mutate Human state. | Prevent valid work from landing in the wrong repository or overwriting unknown work. | `ahl-flow.md`, conforming host bootstrap | Target Binding, discriminating Evidence, bounded discovery, and fail-closed rerouting. | S036–S039 | PRESERVE | Wrong-target protection is a direct startup invariant. |
| LC-18 | `SKILL.md`, Git/recovery examples; `release-gate-policy.md`, provider and CI sections | GitHub, snapshots, CI, and host mechanisms were used as concrete route assumptions. | Preserve admissible provider evidence without making one provider canonical. | `ahl-flow.md`, `boundary-policy.md`, `release-gate-policy.md` | Provider-neutral adapters and exact proposition Evidence. | S040, S041, S048 | REEXPRESS | Provider observations can remain inputs; provider architecture and mandatory Git markers retire. |
| LC-19 | `ahl-flow.md`, no-loop/conflict rules; `release-gate-policy.md`, CI/conflict policy | Related failures received one focused repair attempt; conflicts and unrelated failures stopped. | Bound repair and prevent CI/conflict loops or unrelated mutation. | `ahl-flow.md`, `release-gate-policy.md` | Failure Work Unit, local stop, and explicit release validation. | S012, S040, S044 | PRESERVE | This is a surviving operational safety contract. |
| LC-20 | `release-gate-policy.md`, production gates and one-minute restore | Production release required exact checks, restore, and explicit approval. | Do not release an ambiguous artifact to an ambiguous target. | `release-gate-policy.md`, `boundary-policy.md`, `authorization-policy.md` | Exact artifact → exact Target Binding transition, temporal checks, and post-release Evidence. | S034, S035, S048 | REEXPRESS | Release protection survives as its own owner, not as AHL5/production Level. |
| LC-21 | Bounded inventory found no standalone Scenario 1–5 files; reachable `4af6316` and `4af6316^` `ahl-flow.md` hard-stop table | The legacy predicate let an explicitly requested Level suppress the no-grant approval condition; the repair separated requested Level from authorization. | `authorization-policy.md` for closed-world attributable grant/membership; `consequence-policy.md` for factual Level independence | Exact Envelope/grant membership; requested Level may add valid controls but cannot substitute for authority. | SCN-01–SCN-05; S001, S014, S036, S048, S054, S055 | REEXPRESS | Reachable history proves Scenario 3 protected separation between requested Level and authorization. S055 preserves the scar; no old ordinal rule is carried. |

## Extraction result

- Meaningful contracts found: **21**.
- `PRESERVE`: **5**.
- `REEXPRESS`: **15**.
- `RETIRE`: **1**.
- Unmapped load-bearing contracts: **NONE** within the bounded inspected
  surface.

Retired items are:

- the automatic DB/production numeric Level floor; and
- repeated unchanged confirmation ceremony as ceremony/tax.

The DB/production protected-condition requirement is **NOT retired**. Its
load-bearing protection is **REEXPRESSED** through the newborn concrete DB
Boundary adapter, with applicable Release/Authorization ownership and exact
attributable authority coverage. The numeric floor is retired; the protected
condition is not.

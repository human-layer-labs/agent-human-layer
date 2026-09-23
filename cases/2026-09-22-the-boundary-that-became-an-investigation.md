# 2026-09-22 — The boundary that became an investigation

## Context

An agent was preparing an already-audited payroll fix for deployment to a test environment.

The test environment shared a host with production. Production was explicitly outside the deployment Target. The deploy procedure used production directory metadata as a boundary check: record it before deployment, modify only the test environment, and compare the metadata afterward. Stop if the deployment appeared to have changed production.

Before any server write, the agent ran the planned read-only precheck. The test Target matched the expected build, the package had been built and checked, the audit and test suite had passed, and the planned deployment would not change the schema version.

## What happened

**What was observed:** During the precheck, the agent observed that production directory metadata had changed since an earlier observation. No server write for this deployment had occurred.

**What remained UNEVALUATED:** Who made the earlier change, why it happened, and whether it had any material connection to the test Target or the planned deployment.

**What the agent inferred:** Because the change was unexplained, deployment should not proceed until the Human explained it.

**What became the blocker:** The Human was asked to account for an earlier production change before an action whose Target was the test environment. The report does not establish that this stop was formally labeled as an AHL Authorization blocker.

**What the Human challenged:** Whether the observed change could materially affect the next test-environment deployment. The Human did not need to explain the production change to ask that question.

## What caught it

The Human noticed that the stop had shifted the work from deploying one audited build to investigating an unexplained production change.

The production metadata change was real and worth recording. The account did not show evidence connecting it to the candidate package, test Target, planned deployment, or next test-environment occurrence. The Human challenged whether its unknown origin alone could change the next action.

## What made recovery cheap

No server write had occurred, so no product state needed restoration. The audited package remained ready. The precheck's production metadata observation could serve as a fresh baseline if the test deployment resumed.

## What changed

The production observation remained recorded, while its origin and relevance to the planned test deployment remained UNEVALUATED. The intended route remained limited to the test environment, with a post-deployment comparison against the new baseline and a stop if this deployment appeared to affect production.

The report does not say that the deployment later resumed.

## For other teams

In this incident, separating the observed metadata change from the unknown cause and the unestablished connection to the next deployment kept the Human's question focused on the actual work. The observation was preserved without turning production investigation into an unstated part of the test deployment.

## Bounded claim

**Claim:** In one reported test-environment deployment for a payroll fix on 2026-09-22, an agent's read-only precheck recorded a change in production directory metadata and the agent required the Human to explain it before proceeding, although the reporter says the available observations did not connect that change to the planned test deployment. The Human challenged the stop before any server write.

- state: DECLARED
- evidence: private deployment and audit records, runtime observations, and the Human-agent conversation held by the reporter
- scope: one reported test-environment deployment and its production-metadata check on 2026-09-22
- provenance: the project maintainer reports the incident from private records and runtime observations; this draft is structured from the supplied account
- observed_at: 2026-09-22
- human_reviewed: yes — approved by the reporter on 2026-09-23

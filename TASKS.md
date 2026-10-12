---
type: project
epistemic_status: unverified
authority: none
lifecycle: draft
domain: [software-engineering, systems-engineering, artificial-intelligence]
topics: [agent-assisted-development, specification-driven-development, test-driven-development, evaluation-driven-development]
sources: ["../Justin_Arce_Portfolio_Master_Plan.md", "../../60_Decisions/2026_10_09_Portfolio_Career_ROI_Sequence.md", "../../10_Standards/Project_Harness_Standard.md"]
human_reviewed: false
reviewed:
---

# Vibe Coding Lab: task register

## TASK-001: Define the first observable vertical slice

- Status: scope documented on 2026-10-10; formal acceptance and runtime checks not recorded
- Requirement IDs: PRJ-001
- History: the 2026-10-09 scaffold asked for an unspecified reference service. On 2026-10-10 the user requested harness updates around the proposed CSV Data Quality Checker.
- Included behavior: define users, exclusions, required columns, counting rules, reports, exit codes, acceptance examples and three delivery stages in PROJECT.md and the other harness records.
- Allowed change area: this project folder and the root progress handoff.
- Acceptance review: inspect the seven harness documents for a consistent first-stage contract and master-plan traceability. Documentation validation is separate from application acceptance.
- Evidence: this conversation establishes requested direction; no runtime evidence exists. See PROGRESS.md for structural validation results.
- Known limitations: detailed contract elaboration remains draft and human_reviewed remains false.

## TASK-002: Bootstrap the implementation harness

- Status: ready; next implementation task
- Requirement IDs: PRJ-002, PRE-A
- Dependencies and eligibility: TASK-001 scope is documented and the user requested this checker direction; inspect available local Python and set a bounded fixture/resource budget. No numbered project or container runtime is a prerequisite for this CLI stage.
- Included behavior: record Python/tool versions, package/build/dependency choices, CLI invocation and report formatting; create the src-layout package skeleton, pyproject.toml, declared dev tools, synthetic fixtures and fixture-based acceptance test skeleton.
- Exclusions: checker feature implementation, API, worker, database, containers and paid services.
- Allowed change area: this project folder.
- Acceptance checks and expected results: environment and package skeleton can be bootstrapped using recorded commands; test discovery and tooling run; unimplemented behavior is explicitly red or pending rather than falsely passed.
- Domain/methodological checks: fixtures must match the PROJECT.md contract; keep environment readiness separate from data-quality acceptance.
- Decision owner: user owns scope; record routine local tooling choices with alternatives. Escalate changes involving paid services, sensitive data, restrictive licenses or material hardware commitments.
- Evidence location: VERIFICATION.md with retained environment/tooling outputs; add exercised commands to AGENTS.md.
- Evidence records: none

## TASK-003: Deliver the command-line checker — Preproject A

- Status: proposed
- Requirement IDs: CSV-001 through CSV-007, PRE-A, PRJ-004
- Dependencies: TASK-002 environment and test skeleton available.
- History: the initial TASK-003 combined Preprojects A-B; this revision limits TASK-003 to A and routes B to TASK-004.
- Included behavior: implement the typed parser/checker/report contract, CLI, representative and edge-case tests; add formatting/lint/type/pre-commit checks and justify a coverage target; build a wheel and exercise it in a fresh environment outside the source directory.
- Exclusions: API/worker, persistence, containers, custom schemas, repair, numeric validation, ML and performance optimization.
- Allowed change area: this project folder.
- Acceptance checks: valid fixture yields exit 0; quality defects yield exact counts and exit 1; missing columns yield explicit names; parsing/access errors yield helpful diagnostics and exit 2; built package installs and its CLI/public API work independently of the source checkout.
- Negative gate: temporarily introduce a counting or exit-code defect; the relevant acceptance check must fail, then restore correct behavior and retain the failure and recovery evidence.
- Domain/methodological checks: exercise whitespace, blank IDs, repeated IDs, header-only files and inconsistent row widths against the specified semantics. Record agent interventions and rework without inferring a workflow winner.
- Evidence location: VERIFICATION.md, revision-bound check outputs and package/install records.
- Evidence records: none

## TASK-004: Deliver the API and worker — Preproject B

- Status: proposed
- Requirement IDs: PRJ-003, PRE-B
- Dependencies: TASK-003 proven; local container runtime/resource readiness confirmed; recorded API, job-state, persistence and recovery decision.
- Included behavior: accept a CSV checking job through FastAPI, process it in a worker using the proven checker, retain job/report state and retrieve results. Build a handwritten multi-stage, non-root image and multi-service Docker Compose setup with an asynchronous or stateful dependency.
- Exclusions: Kubernetes, Kafka/Spark/Airflow, public hosting, authentication, multi-agent orchestration and new CSV rules.
- Allowed change area: this project folder.
- Acceptance checks: complete request-to-worker-to-report workflow; invalid submission diagnostic; declared failure/recovery scenario; internal networking, named volume, configuration separation, readiness/health checks, log inspection and interactive debugging; restart/rebuild state behavior; measured initial-versus-optimized image size.
- Domain checks: processing completion and data-quality PASS are distinct; duplicate processing, retry and retention must follow the recorded contract.
- Evidence location: VERIFICATION.md with evaluated Compose/image versions, requests, logs, measurements and recovery results.
- Evidence records: none.

## TASK-005: Extract the reusable engineering baseline

- Status: proposed
- Requirement IDs: PRJ-004, PRJ-006
- Dependencies: TASK-003 and TASK-004 proven; refine this task before starting.
- Included behavior: CI/release gates, reusable repository/specification/ADR/task templates, coding-agent guide, testing standards, runbook and concise engineering handbook based on the delivered checker.
- Acceptance checks: fresh-start quickstart and scripted demo; a broken contract fails the completion gate; extracted baseline can be followed without private KMS access; public evidence package links claims to results and limitations.
- Methodological boundary: include draft stochastic specification/evaluation/release templates required by the master plan, but do not claim they were validated by this deterministic checker.
- Exclusions: adoption of the global draft harness standard and new runtime product features.
- Evidence records: none.

## TASK-006: Compare two agent-assisted workflows

- Status: proposed
- Requirement IDs: PRJ-005, PRJ-006
- Dependencies: a stable checker baseline and TASK-005 gates; predeclare a bounded comparison contract before collecting results.
- Included behavior: compare specification-first coding with specification + tests + independent review on small comparable changes from equivalent starting snapshots. Keep requirements, agent/model versions and resource/time budgets declared; use isolated copies and independent acceptance checks.
- Measurements: elapsed implementation time, defects/test failures, rework, human interventions, code complexity/maintainability assessment and tokens/cost when available. Mark unavailable measurements explicitly.
- Acceptance checks: retain task definitions, workflow conditions, inputs, actual outputs and limitations; account for task difficulty and execution-order effects. A small comparison supports a local retrospective, not a general superiority claim.
- Exclusions: paper-scale benchmarking, autonomous loops and changing product acceptance rules to favor a workflow.
- Evidence records: none.

<!-- BEGIN GENERATED MASTER-PLAN SEED -->
## Master-plan backlog seed

- Canonical seed: [Justin_Arce_Portfolio_Master_Plan.md](../Justin_Arce_Portfolio_Master_Plan.md), locator: `# 0. Portfolio Foundation - Vibe Coding Lab`.
- Portfolio role: Learning foundation and reusable engineering baseline.
- Planning state: Start here. This is sequencing metadata, not implementation evidence.
- Shared constraints: local-first, open-source-first, portable interfaces, explicit contracts, observable failure and reproducible evidence.

| Seeded backlog item | Initial status | Entry condition |
| --- | --- | --- |
| A typed reference service and worker | proposed | refine under the first eligible bounded task before implementation |
| Reusable specification, ADR and task-contract templates | proposed | refine under the first eligible bounded task before implementation |
| CI, container and release-gate baseline | proposed | refine under the first eligible bounded task before implementation |
| A measured comparison of at least two agent-assisted workflows | proposed | refine under the first eligible bounded task before implementation |
| Local Systems Preproject A: an installable typed Python package and CLI | proposed | refine under the first eligible bounded task before implementation |
| Local Systems Preproject B: an optimized FastAPI multi-service Docker Compose build | proposed | refine under the first eligible bounded task before implementation |
| Initial ownership of reusable cross-portfolio harness patterns | proposed | refine under the first eligible bounded task before implementation |

These rows are a coverage inventory, not accepted task contracts. Promote only the next eligible row into a stable TASK identifier with exclusions, allowed change area, acceptance checks, decision owner and evidence locations.
<!-- END GENERATED MASTER-PLAN SEED -->

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

# Vibe Coding Lab: architecture

## Current state

The requested reference application is a CSV Data Quality Checker. Its three delivery stages are specified; runtime versions, packaging tools, job persistence and recovery mechanisms have not been selected or exercised. This is a draft design, not a diagram of running software.

## Staged components and flow

| Stage | Components | Boundary |
| --- | --- | --- |
| 1 | CSV parser, checker core, report renderer and CLI | Local file -> validated records -> quality report -> text and exit code |
| 2 | FastAPI API, worker and persistent job/report store | Submit CSV -> queued job -> worker calls the same core -> retained report -> retrieve job status/report |
| 3 | CI, release gate, templates, handbook and workflow evidence | Reproduce delivery, reject broken contracts and compare declared agent workflows |

Keep checks in a typed Python API usable independently of the CLI. Parsing errors are distinct from readable data that fails quality rules. The core owns the counting and quality result; the CLI owns file access, diagnostics and exit codes. Stage 2 reuses the same checker rather than maintaining another implementation.

The stage 2 job lifecycle is a candidate contract: `queued -> running -> completed` or `failed`. A completed job may contain a FAILED data-quality report; job failure means processing could not complete. Select persistence, ownership, retry and restart behavior in a recorded decision before service implementation. The Compose application must eventually include a stateful or asynchronous dependency and a named persistent volume.

## Required invariants

- The core workflow remains reproducible from declared inputs and versions.
- Interfaces, data/model contracts and failure behavior are explicit.
- Observability identifies the run, inputs, configuration, outcome and failure.
- Public operation does not depend on private KMS access.
- Domain validity is evaluated separately from successful software execution.
- Counts and exit codes agree with the canonical behavior contract in [PROJECT.md](PROJECT.md), including blank and duplicate-ID handling.
- Runtime checks are deterministic. Using a coding agent to create the application does not make the checker itself a stochastic feature.
- A future worker may report completion only after its report is retained; recovery and duplicate-processing behavior require an explicit contract and executed evidence.

## Decisions to record

- Runtime, dependency and packaging choices
- Data/model/source identity and license constraints
- Component boundaries and contracts
- Persistence, recovery and retention strategy
- Verification layers and release gates
- Security, privacy and resource boundaries

## Decisions in delivery order

1. TASK-002: inspect the local Python runtime; choose and pin packaging/dependency tools, CLI entry point, report format, formatting/lint/type/test tooling and a bounded fixture size. Record alternatives and consequences here or in a linked ADR.
2. TASK-003: implement a `src/` package with `pyproject.toml`, typed checker API, CLI and fixtures. Justify the coverage target from the meaningful branches in the contract.
3. TASK-004: decide upload limits, API contracts, job/state identifiers, persistence, worker coordination, retry/recovery and retention before adding FastAPI and Compose. Containers require a local readiness/resource check at this stage, not as a stage 1 prerequisite.
4. TASK-005: extract CI gates and reusable templates from the working implementation.
5. TASK-006: predeclare comparable tasks, workflow conditions, budgets, timing and defect measures before collecting comparison outcomes.

No external repository split is pending: implementation remains in this project folder under the current storage instruction. Revisit only if the user requests a change.

<!-- BEGIN GENERATED MASTER-PLAN SEED -->
## Master-plan architecture seed

- Canonical seed: [Justin_Arce_Portfolio_Master_Plan.md](../Justin_Arce_Portfolio_Master_Plan.md), locator: `# 0. Portfolio Foundation - Vibe Coding Lab`.
- Portfolio role: Learning foundation and reusable engineering baseline.
- Planning state: Start here. This is sequencing metadata, not implementation evidence.
- Shared constraints: local-first, open-source-first, portable interfaces, explicit contracts, observable failure and reproducible evidence.

| Candidate component or boundary | Status | Evidence needed before adoption |
| --- | --- | --- |
| Reference API and worker | candidate | decision and executed evidence required |
| Installable typed Python package and CLI | candidate | decision and executed evidence required |
| Multi-stage, non-root FastAPI Docker image and multi-service Compose profile | candidate | decision and executed evidence required |
| Reusable repository template | candidate | decision and executed evidence required |
| CI and quality gates | candidate | decision and executed evidence required |
| Workflow experiment and evidence store | candidate | decision and executed evidence required |

### Cross-cutting interfaces to resolve

- Versioned input, output, configuration and state contracts.
- Run, data, model or agent identifiers that connect execution to logs, metrics, traces and retained evidence.
- Explicit startup, readiness, failure, retry, recovery and rollback behavior.
- Portable adapters at external service boundaries; private KMS access must not be required to operate a public artifact.
<!-- END GENERATED MASTER-PLAN SEED -->

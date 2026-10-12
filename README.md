# Vibe Coding Lab

**Agent-assisted software engineering under explicit quality standards.**

Vibe Coding Lab explores how to turn work produced with coding agents into reproducible, tested software. A small CSV Data Quality Checker provides the reference application for developing specifications, acceptance tests, review practices and delivery automation.

The planned outputs are a working application, a reusable project baseline and a measured retrospective on two agent-assisted development workflows.

> **Status: planning phase.** The application contract and delivery roadmap are documented. Implementation has not started; no installable package, runnable quickstart, container build or workflow results are available yet.

## Why this project exists

Coding agents can produce changes quickly, but a software project also needs explicit behavior, checks that catch defects, understandable design decisions and a setup others can reproduce. This lab will investigate how those practices affect delivery time, defects, rework and human intervention on bounded software tasks.

Results will be tied to declared tasks, tool versions, starting snapshots and resource budgets. Any conclusions will be limited to the evaluated workflows and tasks.

## Reference application

The first planned release is a local command-line CSV checker with a typed Python API. It will check:

- Required columns: `id` and `value` must be present.
- Missing required values: blank cells are counted after trimming surrounding whitespace.
- Duplicate IDs: repeated nonblank IDs are counted beyond their first occurrence.

Additional columns are allowed. IDs are compared as case-sensitive strings. Numeric validation, automatic repair, custom schemas and large-file performance guarantees are outside the initial scope.

### Expected behavior

Given this input:

```csv
id,value
1,10
2,
2,30
4,40
```

the specified result is:

```text
Rows checked: 4
Missing required cells: 1
Duplicate IDs: 1
Result: FAILED
```

This is a specification example, not captured application output. Exact report formatting will be finalized during implementation. The full behavior contract is in [PROJECT.md](PROJECT.md).

| Exit code | Planned meaning |
| ---: | --- |
| 0 | File passes the declared quality checks |
| 1 | Readable, structurally valid CSV fails quality checks |
| 2 | Invocation, file-access, encoding or CSV parsing error |

## Installation and usage

Installation instructions and verified commands will be published after the first package has been built and exercised in a fresh environment. The intended first workflow is to provide a local UTF-8 CSV file and receive a quality report through the command-line interface.

There is currently no released application to install or run.

<!-- BEGIN GENERATED MASTER-PLAN SEED -->
<!-- Canonical plan locator: Justin_Arce_Portfolio_Master_Plan.md, # 0. Portfolio Foundation — Vibe Coding Lab. Planning provenance and portfolio ownership are retained in PROJECT.md. -->
## Roadmap

| Milestone | Planned deliverables | Status |
| --- | --- | --- |
| Command-line checker | Installable typed Python package, deterministic reports, acceptance tests and clean-environment installation evidence | Specified; not implemented |
| API and worker | FastAPI job submission, background processing, retained reports, multi-service Docker Compose and recovery checks | Planned |
| Reusable engineering baseline | Repository/specification/architecture-decision templates, agent instructions, testing guidance, CI/release gates and runbooks | Planned |
| Workflow comparison | Declared comparison of specification-first coding and specification + tests + independent review, with measurements and limitations | Planned |

The reference path is intended to run locally, favor open-source tooling and use portable component interfaces. Later delivery stages will reuse the checker core.

The broader baseline includes draft specification, evaluation and release templates for stochastic ML/AI systems. Those templates will require validation on suitable systems; this deterministic checker will not establish their effectiveness.
<!-- END GENERATED MASTER-PLAN SEED -->

## Verification and results

No application or workflow results have been collected. Planned evidence includes:

- Correct reports for valid data, missing columns, missing cells and duplicate IDs.
- Useful diagnostics for malformed or unreadable files.
- Installation and execution outside the source directory in a fresh environment.
- A deliberately introduced code defect rejected by an acceptance check, followed by recovery.
- An API-to-worker-to-report demonstration, container measurements and retained-state recovery.
- Workflow measurements covering time, defects, rework and human interventions, with tokens/cost when available.

[VERIFICATION.md](VERIFICATION.md) tracks the acceptance requirements and will retain links to results tied to evaluated versions. Documentation checks do not establish application correctness.

## Development and documentation

The development sequence is specification, tests, agent-assisted implementation, review and executed checks. Coding-agent assistance and human corrections will be recorded alongside results.

| Document | Purpose |
| --- | --- |
| [PROJECT.md](PROJECT.md) | Scope, behavior contract and acceptance criteria |
| [ARCHITECTURE.md](ARCHITECTURE.md) | Component boundaries, invariants and design decisions |
| [TASKS.md](TASKS.md) | Bounded work items and dependencies |
| [AGENTS.md](AGENTS.md) | Contributor and coding-agent guidance; exercised commands when available |
| [VERIFICATION.md](VERIFICATION.md) | Acceptance requirements and executed evidence |
| [PROGRESS.md](PROGRESS.md) | Current delivery state and handoff |
| [WALKTHROUGH.md](WALKTHROUGH.md) | Guided learning path through the reference project |

The current development milestone is package and environment bootstrap. Contributors should consult the task register for scope and dependencies before beginning a change.

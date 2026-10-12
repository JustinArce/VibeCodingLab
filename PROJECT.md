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
repository: "."
---

# Vibe Coding Lab

## Objective

Build a CSV Data Quality Checker and use its delivery to establish an evidence-backed method for agent-assisted software engineering. The product checks small local CSV files; the lab records specifications, tests, review, CI, containers and observed results that later projects can reuse.

## Direction and provenance — 2026-10-10

The assistant proposed a CSV Data Quality Checker with three stages: command-line checker, API/worker service, and reusable engineering baseline. The user then requested that the README and all harness components be updated accordingly. This records the requested project direction, not a human review event or implementation evidence. The detailed contract below is a draft elaboration of that direction.

This planned build realizes the master plan's `# 0. Portfolio Foundation — Vibe Coding Lab` and `## Preproject A — Installable Python Package and CLI`; the planned service stage covers `## Preproject B — Container Build and Compose Foundations`.

## Users and first-stage boundaries

- User: a learner or developer checking a small local dataset before using it in another project.
- Input: a local UTF-8, comma-delimited CSV file with one header row and required columns `id` and `value`. Additional columns are allowed and ignored by the three checks.
- Output: a deterministic text report containing row count, missing required columns, missing required cell count, duplicate ID count and overall status. Malformed or unreadable files produce a useful diagnostic.
- Data: synthetic fixtures committed with the future implementation; no private datasets or external services are needed.
- Initial exclusions: UI, authentication, cloud deployment, streaming, arbitrary user-defined schemas, numeric/type validation, automatic data repair, ML/LLM runtime features, large-file performance claims and autonomous agent orchestration.

## Stage 1 behavior contract

| Rule | Planned behavior |
| --- | --- |
| Header | Require exactly one occurrence of each required column; reject duplicate column names. Header names are case-sensitive and are not silently normalized. |
| Rows | Count parsed data records, excluding the header and completely blank lines. Reject records whose field count differs from the header. A header-only file is valid and has zero data rows. |
| Missing columns | Report missing required column names in sorted order; mark the result FAILED. Skip cell and duplicate counts and render them as not evaluated. |
| Missing values | After trimming surrounding whitespace, an empty `id` or `value` counts as one missing required cell. A row missing both counts as two. |
| Duplicate IDs | Compare trimmed, nonblank IDs as case-sensitive strings. Count occurrences beyond the first: three copies of one ID count as two duplicates. Blank IDs contribute only to missing-cell counts. |
| Result | PASS requires both columns present, zero missing required cells and zero duplicate IDs. Otherwise report FAILED. |
| Exit codes | `0`: data passes; `1`: readable, structurally valid CSV fails quality checks; `2`: invocation, file-access, encoding or structural parsing error. Error diagnostics must identify the cause without exposing private file contents. |

Planned acceptance fixtures:

| Fixture | Expected result |
| --- | --- |
| `id,value` followed by `1,10` and `2,20` | 2 rows, 0 missing cells, 0 duplicate IDs, PASS, exit 0 |
| `id,value` followed by `1,10`, `2,`, `2,30`, `4,40` | 4 rows, 1 missing cell, 1 duplicate ID, FAILED, exit 1 |
| Header `id` followed by `1` | Missing column `value`, other checks not evaluated, FAILED, exit 1 |
| Duplicate headers, invalid UTF-8, inconsistent row width, malformed quoting or unreadable file | Useful diagnostic, exit 2 |

CLI name, exact invocation, report formatting and runtime/tool versions are resolved in TASK-002 and recorded before implementation relies on them.

## Scope

- Stage 1: typed checker core, installable Python package and CLI (Preproject A)
- Stage 2: FastAPI job API and worker sharing the checker core, retained job/report state, and optimized Docker Compose build (Preproject B)
- Stage 3: reusable development baseline and a measured comparison of at least two agent-assisted workflows
- Reusable specification, ADR and task-contract templates
- CI, container and release-gate baseline
- Initial ownership of reusable cross-portfolio harness patterns

## Working repository

This directory is the working home inside the KMS. Keep implementation, project context and evidence here unless the user explicitly changes that storage decision.

## Relevant KMS guidance

- [Portfolio Project Harness](../PORTFOLIO_HARNESS.md)
- [Project Harness Standard](../../10_Standards/Project_Harness_Standard.md) — draft and unadopted.
- [Bootstrap playbook](../../20_Playbooks/Project_Harness_Bootstrap.md) — draft procedure.

## Dependencies

- No numbered portfolio project is a prerequisite.
- Use the [Portfolio Project Harness](../PORTFOLIO_HARNESS.md) as draft guidance without claiming that its global standard has been adopted.
- This project produces the engineering baseline and Preprojects A-B required by projects 02 and 03.

## Acceptance criteria

- A fresh contributor can follow documented setup and obtain the declared smoke result.
- One representative complete workflow proves the project's core portfolio claim.
- Core requirements map to current checks and retained evidence.
- A deliberately broken contract or test must fail the completion gate with a useful diagnostic.
- The public README states results, limitations, reproduction steps and the role of AI assistance.
- Stage 1 satisfies the behavior contract and installs from a built artifact into a clean environment outside the source directory.
- Stage 2 retains job/report state across the declared restart scenario and proves the master plan's image, networking, volume, health, debugging and recovery requirements.
- Stage 3 retains a bounded workflow comparison and reusable artifacts based on observed delivery experience. Stochastic specification/evaluation/release templates remain draft examples until exercised on a later stochastic system.

## Status and next action

Draft checker contract; no implementation or runtime verification has occurred. Next: TASK-002, inspect the local Python runtime and record package, CLI and development-tool choices, then establish the stage 1 bootstrap and fixture/test skeleton.

## Lessons

Capture reusable observed experience in 70_Lessons only after implementation produces evidence.

<!-- BEGIN GENERATED MASTER-PLAN SEED -->
## Master-plan traceability seed

- Canonical seed: [Justin_Arce_Portfolio_Master_Plan.md](../Justin_Arce_Portfolio_Master_Plan.md), locator: `# 0. Portfolio Foundation - Vibe Coding Lab`.
- Portfolio role: Learning foundation and reusable engineering baseline.
- Planning state: Start here. This is sequencing metadata, not implementation evidence.
- Shared constraints: local-first, open-source-first, portable interfaces, explicit contracts, observable failure and reproducible evidence.

| Planned workstream | Local owner | Current evidence state |
| --- | --- | --- |
| A typed reference service and worker | ARCHITECTURE.md and TASKS.md | planned; no implementation evidence |
| Reusable specification, ADR and task-contract templates | ARCHITECTURE.md and TASKS.md | planned; no implementation evidence |
| CI, container and release-gate baseline | ARCHITECTURE.md and TASKS.md | planned; no implementation evidence |
| A measured comparison of at least two agent-assisted workflows | ARCHITECTURE.md and TASKS.md | planned; no implementation evidence |
| Local Systems Preproject A: an installable typed Python package and CLI | ARCHITECTURE.md and TASKS.md | planned; no implementation evidence |
| Local Systems Preproject B: an optimized FastAPI multi-service Docker Compose build | ARCHITECTURE.md and TASKS.md | planned; no implementation evidence |
| Initial ownership of reusable cross-portfolio harness patterns | ARCHITECTURE.md and TASKS.md | planned; no implementation evidence |

This table establishes local planning ownership only. It does not adopt the draft global harness standard, select the implementation stack, or establish that any workstream is runnable or verified.
<!-- END GENERATED MASTER-PLAN SEED -->

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

Create a reusable, evidence-backed method and repository baseline for building software with coding agents under explicit specifications, architecture, tests, review, CI, containers and observability.

## Scope

- A typed reference service and worker
- Reusable specification, ADR and task-contract templates
- CI, container and release-gate baseline
- A measured comparison of at least two agent-assisted workflows
- Local Systems Preproject A: an installable typed Python package and CLI
- Local Systems Preproject B: an optimized FastAPI multi-service Docker Compose build
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

## Status and next action

Draft scaffold; no implementation or verification has occurred. Next: Define one small reference service, its users, non-goals and observable acceptance demo before selecting implementation details.

## Lessons

Capture reusable observed experience in 70_Lessons only after implementation produces evidence.


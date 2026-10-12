---
type: project
epistemic_status: unverified
authority: none
lifecycle: draft
domain: [software-engineering, data-engineering, artificial-intelligence]
topics: [agent-assisted-development, specification-driven-development, test-driven-development, data-quality]
sources: ["PROJECT.md", "TASKS.md", "ARCHITECTURE.md", "VERIFICATION.md", "../Justin_Arce_Portfolio_Master_Plan.md"]
human_reviewed: false
reviewed:
---

# Vibe Coding Lab: your guided walkthrough

You are learning how to take an idea, work with a coding agent, check its work and deliver a program another person can use. The CSV checker gives you a small project on which to practice those skills. The reusable result is your way of working, supported by the program and the evidence you collect.

This is a draft learning guide requested by the user on 2026-10-10. It follows the local checker contract and task register; it does not report completed implementation. All sample results below are expectations. Exact setup and application commands will be documented after they are selected and exercised.

## Your role throughout the lab

You decide what the program should do and judge whether its results make sense. The coding agent can explain options, create files, write code and tests, run checks and help diagnose mistakes. Ask it to explain choices you do not understand, and inspect one small change at a time.

The learning loop is:

1. Describe one behavior and its expected result.
2. Create a check that would catch an incorrect result.
3. Use the agent to implement that behavior.
4. Inspect the result and the check output.
5. Record corrections and what you would reuse next time.

Keep a short work log as you go: task, agent/tool version, measured time when available, corrections you requested, observed defects, check-output locations and one lesson. Distinguish observed results from estimates. The formal workflow comparison comes later.

## Step 1: understand what you are asking the program to do

**Your action:** read these three examples and work out the expected answers yourself before asking an agent to write tests.

Clean file:

```csv
id,value
1,10
2,20
```

Expected: 2 rows, 0 missing required cells, 0 duplicate IDs, PASS.

File with quality problems:

```csv
id,value
1,10
2,
2,30
4,40
```

Expected: 4 rows, 1 missing required cell, 1 duplicate ID, FAILED. The second data row has an empty value; ID `2` occurs twice, so there is one occurrence beyond its first appearance.

File missing a required column:

```csv
id
1
```

Expected: report the missing `value` column, FAILED; cell and duplicate checks are not evaluated.

A quality-failing report can be the correct output of a correctly working checker. Later, you will separately prove that your tests reject incorrect program behavior.

**What you learn:** turn a general idea into specific, independently understandable examples. This is the practical starting point of specification-driven development.

**Ready to move on when:** you can explain the three expected results and understand the detailed counting rules in [PROJECT.md](PROJECT.md), under "Stage 1 behavior contract." That file is the canonical contract; this walkthrough explains it.

## Step 2: set up a small place to build it — TASK-002

**Your action:** have the agent inspect the available Python runtime, explain a simple packaging/tooling choice, and set up the package skeleton, environment, example files and test skeleton. Keep implementation in this project folder.

You can give it this prompt:

> Work on Vibe Coding Lab TASK-002. Read the local harness and inspect the available Python runtime. Explain and record a simple package, CLI and development-tool setup. Create the package skeleton, synthetic CSV fixtures and acceptance test skeleton from PROJECT.md. Exercise the setup and test discovery, record actual results and exact commands, and leave checker behavior for TASK-003. Explain what each created file is for.

The CLI is the command you will eventually run to check a file. A package is the installable collection of code behind it. Tests are small programs that compare actual behavior with expected behavior.

**What you learn:** make setup reproducible and understand where the code and checks belong.

**Ready to move on when:** the environment starts, tests can be discovered, the setup choices are recorded, and you can explain the purpose of the main files. Unimplemented checks may fail or be explicitly pending; a working setup does not mean the checker works.

## Step 3: build one behavior at a time — TASK-003

Start with the clean-file result. Then handle missing required columns, missing cells, duplicate IDs and file/parsing errors. Use the full contract for edge cases and precedence.

For each small behavior, ask the agent to define the expected check before implementing it. Run the check against the unfinished or incorrect behavior, observe the failure, implement the behavior, and run the checks again. Keep earlier checks so later changes cannot silently break previous behavior.

Example prompt:

> Work on TASK-003 using the recorded setup. Begin with the clean-file acceptance case from PROJECT.md. Add a meaningful test, show that it fails because the required behavior is absent, implement the smallest coherent behavior, and rerun the relevant checks. Explain the result before moving to the next rule. Preserve the full CSV contract and keep the API and containers for later tasks.

**Your action:** compare outputs with your hand-worked examples. Ask why a failure happened. For duplicate IDs, also inspect a case with three copies: it must count two duplicates. For missing cells, a row missing both required values must count two.

**What you learn:** use tests to guide implementation and corrections, and hold an agent's work to expectations defined independently of its code.

**Ready to move on when:** the checker implements all the stage 1 rules, meaningful edge cases pass, and formatting, lint and type checks produce recorded results. The full acceptance map is in [VERIFICATION.md](VERIFICATION.md).

## Step 4: make the program usable outside your development folder

**Your action:** have the agent build the installable package, install it into a fresh environment, and run its public Python API and CLI from outside the source directory.

The CLI must communicate three outcomes:

| Outcome | Meaning | Exit code |
| --- | --- | ---: |
| PASS | The file passes the declared quality rules | 0 |
| FAILED | The file can be read, but has quality problems | 1 |
| Error | The invocation, file access, encoding or CSV structure prevents checking | 2 |

An exit code is the number returned to other programs so they can distinguish those outcomes automatically.

Have the agent also demonstrate that a deliberately introduced counting or exit-code defect causes the relevant acceptance check to fail. Use an isolated temporary copy or reversible change, restore correct behavior, and retain both rejection and recovery results.

**What you learn:** delivery includes installation, useful errors and checks that actually catch bad code.

**Stage 1 is demonstrated when:** the built package runs in the fresh environment, valid and faulty fixtures produce their specified reports and exits, file/parsing errors are useful, and the deliberate code defect is rejected. Record versions, procedure and actual outputs in VERIFICATION.md, and update PROGRESS.md.

Pause here and review what you built. You now have the first working portfolio artifact and a full example of your development loop.

## Step 5: give the checker a service interface — TASK-004

Once the package is proven, extend it so another program can submit a CSV checking job and retrieve its result. The API receives requests; a worker processes jobs using the same checker; persistent storage keeps job status and reports.

**Your action:** first ask the agent to explain the proposed flow and the decisions needed for job storage and recovery. Then implement one submission-to-result path. Use Docker Compose to start the components together after container readiness and resources are checked.

Test a normal job and a declared failure/recovery case. Show which state survives a restart. Keep a completed job with dirty data distinct from a job that failed to process. Measure the initial and optimized container image sizes as required by Preproject B.

**What you learn:** coordinate components, make state and failures visible, and prove that restart behavior matches your design.

**Ready to move on when:** the request-to-report workflow, container setup, health checks, persistence and declared recovery scenario have executed evidence. Refine the task before starting; these mechanisms are currently unresolved.

## Step 6: keep the parts that will help your next project — TASK-005

Look back at the working delivery process. Extract the project starting point, specification and architecture-decision templates, agent instructions, automated checks, setup guide and runbook. CI means running the declared checks automatically when code changes.

**Your action:** ask of each reusable artifact: what real problem did this help solve, and can another person follow it without this chat or private KMS access? Demonstrate the extracted setup and make sure its completion gate rejects a broken contract.

The master plan also calls for templates for stochastic ML/AI systems. Those remain draft examples until exercised on an appropriate system; the deterministic CSV checker cannot prove their validity.

**What you learn:** turn observed experience into a useful starting point for later software projects.

**Ready to move on when:** the setup, checks, templates and public evidence agree with the delivered implementation, and you can explain the remaining limits.

## Step 7: compare ways of using the coding agent — TASK-006

With a stable baseline, choose small comparable changes and compare the two declared workflows: specification-first coding, and specification plus tests plus independent review. Define the comparison before running it.

Keep starting snapshots, requirements, budgets, agent/tool versions and independent acceptance checks explicit. Account for task difficulty and execution order. Record elapsed time, defects, rework and your interventions; include tokens/cost only when available.

**Your action:** explain which workflow helped for these particular tasks and what the evidence does not establish. A small comparison supports your local working choices; it cannot establish a universal winner.

**What you learn:** choose your working practices using observed results.

## Where to look when you get stuck

| Your question | Read |
| --- | --- |
| What should the checker do? | [PROJECT.md](PROJECT.md) |
| Why is it organized this way? | [ARCHITECTURE.md](ARCHITECTURE.md) |
| What is the next bounded task? | [TASKS.md](TASKS.md) |
| How do I run the exercised commands? | [AGENTS.md](AGENTS.md), once commands exist |
| What has actually been checked? | [VERIFICATION.md](VERIFICATION.md) |
| Where did we stop? | [PROGRESS.md](PROGRESS.md) |

Your next implementation task is TASK-002. Start with the setup prompt in Step 2, and use Step 1's examples to keep the purpose of that setup concrete.

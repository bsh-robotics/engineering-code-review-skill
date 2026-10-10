---
name: engineering-code-review
description: Use when reviewing, designing, implementing, refactoring, or verifying code in an existing project where system context, modular boundaries, staged execution, or evidence-backed conclusions matter.
---

# Engineering Workflow and Code Review

Use this skill as the default engineering workflow for repository work. Start from the real system context, define boundaries before editing, keep modules cohesive, validate behavior in stages, and keep conclusions within the evidence. Separate **review mode** from **implementation mode**; do not scan the entire project for an ordinary small edit unless the user asks for a project-wide review.


## General engineering principles

Apply these principles in both modes:

- Understand the existing system before changing it: identify real entry points, callers, data flow, configuration sources, side effects, and failure paths.
- Treat documentation, comments, plans, and tests as claims or partial evidence. Confirm behavior through the actual execution path.
- Define module responsibilities, interfaces, inputs, outputs, state ownership, and error contracts before adding logic. Avoid hidden global state and oversized files or functions.
- After a local change, inspect its callers, downstream consumers, alternate paths, compatibility surfaces, configuration, scripts, and tests.
- Design failure, timeout, retry, cleanup, rollback, partial-success, and resource-exhaustion behavior as part of the feature.
- Keep changes traceable and reversible. Separate unrelated refactors from functional changes and record assumptions that remain unverified.
- Match the conclusion to the evidence: compilation, importability, unit tests, integration tests, runtime checks, data checks, and production or hardware validation prove different things.

## Choose the mode

- **Review mode** applies when the user asks to review, audit, understand, assess, or verify code. Read the repository structure first, then trace the complete code tree for the requested feature.
- **Implementation mode** applies when the user asks to add, change, refactor, or fix code. Inspect the target modules, their local conventions, and their callers before editing.
- If both are requested, finish the review deliverable before implementation.

## Non-negotiable workflow

1. State the selected mode, scope, assumptions, and evidence still missing.
2. In review mode, inspect the project tree and trace the feature through entry points, imports, configuration, data contracts, side effects, error paths, tests, scripts, and runtime writes. Treat comments, README files, and planned behavior as claims to verify, not as proof.
3. Before coding, decide whether external research is needed. Search GitHub, papers, official documentation, or other primary sources only when the task involves a new technology, complex algorithm, architecture design, or an unclear existing solution. Record each query or URL, source date/version when available, the decision it informed, and any disagreement between sources.
4. If a plan, issue, or design document exists, translate it into ordered checkpoints with a success criterion, validation command or observation, affected files, and a stop/escalation condition. Do not skip ahead: finish and verify one checkpoint before starting the next.
5. Produce a read-only analysis and implementation plan for user review before making code changes. Treat approval as an explicit user message; until it arrives, do not edit, generate patches, run mutating commands, or continue implementation.
6. Implement in cohesive modules with narrow responsibilities and explicit interfaces. Follow the repository's existing package, import, configuration, error-handling, and test conventions. Avoid placing unrelated behavior in one file or one oversized function.
7. After each checkpoint, run the smallest meaningful validation and report what the evidence proves. Keep static review, tests, runtime smoke, data/sample inspection, and hardware or closed-loop evidence distinct. If dynamic registration, reflection, plugin metadata, generated code, environment variables, or CLI wrappers affect the path, include them in the validation surface.
8. Before claiming completion, report changed files, validation commands and results, repository revision or relevant environment, remaining uncertainty, and any evidence that was not obtained.

## Output contract

For review mode, return: scope and tree examined; call-chain/data-flow findings; confirmed issues with file and line evidence; risks and missing evidence; prioritized recommendations; and a staged plan if changes are requested.

For implementation mode, return: pre-change analysis; approved checkpoints; changes grouped by module; validation per checkpoint; and an evidence-bounded completion report.

Read [references/review-mode.md](references/review-mode.md) for the repository-wide review checklist. Read [references/implementation-mode.md](references/implementation-mode.md) for modular implementation and checkpoint rules.

## Stop conditions

Stop and ask the user when the requested scope is ambiguous, a plan conflicts with repository behavior, required evidence is unavailable, or a destructive/external action is outside the user's authorization. Do not silently widen scope or convert a passing unit test into a claim of end-to-end success.

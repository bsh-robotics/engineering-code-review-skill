# Implementation mode checklist

Use this mode for new features, fixes, refactors, migrations, and other code changes.

## Before editing

- Identify the smallest complete change surface and the existing conventions it must preserve.
- Define the responsibility and interface of each new or changed module before writing its internals.

- Read the relevant plan or issue and list ordered checkpoints.
- Inspect target modules, their public interfaces, callers, tests, configuration, and nearby patterns.
- For new technology, complex algorithms, architecture decisions, or unclear behavior, gather primary external references and state which decision each reference informs.
- Present the analysis, proposed module boundaries, file changes, risks, checkpoint success criteria, validation commands, and stop conditions for user review. Do not edit files until explicit approval arrives.

## While editing

- Keep each module responsible for one coherent concern. Make data flow and ownership explicit; do not use a large function as a substitute for module boundaries.
- Prefer explicit inputs and outputs over hidden shared state.
- Reuse existing interfaces and conventions unless the change explicitly updates the contract. If a contract changes, update all callers, adapters, configuration, tests, and documentation that depend on it.
- Separate functional changes, refactors, and test changes when possible. Keep unrelated cleanup out of the implementation checkpoint.
- Complete and validate one checkpoint before moving to the next. If validation fails, diagnose and resolve that checkpoint before proceeding; if the same blocker persists or requires a scope change, stop and report it for user direction.

## Failure and recovery

- Define expected behavior for invalid input, timeouts, retries, partial success, cleanup, rollback, and unavailable dependencies.
- When a checkpoint fails, preserve the failure evidence, fix the owning boundary, and re-run the checkpoint before moving forward. Do not hide the failure with a fallback that changes the contract silently.

## Validation report

For every checkpoint, record the command or observation, result, and what it proves. Distinguish static checks, focused tests, integration or runtime smoke, data/sample inspection, and hardware or closed-loop evidence. Report untested paths and unresolved assumptions instead of inferring success from loadability or a green unit test alone.

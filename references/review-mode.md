# Review mode checklist

## 1. Establish the surface

- Identify repository root, package boundaries, entry points, build/test commands, configuration, generated files, and active branches or worktrees when relevant.
- Use fast file and text search to map the target feature. Include source, tests, scripts, schemas, fixtures, migrations, deployment files, adapters, plugin or entrypoint metadata, generated-code sources, environment-variable reads, and CLI wrappers.
- Read the smallest complete set of files needed to establish the call chain, then expand until every boundary and side effect is accounted for. Check dynamic registration, reflection, import-time side effects, generated files and alternate configuration paths explicitly.

## 2. Trace behavior

For each path, record:

- caller and entry condition;
- inputs, transformations, outputs, and persistence or control writes;
- configuration and feature gates;
- retries, timeouts, cleanup, and failure handling;
- observable logs, metrics, artifacts, or runtime state;
- tests that actually exercise the path.

Compare intended behavior with production behavior. Flag dead code, bypasses, duplicated contracts, implicit globals, and claims supported only by comments or documentation.

## 3. Report findings

Each finding must include location, observed behavior, impact, confidence, and a concrete reproduction or evidence path when available. Separate:

- confirmed defect;
- design or maintainability risk;
- unverified hypothesis;
- missing validation.

Prioritize by user impact and failure likelihood. Do not recommend a broad rewrite when a focused boundary or contract fix is sufficient.

# AI Rules

These rules apply to any AI agent making changes in this repository.

## Non-negotiables

- Do not change licensing.
- Do not add dependencies without explicit instruction.
- Do not make silent behavior changes that contradict documented intent.
- Keep diffs small and reviewable.

## Required workflow

1. Propose a plan (files to change, risks, test/check plan).
2. Make changes.
3. Run relevant quality gates (format/validate/lint/test as applicable).
4. Report what you ran and what happened.
5. If something fails, stop and explain the failure with the most relevant logs.

## Documentation expectations

- Update docs when behavior changes.
- Keep README as the map, and put deep details in `docs/`.

## Commit expectations

- Use consistent, structured commit messages so changelog generation works.

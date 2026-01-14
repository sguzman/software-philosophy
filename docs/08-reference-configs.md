# Reference Configs and Patterns

This document is a scratchpad of recommended patterns.

## Repo-level patterns

- `README.md` as map
- `docs/` as depth
- `examples/` as runnable patterns

## Tooling patterns

- one place to define tool config
- CI runs the same checks developers run
- release process is documented and repeatable

## AI collaboration patterns

- "AI rules" doc is required
- changes are small and reviewable
- logs and checks are surfaced in PRs

## Deployment patterns

- one container per service
- compose for local stacks
- clear separation of config vs code

# Quality Gates

Quality gates are the checks that must pass before merging or releasing.

## Why gates exist

- prevent "format wars"
- catch invalid config early
- make CI predictable
- reduce reviewer burden

## Recommended baseline

- format:
  - TOML (taplo)
  - JS/TS/JSON (biome) where relevant
- validate:
  - TOML schema validation if available
  - config sanity checks (custom, small, fast)
- lint/static checks:
  - per-language if applicable
- tests:
  - unit/integration where applicable
- docs integrity:
  - lychee link checks

## Policy: small and strict

- prefer fewer gates that always run
- add new gates only if they pay rent
- keep them fast
- make failures actionable

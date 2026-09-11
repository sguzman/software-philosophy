# Operational Criticality

## Status

- Project criticality: `unknown | non-load-bearing | load-bearing`
- Last reviewed:
- Principal/director decision:

`unknown` does not mean safe to break. If credible evidence suggests active dependence, resolve criticality before invasive work.

## Load-bearing capabilities

List capabilities the principal currently depends on outside development itself.

| Capability | Criticality | Current verified runtime | Evidence / notes |
| --- | --- | --- | --- |
|  |  |  |  |

## Continuity envelope

The following capabilities must remain available while development proceeds:

- 

## Experimental surfaces

The following capabilities may regress on the development channel without violating continuity:

- 

## Runtime channels

### Stable / consumption

- branch/tag/version:
- filesystem/install path:
- runtime/profile/service identity:
- last verified candidate:

### Development

- branch:
- filesystem/install path:
- runtime/profile/service identity:

## Promotion gate

A development candidate may advance the stable channel only after:

1. 
2. 
3. 

- Explicit principal acceptance required: `yes | no`
- Strongest required evidence class:

## Recovery invariant

If development fails completely, the principal resumes the stable capability by:

1. 

This recovery should not require repairing development first.

## Shared-state / collision audit

See:

- `docs/project/collision-audit.md` or project-equivalent path.

## Discovery notes

Record evidence that caused criticality to be declared or reconsidered. Do not record private/sensitive details that are unnecessary to enforce the continuity contract.

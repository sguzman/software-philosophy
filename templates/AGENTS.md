# Agent Guide

The repository documentation is the system of record.

## Read before changing code

1. docs/project/philosophy.md
2. docs/project/product-scope.md
3. docs/project/priorities.md
4. ARCHITECTURE.md
5. docs/project/current-status.md
6. docs/project/roles-and-workflow.md
7. the active roadmap
8. the single authorized goal under docs/work/ready/ or docs/work/active/

## Roles

- Director / architect / integrator: owns philosophy, product scope, priorities, architecture, roadmap ordering, goal definitions, semantic review, and integration.
- Implementation worker: owns bounded implementation, directly related repair passes, validation, and durable reporting.
- Human maintainer: owns local operation and real-machine observations when requested. The human is not the normal communication courier.

## Scope discipline

- Implement only the authorized macro-goal.
- Respect every non-goal.
- Do not silently change architecture, product semantics, persistence contracts, or priority.
- Do not weaken tests to obtain green.
- Do not perform opportunistic broad rewrites.

## Worker autonomy

Continue through directly related diagnosis, implementation, repair, and retest loops already authorized by the goal.

Stop only when:
- acceptance gates pass;
- an explicit non-goal would be violated; or
- a true architectural ambiguity requires director input.

## Handoff

Commit and push enough evidence that the director can review without chat history.

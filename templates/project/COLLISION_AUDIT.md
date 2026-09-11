# Stable / Development Collision Audit

Use this when a verified stable channel and an experimental development channel coexist.

Classification vocabulary:

- `ISOLATED`
- `SHARED READ-ONLY`
- `SHARED MUTABLE / COORDINATED`
- `COLLISION-PRONE`
- `GLOBAL BUT ACCEPTABLE`
- `UNKNOWN`

| Surface | Stable identity | Dev identity | Classification | Concurrent use allowed? | Failure / cleanup risk | Mitigation / evidence |
| --- | --- | --- | --- | --- | --- | --- |
| Source/worktree |  |  |  |  |  |  |
| Install/runtime path |  |  |  |  |  |  |
| App/extension/plugin identity |  |  |  |  |  |  |
| Profile/user-data directory |  |  |  |  |  |  |
| Persistent storage/database |  |  |  |  |  |  |
| Runtime namespace / DOM / globals |  |  |  |  |  |  |
| Audio/device/global resource |  |  |  |  |  |  |
| IPC/ports/sockets |  |  |  |  |  |  |
| Native/OS registration |  |  |  |  |  |  |
| External service/cloud state |  |  |  |  |  |  |
| Uninstall/reset/cleanup |  |  |  |  |  |  |

## Unknown surfaces

Anything marked `UNKNOWN` remains an unverified isolation claim.

- 

## Simultaneous-activation rule

State what may safely coexist and what must not run concurrently.

- 

## Cleanup rule

State exactly what dev cleanup/uninstall may mutate and confirm that stable requirements survive it.

- 

## Recovery rule

After a catastrophic dev failure, the path back to stable operation is:

1. 

## Review conclusion

- Stable continuity preserved: `yes | no | unknown`
- Remaining accepted shared state:
- Blocking isolation defects:

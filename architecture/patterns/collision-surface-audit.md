# Collision Surface Audit

Modality: **PATTERN**

## Purpose

When stable and development channels coexist, do not assume separation because they use different branches, directories, processes, profiles, or extension IDs.

Two channels may still collide through shared mutable resources.

A **collision surface audit** enumerates those resources explicitly and classifies the cost of simultaneous existence, activation, cleanup, and failure.

## Core rule

> **Isolation claims are only as strong as the least-isolated shared surface.**

A filesystem split can be perfect while an OS registration, database, port, page namespace, device, or cloud resource remains globally shared.

## Audit categories

At minimum inspect the following classes when relevant.

### Source and filesystem

- working tree paths;
- generated artifacts;
- config files;
- state/data directories;
- caches;
- logs;
- lockfiles/sentinels;
- install directories.

### Runtime identity

- application IDs;
- extension/plugin IDs;
- process/service names;
- named pipes/sockets;
- ports;
- IPC endpoints;
- profile/user-data directories.

### Persistent state

- databases;
- migrations;
- browser/plugin storage;
- registry keys;
- environment variables;
- OS credential stores;
- shared settings;
- cloud state.

### In-process/page/application namespace

- DOM IDs/classes/data attributes;
- CSS/highlight names;
- global JavaScript symbols;
- hook/event names;
- singleton registries;
- file watchers;
- plugin command names;
- global hotkeys.

### External integration

- Native Messaging host names;
- COM/SAPI/system adapters;
- shell/file associations;
- protocol handlers;
- scheduled tasks;
- services;
- browser native hosts;
- device drivers;
- local daemon registrations.

### Exclusive or scarce resources

- audio output/control;
- microphone/camera;
- GPU contexts when globally constrained;
- serial devices;
- clipboard/global input hooks;
- files with exclusive locks;
- ports;
- hardware devices.

### Destructive lifecycle operations

- uninstall;
- cleanup;
- reset;
- migration rollback;
- cache purge;
- unregister;
- delete-data commands;
- credential rotation.

A channel that is safe to run but whose uninstall deletes the other channel is not isolated.

## Classification

Classify each surface with a status such as:

- **ISOLATED** — distinct identity/state; ordinary operations cannot affect the other channel;
- **SHARED READ-ONLY** — both channels consume the same immutable resource;
- **SHARED MUTABLE / COORDINATED** — sharing is intentional and has explicit ownership/locking/version rules;
- **COLLISION-PRONE** — concurrent use can corrupt, cancel, overwrite, or confuse state;
- **GLOBAL BUT ACCEPTABLE** — shared system state exists and empirical/design evidence says coexistence is currently safe;
- **UNKNOWN** — not yet audited; do not claim isolation.

For every non-isolated surface, record:
- what is shared;
- who owns mutation;
- whether concurrent activation is allowed;
- failure consequence;
- cleanup consequence;
- mitigation;
- evidence supporting the classification.

## Collision is not binary

The goal is not necessarily to eliminate all shared state.

Some sharing can be cheap or harmless.

Examples:
- two channels reading the same immutable model file may be fine;
- two processes writing the same SQLite database without a compatibility contract may be dangerous;
- a system-wide adapter may be acceptable if both channels use it compatibly;
- simultaneous audio playback may be annoying but not destructive;
- a dev installer overwriting a production Native Messaging registration is unacceptable.

The audit should distinguish inconvenience, interference, corruption, and continuity loss.

## Cost dimensions

For each collision surface consider:

1. **coexistence cost** — can both channels simply be installed/present?
2. **activation cost** — can both run at once?
3. **data integrity cost** — can one corrupt the other's state?
4. **continuity cost** — can dev disable the stable capability?
5. **cleanup cost** — can dev uninstall/reset damage stable?
6. **operator confusion cost** — can the human easily invoke the wrong channel?
7. **recovery cost** — what must happen after failure?

This prevents overreacting to benign overlap and underreacting to destructive shared state.

## Channel namespacing

When practical, namespace channel-specific mutable resources:

    product.resource
    product.resource.dev

or equivalent stable/dev identities.

Good candidates include:
- service names;
- Native Messaging hosts;
- ports;
- profile directories;
- storage prefixes;
- DOM/UI identifiers when two versions may touch one document;
- install directories;
- caches;
- IPC endpoints.

Do not namespace a genuinely shared immutable/global dependency merely for ceremony.

## Cleanup symmetry

Every development-specific install/mutation should have development-specific cleanup.

Hard question:

> **Can dev uninstall/reset/cleanup run without deleting or unregistering anything the stable channel still requires?**

If no, lifecycle isolation is incomplete.

## Audit artifact template

A project-level audit can use a table:

| Surface | Stable identity | Dev identity | Classification | Concurrent use | Failure/cleanup risk | Mitigation/evidence |
| --- | --- | --- | --- | --- | --- | --- |
| Files/worktree | ... | ... | ISOLATED | yes | low | separate worktrees |
| App/extension identity | ... | ... | ... | ... | ... | ... |
| Persistent storage | ... | ... | ... | ... | ... | ... |
| Runtime namespace | ... | ... | ... | ... | ... | ... |
| Audio/device | ... | ... | ... | ... | ... | ... |
| OS/native registration | ... | ... | ... | ... | ... | ... |
| Uninstall/cleanup | ... | ... | ... | ... | ... | ... |

## Review questions

1. What surfaces exist outside Git/filesystem isolation?
2. Which resources are global or singleton?
3. Which resources are shared mutable?
4. Can simultaneous activation cause only annoyance, or actual state loss?
5. Can dev cleanup damage stable?
6. Can the human distinguish channels without carrying excessive mental state?
7. What remains UNKNOWN?

## Governing sentence

> **Do not say two runtimes are isolated until you have audited where they still touch.**

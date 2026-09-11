# Stable / Development Runtime Split

Modality: **PATTERN**

Satisfies: `principles/0002-load-bearing-runtime-continuity.md`

## Purpose

Preserve a verified runtime for a load-bearing continuity envelope while allowing development to remain invasive, iterative, and temporarily broken.

## Canonical shape

    SAME PROJECT / SAME HISTORY

    stable channel
      known-good candidate
      principal consumes here
      mutation prohibited except promotion

    development channel
      current integration work
      workers mutate here
      regression allowed

The channels should share project lineage without sharing a single mutable runtime surface.

## Preferred repository shape

When the application/plugin executes directly from checkout files, prefer:

    repository
      stable branch  -> stable worktree/path
      main/dev line  -> development worktree/path

For example:

    project/
      stable worktree

    project-dev/
      development worktree

Do not create a copied `stable/` source directory inside the development tree merely to preserve old files. That creates a second ungoverned source copy that can drift.

A second repository is also normally unnecessary when stable and dev are still one product lineage.

## Why physical separation matters

A branch distinction alone is insufficient if the active runtime reads whatever files happen to exist in one checkout.

Separate worktrees/checkouts provide:
- distinct filesystem paths;
- no branch switching underneath the stable runtime;
- easier runtime identity;
- simpler operator mental model;
- lower chance that a worker edits the consumption tree by accident.

## Promotion flow

    dev candidate C
      -> automated evidence
      -> real-runtime evidence required by continuity envelope
      -> principal/director acceptance as applicable
      -> advance stable to exact C
      -> stable remains known-good

Never promote a nearby commit merely because the intended fix is equivalent.

The tested candidate identity is part of the evidence.

## Failure flow

    dev candidate fails
      -> preserve failure evidence/snapshot if useful
      -> fix forward in dev
      -> stable does not move
      -> principal continues normal activity on stable

Do not force stable backward/forward repeatedly as a side effect of development debugging.

## Development snapshot

For a severe regression or architectural failure, an explicit forensic snapshot branch/tag can preserve the broken development state while repair continues.

This is optional. It is useful when:
- the broken state contains substantial implementation work worth investigating;
- rollback to known-good is needed immediately for the consumption channel;
- future diagnosis needs an immutable reference to the failure.

The snapshot is evidence/history, not a new active runtime channel.

## Stable mutation policy

The stable channel should normally be advanced only through promotion.

Do not:
- run experimental worker goals directly against the stable worktree;
- make ad hoc fixes only in stable without reconciling project lineage;
- let dev install/uninstall scripts mutate stable-only external registrations;
- use stable as a scratch recovery branch.

## Other deployment shapes

The same pattern can be implemented without Git worktrees when the runtime naturally has installation/release channels:

- stable installed binary + dev build directory;
- production local service + dev service instance;
- pinned stable package version + local/path override for development;
- stable browser profile/plugin + development browser profile/plugin;
- stable data pipeline + sandbox pipeline.

The principle is logical and operational isolation, not a mandatory Git mechanism.

## Promotion gate template

A project should record:

- **stable channel identity:** branch/tag/version/path;
- **development channel identity:** branch/path/runtime;
- **continuity envelope:** capabilities that must remain working;
- **automated gates:** compile/tests/static checks;
- **runtime gates:** exact manual/integration observations;
- **human gate:** whether explicit principal acceptance is required;
- **shared-state hazards:** link to collision audit;
- **rollback/recovery action:** how to resume stable after dev failure.

## Desired guarantee

> **Development can fail independently of consumption.**

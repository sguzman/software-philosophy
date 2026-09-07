# Dependency Materialization

External development tools are part of project state.

Their **requirements** belong in the repository even when the binaries themselves do not.

## Principle

> The repository declares its environment; repository-owned machinery materializes it.

A dependency workflow should separate:

    declaration
      -> materializer
      -> verification
      -> human/product command

## Requirements

Dependency setup should be:
- declared in committed, inspectable files;
- idempotent or safely rerunnable;
- callable from a stable repo-owned bootstrap;
- deterministic enough for CI and local work to share the same contract;
- explicit about unavoidable platform-native exceptions;
- accompanied by actionable diagnostics.

Do not make a human-maintained setup checklist the only environment definition.

## Windows platform profile

For the principal's current Windows workflow:

### Ordinary CLI dependencies -> Scoop

Scoop is the canonical manager for normal command-line tools.

Prefer Scoop's own manifest/export/import representation, such as:

    Scoopfile.json

A repo bootstrap may wrap:

    scoop import .\Scoopfile.json

so environment checks, first-install behavior, and project-specific verification remain one command.

### Language toolchains -> native declarations when appropriate

Do not force every tool through Scoop merely for aesthetic uniformity.

Example:

    rust-toolchain.toml
      -> rustup

The repo should still own the declaration and bootstrap/check path.

### Platform-native workloads -> explicit exception

Some Windows-native compiler/SDK/workload installation may be more correctly owned by Microsoft platform installers.

Such exceptions must be narrow, documented, automated as far as practical, invoked by the repo bootstrap, and not converted into a long manual setup ritual.

Scoop remains the default Windows CLI dependency policy; exceptions do not dissolve that policy.

## Human responsibility

The human does not monitor dependency drift.

The director owns telling the principal when to run or rerun dependency materialization for a requested local test.

A repo QA command may invoke the dependency bootstrap automatically.

Either way, the human should not have to infer:

> Did this goal add Pandoc? Do I need CMake now? Which installer was it?

That knowledge belongs to the repo/director layer.

## CI parity

CI should exercise the same declarations/materializers when practical.

This does not mean CI and a workstation are identical evidence environments.

It means they should not maintain unrelated dependency stories.

## Avoid bespoke schemas when a good native declaration exists

Prefer ecosystem-native representations when they express the needed state.

The point is not to invent `deps.toml` for every repository.

The point is to make the dependency contract durable, machine-readable, and repo-owned.

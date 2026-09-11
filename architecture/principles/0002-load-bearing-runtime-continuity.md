# 0002 — Load-Bearing Runtime Continuity

Modality: **PROHIBITION / HARD INVARIANT**

## Failure mode

A project becomes useful enough that the principal begins relying on it for real activity, while the same live runtime remains the target of invasive development.

A development regression then destroys the principal's working tool at the exact moment the development line is least trustworthy.

This is not merely a regression bug. It is an isolation failure.

## Invariant

> **Experimental mutation must not be able to remove the last verified runtime for a declared load-bearing continuity envelope.**

The development channel may be unstable. The relied-upon channel must remain recoverable without repairing development first.

## Prohibited topology

For a load-bearing capability, do not use a single mutable runtime surface as both:
- the principal's normal consumption environment; and
- the worker's experimental integration environment.

Examples of prohibited shapes include:
- a browser loading an unpacked extension directly from the same checkout workers mutate;
- a local service instance serving production-like personal use while workers replace its binaries/config in place;
- a relied-upon library consumer tracking an unverified development head with no pinned known-good path;
- a plugin installation that is simultaneously the only working copy and the development target.

## Required property

The stable and development channels must differ enough that a development failure has bounded reach.

The desired recovery action is small:

    dev failure
      -> stop/leave dev channel
      -> resume verified stable channel

not:

    dev failure
      -> debug
      -> branch surgery
      -> reinstall/reset
      -> reconstruct settings
      -> hope normal activity returns

## Stable-channel semantics

A stable channel is not merely a branch named `stable`.

It is a runtime path with all of these properties:
- points to a known candidate identity/commit/version;
- has passed the promotion evidence required by the continuity envelope;
- is not mutated by ordinary experimental work;
- can be invoked without switching the development checkout into a known-good state;
- remains available while development continues.

## Development-channel semantics

The development channel may:
- contain unfinished features;
- regress;
- change architecture;
- carry additional instrumentation;
- use experimental external integrations;
- be reset or recreated.

Its failures must not silently rewrite the stable runtime's files or destructive external state.

## Shared external state

Separate source trees alone are insufficient when stable and dev still share mutable external resources.

Audit at least:
- process/service names;
- ports and sockets;
- databases and migrations;
- config/state directories;
- caches;
- extension/plugin identities;
- browser page/DOM namespaces;
- storage keys;
- audio/device ownership;
- OS registrations;
- Native Messaging hosts;
- environment variables;
- cloud resources/accounts;
- uninstall/cleanup paths;
- generated artifacts consumed by both channels.

A shared resource is not automatically forbidden. It must be classified and its failure semantics understood.

## Promotion boundary

Movement from dev to stable is a state transition requiring evidence.

The promotion gate must verify the declared continuity envelope using the strongest relevant evidence class.

For interactive software, real-runtime human verification may be required even when automated tests are green.

The exact commit/version tested must be the one promoted.

## Exceptions

A separate stable runtime may be unnecessary when:
- the project is explicitly non-load-bearing;
- the principal accepts interruption and the cost is trivial;
- the runtime is inherently disposable and can be reproduced instantly from an immutable known-good artifact;
- another independent tool already provides equivalent continuity.

The absence of a recorded load-bearing declaration is not itself an exception when credible evidence suggests dependence.

## Review questions

1. What capability is load-bearing?
2. Where is the verified runtime physically/logically located?
3. Can development mutation touch its files or mutable dependencies?
4. What shared state crosses the channel boundary?
5. What is the worst plausible dev failure blast radius?
6. Can stable continue operating while dev is completely broken?
7. What evidence promotes a candidate?
8. Does cleanup/uninstall of dev leave stable untouched?

## Derived pattern

See `architecture/patterns/stable-development-runtime-split.md` and `architecture/patterns/collision-surface-audit.md`.

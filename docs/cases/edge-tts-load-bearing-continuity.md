# Case Study — Edge TTS Load-Bearing Continuity Failure

This case produced the v1.8 load-bearing continuity doctrine and Edge-extension isolation pattern.

## Starting condition

`edge-tts` had crossed an important boundary without the development topology acknowledging it.

It was still being treated as a project under active structural revision, but it had also become a real reading tool the principal was actively consuming.

The same unpacked Edge extension/runtime path was therefore serving two incompatible roles:

- verified personal consumption runtime;
- experimental integration surface.

The principal had not previously made the degree of private reliance explicit enough, and the director had not promoted the available signs of active consumption into a durable continuity contract.

This responsibility was asymmetric:

- the principal possessed hidden facts about private use that an agent could not be expected to infer perfectly;
- the director nevertheless had enough contextual evidence to have treated possible reliance as a question worth surfacing before invasive browser/runtime work.

## Regression event

A structural integration intended to add Windows Natural voices regressed the existing reader before the new feature was actually available.

Visible symptoms included:
- duplicate/stale HUD behavior;
- reader controls becoming non-responsive;
- speech stuck in startup;
- quit/stop behavior failing;
- the intended natural voice catalog still missing.

A concrete stale-session bootstrap bug was found and repaired, but the broader problem remained: the principal's only working reader had already been converted into the development target.

The structural lesson was therefore larger than the individual bug.

## Recovery topology

The correction did not create a second repository or a copied `stable/` source folder.

It retained one project lineage and introduced two runtime roles:

    stable branch
      -> last browser-verified working runtime

    main branch
      -> development/integration
      -> allowed to regress

with separate physical worktrees:

    edge-tts
      stable runtime checkout

    edge-tts-dev
      development checkout

The initial stable branch was pinned to commit:

    c089d08ece6009592faa2fdf4306e4ce873e4ea8

The broken Windows Natural integration line was preserved rather than destroyed, including an explicit forensic snapshot:

    development-snapshot/win-natural-regression

This established an important secondary principle:

> **Restoring continuity does not require erasing the failed development state.**

Stable recovery and development forensics can coexist.

## Promotion discipline

`stable` could advance only after the exact candidate had passed real Edge manual QA and the principal accepted it.

Automated tests, source inspection, native-helper tests, or a worker DONE claim were not sufficient evidence for browser-facing stable promotion.

The relied-upon continuity envelope included the ordinary reader path, not merely the new feature being developed.

## Edge profile isolation

The next problem was coexistence.

Two different worktrees were not enough to prove that two unpacked extensions could safely exist at the same time.

The preferred runtime topology became:

    normal Edge profile
      -> stable checkout
      -> load-bearing reader

    development Edge profile
      -> dev checkout
      -> experimental reader

This reduced operator confusion and isolated extension-scoped storage/service-worker lifecycle while allowing the principal to abandon a broken dev window/profile and immediately return to stable.

## Collision audit

The audit identified multiple distinct collision classes.

### Files / Git

**Isolated.** Separate worktrees prevented development edits from rewriting stable source files.

### Extension identity / extension-scoped storage

**Isolated enough for coexistence.** Distinct unpacked paths and no fixed manifest key produced distinct extension identities, separating extension storage, service workers, reload, and uninstall lifecycle.

### Same-document DOM / CSS namespace

**Collision-prone.** Stable and dev used overlapping DOM IDs, data attributes, highlight/style identifiers, and cleanup selectors. Development bootstrap cleanup could therefore remove or damage the stable page session if both versions were activated in one document.

This proved that distinct extension IDs do not imply same-page isolation.

### Audio / speech ownership

**Collision-prone for concurrent activation.** Each extension could believe it owned playback; browser-global speech operations could cancel each other and direct audio could overlap.

Concurrent stable/dev speech was therefore not treated as safe by default.

### Native Messaging

**Insufficiently isolated.** A single global Native Messaging host registration and one `allowed_origin` meant dev installation could overwrite the registration needed by another channel.

The desired correction was channel-specific host identities/install paths, for example a stable host plus a `.dev` host, with dev uninstall unable to remove production registration.

### System-wide speech adapter

**Global but empirically acceptable.** The shared adapter was system-wide, but stable had already been verified while it was installed. The correct discipline was not automatic duplication; it was to prevent ordinary dev cleanup from unregistering shared infrastructure still required by stable.

## Recovery invariant

The desired user-facing guarantee became:

> **A dev failure should cost the dev tab/window/profile, never the principal's ability to continue using the verified reader.**

No stable branch switching, uninstall, reset, settings reconstruction, or repair should be required merely because development broke.

## Generalized lessons

This incident produced the following reusable concepts:

1. **Private load-bearing status** — software can become infrastructure for the principal without a formal release process noticing.
2. **Capability-level criticality** — existing relied-upon behavior can be load-bearing while a new feature remains experimental.
3. **Continuity envelope** — identify the minimum capability set that must stay available.
4. **Stable/development runtime split** — consumption and invasive mutation should not share the only live runtime when regression cost is meaningful.
5. **Evidence-gated promotion** — stable advances only after the exact candidate passes the evidence class that matters in the actual runtime.
6. **Collision-surface audit** — physical/source separation is only one layer; shared DOM, audio, registrations, storage, devices, and cleanup paths must be inspected independently.
7. **Bounded recovery cost** — catastrophic development failure should be recoverable by leaving the dev channel, not by repairing the stable channel.
8. **Preserved failure evidence** — continuity recovery need not destroy the broken development state or its forensic value.

## Derived doctrine

See:

- `docs/20-load-bearing-software-continuity.md`
- `architecture/principles/0002-load-bearing-runtime-continuity.md`
- `architecture/patterns/stable-development-runtime-split.md`
- `architecture/patterns/collision-surface-audit.md`
- `architecture/patterns/edge-extension-stable-dev-isolation.md`

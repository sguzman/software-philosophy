# Latent Options

Some ideas deserve to be remembered without deserving work.

v1.3 calls these **latent options**.

## Purpose

A latent option preserves future design space.

It answers:

> If circumstances change later, what alternative should the director remember exists?

It does **not** answer:

> What should we build next?

## Properties

A latent option has:
- a name;
- the current convention it might augment/replace;
- why the option could become attractive;
- possible promotion triggers;
- known costs/uncertainties;
- a clear statement of non-authorization.

It has no priority, due date, active owner, acceptance gate, branch, or worker session.

## Relation to the roadmap

Do not put latent options in the active roadmap merely so they are not forgotten.

Use an option register.

Suggested shape:

    options/
      README.md
      windows-environment-materialization.md

## Promotion triggers

A future environment system such as Nix or mise might deserve evaluation if:
- dependency graphs become much larger;
- cross-platform environment parity becomes painful;
- reproducibility demands become stricter;
- repeated bootstrap defects appear;
- a unified multi-language tool/version environment would materially reduce ceremony.

Until such a trigger matters, the current convention remains authoritative.

## No implied dissatisfaction

Recording an option must not create a narrative that the present system is provisional trash.

For example:

    CURRENT CONVENTION: Scoop for ordinary Windows CLI dependencies
    LATENT OPTIONS: mise, Nix

means:

> Scoop is the chosen solution now. Keep mise/Nix in memory if future constraints make them worth evaluating.

It does not mean:

> Migrate when you get bored.

## Promotion protocol

When the principal/director decides a latent option deserves attention:
1. mark it `EVALUATE`;
2. define the concrete trigger/problem being addressed;
3. compare against the current convention;
4. if change is warranted, write the architectural/policy decision;
5. create a macro-goal only after that decision.

This prevents future possibility from becoming accidental background pressure.

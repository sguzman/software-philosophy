# Doctrinal Modalities

v1.3 gives durable project statements explicit normative force.

Without this distinction, a repository can accidentally treat `never do this`, `this is what we use now`, and `maybe consider this someday` as equivalent planning objects.

They are not equivalent.

## 1. Prohibition — negative doctrine

A prohibition names a workflow or design shape that must not occur.

Examples:
- do not make the principal a courier;
- do not make the principal poll long-running work;
- do not conflate worker sessions with macro-goals;
- do not ask the principal to download/run generated development or QA payloads outside the checkout.

Prohibitions should be explicit, durable, accompanied by enough rationale that future directors do not casually optimize back into the failure, and treated as review criteria.

A prohibition is broader than a goal-specific non-goal.

## 2. Current convention — positive doctrine

A current convention says what mechanism the system should use **now**.

Examples:
- repository macro-goals are the durable work identity;
- human QA uses repo-owned entrypoints;
- ordinary Windows CLI dependencies use Scoop.

A convention is binding for current implementation, but revisable.

This matters because `chosen now` is not the same thing as `metaphysically best forever`.

## 3. Latent option — preserved optionality

A latent option says:

> This future direction may be worth considering later. Remember it, but do not schedule it.

A latent option carries no deadline, roadmap rank, active-goal authority, migration pressure, or claim that the current convention is inadequate.

It is a memory object, not a task.

## Promotion

Only the principal/director may promote a latent option.

Typical states:

    latent
      -> evaluate
      -> adopt as convention
         or
      -> reject/archive

Promotion should be triggered by actual conditions, not mere existence of the note.

## Why modality matters

Repositories are shared minds. Shared minds need more than facts; they need **force**.

An agent must be able to tell the difference between:
- `must not`;
- `do this currently`;
- `do not forget this possibility`.

That distinction prevents both accidental violations and accidental busywork.

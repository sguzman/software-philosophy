# Correction Continuations and Disposable Worker Sessions

v1.2 formalizes a distinction exposed by real Codex UI behavior:

> **A repository macro-goal is durable. A worker session is disposable.**

The two often begin together, but they do not share a lifecycle.

## The motivating failure

A worker session can:
1. execute Goal 0006;
2. claim DONE;
3. push its candidate;
4. send a terminal notification;
5. terminate its UI/session lifecycle.

The director can then inspect that candidate and determine that Goal 0006 is **not actually acceptable**.

If the doctrine assumes `one macro-goal = one worker session`, the system faces a false choice:

- incorrectly create Goal 0007 for mere correction work; or
- somehow try to resurrect an execution session that the tool considers finished.

Both are category errors.

## Three identities

### 1. Repository macro-goal identity

Example: `0006 — Non-PDF reader and TTS parity`.

This is the semantic work unit. It answers:
- what outcome are we trying to reach?
- what architecture/constraints govern it?
- what counts as acceptance?

This identity persists across correction passes.

### 2. Goal lineage

Example:
- branch `codex/0006-non-pdf-reader-parity`;
- report `docs/work/reports/0006.md`;
- reviews `docs/work/reviews/0006.md` plus later deltas/history;
- candidate commits from multiple attempts.

This is the durable causal history of the goal.

### 3. Worker session identity

Example: one Codex Goal UI session.

This is merely an execution container.

It may become permanently terminal after one attempt. That does not control the macro-goal number.

## The correction rule

When director review finds correctable defects and the semantic outcome remains the same:

> **Reopen the same repository macro-goal. Start a fresh worker session if the prior session terminated.**

Do not increment the repository goal number solely because a Codex Goal session ended.

## Canonical correction loop

    Repo Goal 0006
    ├─ Worker session S1 / Attempt A1
    │    -> candidate C1
    │    -> worker claims DONE
    │    -> terminal notification
    │    -> session terminates
    │
    ├─ Director review
    │    -> REVISE / correctable REJECT
    │    -> correction contract committed on main
    │    -> same Goal 0006 reopened to ready
    │
    └─ Worker session S2 / Attempt A2
         -> reads current goal + review
         -> continues branch/report lineage
         -> re-arms completion observer
         -> candidate C2
         -> director ACCEPT

## When the goal ID stays the same

Keep the same goal ID when:
- the desired outcome is unchanged;
- the correction is a response to director review of the same candidate objective;
- original architecture/non-goals still govern, possibly with a bounded correction delta;
- the work is needed to satisfy the original acceptance gates or make the evidence truthful;
- the new execution session exists only because the previous session ended.

Typical examples:
- missing tests;
- overstated evidence;
- a bounded correctness defect found in review;
- incomplete coverage of an acceptance gate;
- replacing a bad implementation approach while pursuing the same authorized outcome.

## When a new goal ID is justified

Create a new goal when the semantic work unit actually changes.

Examples:
- the prior goal was accepted and the project advances to the next capability;
- the principal/director changes the desired outcome;
- the prior goal is deliberately abandoned/superseded;
- correction would require a distinct strategic scope or architecture decision that the director chooses to represent as a new goal.

Goal numbering represents semantic sequence, not retry count.

## Work-state cycling

`done` and `blocked` are terminal for an **attempt**, not absorbing terminal states for the goal lineage.

A correction-aware work state machine may cycle:

    queued
      -> ready
      -> active(A1)
      -> done
      -> review: revise
      -> ready
      -> active(A2)
      -> done
      -> review: accept
      -> integrated/closed

A resolved blocker may similarly move:

    blocked -> director decision -> ready -> active(A_next)

## Director responsibilities

When requesting a correction continuation, the director should commit durable instructions that answer:
- same goal ID or superseded goal?
- review decision and defects;
- accepted work to keep;
- required corrections;
- correction non-goals;
- branch reuse or replacement;
- report history behavior;
- work-state transition back to `ready/`;
- whether the prior worker session is known to have terminated;
- completion-observer re-arm expectations;
- validation required for the next review.

The director should not tell the human to somehow continue a dead worker session when the tool requires a new session.

## Human responsibilities

The human should need only:
1. pull the director correction from main;
2. start/reset a fresh worker session when the previous one is terminal;
3. send the thin correction-continuation invocation;
4. disengage until the new attempt notification arrives.

The human does not renumber the goal, rewrite the review, reconstruct the old prompt, or manually reset notification state.

## Worker responsibilities

A correction worker session should:
1. read AGENTS and current accepted-main governance;
2. read the reopened goal and director review before editing;
3. recognize that this is the same macro-goal, not a new work item;
4. fetch/switch to the existing goal branch unless told otherwise;
5. synchronize the director's current correction/governance state into the working branch safely;
6. preserve accepted work from earlier attempts;
7. append or preserve report history;
8. re-arm completion observation for the new attempt;
9. execute until acceptance gates pass or a real escalation boundary is reached;
10. push and terminalize normally.

## Branch lineage

Default: reuse the same goal branch.

This keeps the causal chain compact and makes director review of correction deltas easy.

A director may explicitly require a replacement branch when the old approach should be discarded wholesale. Even then, the repository goal ID may remain the same if the semantic outcome is unchanged.

Branch identity is therefore also not identical to goal identity, though a stable branch is the preferred default.

## Report lineage

Do not erase the first attempt merely because it was insufficient.

Prefer:
- append a `Director Correction Pass` / `Attempt 2` section;
- retain prior validation and findings;
- state which review findings were closed;
- record new candidate head/evidence.

This preserves recoverable causality.

## Notification lineage

Completion observers are scoped to attempts, not entire goal lifetimes.

Each correction session must get a fresh observer epoch.

Stale terminal/ack state from attempt A1 must not cause attempt A2 to instantly notify.

The observer implementation may solve this with an attempt token, attempt number, rotated state file, or safe reset under a single-active-attempt invariant.

The human does not manage this.

## Thin correction prompt

A vendor-specific invocation may look like:

> This is a director correction continuation of repository Goal 0006, not a new macro-goal. Read `AGENTS.md`, the reopened goal in `docs/work/ready/`, and `docs/work/reviews/0006.md`. Continue the existing Goal 0006 branch/report lineage, re-arm completion notification for this new attempt, and execute all correction items until acceptance passes or an escalation condition is reached.

The prompt names the identity relationship. The repository still contains the actual correction contract.

## The deeper principle

Tool sessions are implementation details.

Repository semantics should not be forced to mirror UI lifecycle.

That gives the system a stable hierarchy:

    principal intent
      -> director-owned semantic goal
        -> durable repository lineage
          -> disposable worker sessions
            -> candidate attempts

The lower layer may restart without renaming the higher layer.

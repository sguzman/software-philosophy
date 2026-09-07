# Completion Observability and the Return Channel

v1.1 adds a missing half of practical delegation.

Macro-goals solved the problem of keeping a worker moving without repeated human prompts. They did not by themselves solve the problem of the human needing to watch for the worker to stop.

This document defines the **return channel**.

## The principle

> **A delegated long-running goal should wake the human at terminal state; the human should not have to poll for completion.**

The implementation worker is responsible for arming the repository-owned observer as part of goal activation.

The human is not responsible for remembering a second watcher command.

## Forward channel and return channel

A repository-mediated delegation has two directions:

    human/director -> repository goal -> worker
                 forward contract

    worker terminal state -> observer -> human
                 return signal

The forward channel carries authority and intent.

The return channel carries only attention.

Confusing those channels is dangerous. A notification must never become authority, evidence, or acceptance.

## Terminal semantics

The observer should signal only when the worker has reached a real terminal state.

Typical states:
- `done`: candidate work and report are ready for director review;
- `blocked`: execution stopped at a legitimate escalation/capability boundary.

Do not notify on:
- intermediate agent turns;
- compile/test passes;
- ordinary retries;
- partial stage completion;
- transient shell/process exits that do not terminalize the repository goal.

One goal terminalization should produce at most one terminal notification.

## The repository is still truth

The notification is deliberately weaker than repository state.

Think of it as:

> **an interrupt, not a verdict.**

The signal means: `the worker stopped; inspect the repository`.

It does not mean:
- the worker's DONE claim is correct;
- required evidence exists;
- tests passed;
- the director accepted the candidate;
- main changed.

If notification delivery fails, the repository can still contain a perfectly valid done/blocked handoff.

## Worker ownership

When a repository provides completion-observer machinery, the worker owns:
1. moving the goal into its active state;
2. starting the observer automatically for that explicit goal identity;
3. starting it detached from the current agent turn/shell lifecycle;
4. continuing ordinary authorized work;
5. terminalizing the goal only at real `done` or `blocked` state;
6. recording material observer startup/failure information in the report when useful.

The human should not manually launch the observer in the normal workflow.

## Detached lifetime

The observer should not depend on a single Codex turn, shell process, or conversational connection remaining alive.

It should be able to outlive ordinary process turnover long enough to observe terminalization.

This is why a detached local process is appropriate for workstation-driven development.

## Observe durable state

The observer should consume durable state rather than private agent state.

Preferred inputs include:
- repository work-state paths such as `docs/work/done/<goal>` and `docs/work/blocked/<goal>`;
- a goal-specific durable sentinel;
- branch-aware Git state when the local checkout may move.

Do not make correctness depend on scraping agent prose or guessing that a process exit means completion.

## Checkout-restoration race

Many workflows restore the shared checkout to `main` after pushing a candidate branch.

A naive polling watcher can miss `done/` if the working tree changes back to main before its next poll.

A robust observer must therefore have a deterministic terminalization handoff, for example:
- observe/ack terminal state before checkout restoration;
- inspect the goal branch through Git rather than only the checked-out filesystem;
- use a goal-specific temporary sentinel/ack;
- use another equivalent repository-owned mechanism.

The doctrine does not mandate one implementation. It mandates that routine checkout restoration cannot silently erase the event before it is observable.

## Exactly-once behavior

Human attention should not be spammed.

For one observer instance and one goal terminalization:
- signal once for `done` or once for `blocked`;
- never signal both unless the repository actually records two distinct terminalization epochs;
- exit after terminal signaling.

Persistent always-on daemons are not required by the philosophy. A bounded one-goal observer is usually easier to reason about.

## Failure semantics

Completion notification is workflow UX, not a product correctness gate.

Therefore:
- notification failure must not convert a correct product goal into BLOCKED or FAILED;
- an unavailable desktop-notification API should be classified honestly;
- deterministic observer logic should still be testable without real toast delivery;
- material observer failures can be recorded in the worker report and repaired as workflow work.

## Testability

A good observer implementation should provide a no-notification or injectable-sink mode.

Test at least:
- done detection;
- blocked detection;
- no notification for active/ready;
- exactly-once behavior;
- missing/malformed goal handling;
- survival of the repository's checkout/handoff pattern;
- non-fatal notification delivery failure.

## Windows adapter

In the workflow that motivated v1.1, the repository owns a PowerShell watcher such as:

    scripts/codex-goal-notify.ps1 -GoalId 0005 -RepoRoot <repo>

Codex launches it automatically as an independent Windows process. It watches the goal and emits a Windows desktop notification when the goal reaches `done` or `blocked`.

This is an implementation of the doctrine, not the doctrine itself.

Other repositories may use a macOS notification, Linux desktop notification, terminal bell, local webhook, or another bounded local return channel as long as the same semantics are preserved.

## Attention economics

Prompt tax makes the human repeatedly **push** work forward.

Vigilance tax makes the human repeatedly **pull** status back.

A well-designed agentic repository removes both low-value loops:

    one intent
      -> one durable macro-goal
      -> autonomous bounded execution
      -> one terminal signal
      -> director review / high-value human observation

The result is not a human-free system.

It is a system in which human attention is reserved for intent, taste, veto, architecture-changing ambiguity, and observations the machine cannot obtain.

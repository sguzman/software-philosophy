# Completion Observability and the Return Channel

v1.1 introduced the return channel; v1.2 makes it safe for multi-session correction continuations.

## The principle

> **A delegated long-running execution attempt should wake the human at terminal state; the human should not have to poll for completion.**

The implementation worker is responsible for arming the repository-owned observer as part of each attempt activation.

The human is not responsible for remembering a second watcher command.

## Forward channel and return channel

A repository-mediated delegation has two directions:

    human/director -> repository goal/review -> worker session
                 forward contract

    worker attempt terminal state -> observer -> human
                 return signal

The forward channel carries authority and intent.

The return channel carries only attention.

A notification must never become authority, evidence, acceptance, or macro-goal closure.

## Terminal semantics

The observer signals only when the **current execution attempt** reaches a real terminal state.

Typical states:
- `done`: current candidate/report are ready for director review;
- `blocked`: current attempt stopped at a legitimate escalation/capability boundary.

Do not notify on intermediate agent turns, compile/test passes, ordinary retries, partial stage completion, or transient shell/process exits that do not terminalize the repository attempt.

## Exactly once per attempt, not once per goal lifetime

One macro-goal may contain multiple worker attempts:

    Goal 0006
      Attempt A1 -> Completed notification
      director: revise
      Attempt A2 -> Completed notification
      director: accept

That is correct.

The exactly-once rule applies to **one observer epoch / one attempt terminalization**.

It does not prohibit later notifications for later attempts under the same goal ID.

## Re-arming after correction

A correction continuation must start a fresh observer epoch.

Old terminal state must not cause the new watcher to immediately announce the previous attempt.

Acceptable designs include:
- an explicit attempt/epoch ID in signal filenames;
- a monotonically increasing attempt number;
- a unique worker-session token;
- safe clearing/rotation of prior ephemeral terminal+ack state when the repository guarantees only one active attempt for that goal;
- another deterministic equivalent.

The human should not manage these tokens manually. Re-arming belongs to worker/repository automation.

## Stale-signal safety

Observer implementations must test the correction case:

1. attempt A1 signals `done` and is acknowledged;
2. director reopens the same goal;
3. attempt A2 observer starts;
4. A2 does **not** notify from A1's stale terminal marker;
5. A2 later signals its own `done` or `blocked` exactly once.

This is now a required semantic property for repositories that support correction continuations.

## The repository is still truth

The notification is deliberately weaker than repository state.

Think of it as:

> **an interrupt, not a verdict.**

The signal means: `the current worker attempt stopped; inspect the repository`.

It does not mean the worker's DONE claim is correct, required evidence exists, tests passed, the director accepted the candidate, the macro-goal is closed, or main changed.

## Worker ownership

When a repository provides completion-observer machinery, the worker owns:
1. moving/reopening the goal into its active state for the current attempt;
2. arming a fresh attempt-safe observer automatically;
3. starting it detached from the current agent turn/shell lifecycle;
4. continuing ordinary authorized work;
5. terminalizing only at real `done` or `blocked` state;
6. recording material observer startup/signal failures in the report when useful.

The human should not manually launch, reset, rotate, or signal the observer in the normal workflow.

## Detached lifetime

The observer should not depend on a single agent turn, shell process, or conversational connection remaining alive.

It should outlive ordinary process turnover long enough to observe the current attempt terminalization.

## Observe durable state

The observer should consume durable state rather than private agent state.

Preferred inputs include repository work-state paths, goal/attempt-specific durable sentinels, or branch-aware Git state when the local checkout may move.

Do not make correctness depend on scraping agent prose or guessing that process exit means completion.

## Checkout-restoration race

A robust observer must ensure routine checkout restoration cannot erase the terminal event before observation.

Acceptable strategies include post-push signaling into `.git`/temporary state, branch-aware Git inspection, or an explicit acknowledgment handshake.

## Failure semantics

Completion notification is workflow UX, not a product correctness gate.

Notification failure must not convert a correct product goal into BLOCKED or FAILED. An unavailable desktop API should be classified honestly. Observer logic should be deterministically testable without real desktop delivery.

## Minimum tests

Test at least:
- done detection;
- blocked detection;
- no signal for active/ready;
- exactly-once behavior within one attempt;
- **re-arm of the same goal ID for a second attempt without stale retrigger**;
- missing/malformed goal handling;
- checkout-restoration-safe behavior;
- notification sink failure remains non-fatal.

## Windows adapter

A Windows repository may use a PowerShell watcher such as:

    scripts/codex-goal-notify.ps1 -GoalId 0006 -RepoRoot <repo>

and a post-push signal helper.

For correction continuations, that adapter must either use an attempt-aware state key or reset/rotate the old goal terminal+ack state safely before starting the new observer epoch.

This is implementation, not universal doctrine.

## Attention economics

Prompt tax makes the human repeatedly **push** work forward.

Vigilance tax makes the human repeatedly **pull** status back.

Session/goal conflation creates a third avoidable burden: the human has to reason about tool lifecycle as if it were project lifecycle.

A well-designed repository removes all three:

    one durable goal identity
      -> attempt A1 in session S1
      -> terminal signal
      -> director correction
      -> attempt A2 in fresh session S2
      -> terminal signal
      -> director acceptance

The tool session can be disposable because the repository lineage is not.

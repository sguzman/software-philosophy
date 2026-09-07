# Roles and Repository Workflow

The Git repository is the durable communication channel between the human principal, director, and implementation worker.

## Human principal / maintainer

Owns:
- intent and taste;
- final veto;
- local runtime observations that agents cannot obtain.

Does not normally own:
- relaying architecture prompts;
- relaying worker reports;
- reviewing implementation diffs;
- merging worker branches;
- polling long-running worker status;
- manually starting a completion watcher.

## Director / architect / integrator

Owns:
- philosophy;
- product scope;
- priorities;
- architecture;
- roadmap ordering;
- macro-goals;
- semantic review;
- integration;
- evidence-backed current-state updates.

## Implementation worker

Owns:
- executing the authorized goal;
- directly related diagnosis and repair;
- tests and validation;
- durable reporting;
- pushing the candidate branch;
- automatically launching repository-owned completion observation when available.

## Completion observer

The completion observer is infrastructure, not an authority role.

It watches one goal's durable terminal state and emits a best-effort local signal for `done` or `blocked`.

It must not convert notification delivery into a correctness gate.

## Lifecycle

    director commits goal
      -> human invokes worker once
      -> worker activates goal + observer
      -> worker executes autonomously within goal
      -> worker terminalizes done/blocked + pushes candidate/report
      -> observer returns attention to human
      -> director reviews directly
      -> accept / reject / revise / block
      -> integrate accepted work
      -> update current state / roadmap

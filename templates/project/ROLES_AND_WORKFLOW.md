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
- merging worker branches.

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
- pushing the candidate branch.

## Lifecycle

    director commits goal
      -> human invokes worker
      -> worker executes and pushes candidate
      -> director reviews directly
      -> accept / reject / revise / block
      -> integrate accepted work
      -> update current state / roadmap

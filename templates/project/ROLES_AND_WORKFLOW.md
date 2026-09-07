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
- manually starting/resetting a completion watcher;
- deciding that a new worker session implies a new repository goal number;
- downloading/unpacking generated execution payloads for ordinary QA;
- inferring hidden dependency changes or manually reconstructing the development environment.


## Director / architect / integrator

Owns:
- philosophy;
- product scope;
- priorities;
- architecture;
- roadmap ordering;
- macro-goal identity;
- semantic review and correction contracts;
- integration;
- evidence-backed current-state updates;
- human execution policy;
- dependency-materialization policy and telling the principal when refresh is required.


## Implementation worker

Owns:
- executing the authorized goal attempt;
- directly related diagnosis and repair;
- tests and validation;
- durable reporting;
- pushing the candidate branch;
- completion-observer startup/re-arm when available.

## Repo-native human execution

Normal local development/QA remains inside the checkout.

The repository should declare dependencies, provide a bootstrap/check entrypoint, expose a stable QA/build command, and retain logs under repo-owned paths.

Do not use generated CI/agent payload downloads as the principal's development/testing handoff.

## Completion observer


The completion observer is infrastructure, not an authority role.

It watches one execution attempt's durable terminal state and emits a best-effort signal.

## Lifecycle

    director commits Goal G
      -> human starts worker session S1
      -> worker executes attempt A1
      -> A1 done/blocked + notification
      -> director reviews
          -> ACCEPT: integrate / close G
          -> REVISE: reopen same G to ready
               -> human starts fresh session S2 if S1 terminated
               -> worker continues same branch/report lineage as attempt A2
               -> re-arm observer
               -> review again

Worker-session count and repository-goal count are intentionally independent.

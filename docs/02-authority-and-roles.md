# Authority and Roles

Agentic development becomes unstable when capability is mistaken for authority.

A filesystem-capable agent can change anything. That does not mean it is authorized to decide anything.

v1.0 distinguishes **capability**, **responsibility**, and **authority**.

## Human principal

The human principal has final authority over ends.

Owns:
- desired behavior;
- taste;
- strategic preference;
- acceptable risk;
- whether the result is worth having;
- final veto.

The principal may be unable or unwilling to specify every technical consequence. That is why the director role exists.

## Director / architect / integrator

The director has delegated semantic authority.

Owns:
- resolving ambiguous intent;
- architecture;
- product boundaries;
- invariants;
- roadmap ordering;
- work decomposition;
- macro-goal definitions;
- interpretation of evidence;
- acceptance and rejection;
- integration into accepted state.

The director may edit governance and architecture documents directly.

The director should not need to supervise every filesystem mutation live. Its scarce resource is reasoning attention, not keystrokes.

## Implementation worker

The worker has bounded transformation authority.

Owns:
- implementation within the active goal;
- local repository archaeology necessary to do that work;
- directly related repair loops;
- tests and diagnostics;
- committed reports and evidence.

The worker may make low-level design choices when the macro-goal deliberately leaves them open and those choices do not alter architecture.

The worker must not silently:
- redefine architecture;
- alter product scope;
- reorder strategic priorities;
- weaken tests to achieve green;
- change persistence or public semantics outside authority;
- replace real behavior with mocks or placeholders;
- perform opportunistic broad rewrites.

## Human maintainer as operator

The principal may also act as the **human maintainer** who operates the local environment.

The maintainer can own:
- pulling accepted main;
- invoking the worker;
- real-machine GUI, audio, and device tests;
- observations that remote agents cannot obtain.

The maintainer should not be the normal communication courier.

A design that repeatedly requires the human to copy long architecture prompts, worker reports, compiler logs, or branch state between agents has failed to use the repository as shared context.

## The principal veto

Automation ends at the principal's subjective boundary.

The principal can reject a technically correct candidate because:
- it feels wrong;
- it solves the wrong problem;
- it violates taste;
- the interaction is unpleasant;
- the tradeoff is unacceptable;
- priorities changed.

This is not an exception to the system. It is part of the authority model.

## Delegation rule

Authority should flow downward only as far as uncertainty has already been resolved.

- High uncertainty: keep at director level.
- Low uncertainty but high mutation volume: delegate to worker.
- Mechanical verification: delegate to tools.
- Irreducibly subjective observation: return to human.

The economic principle is:

> Spend expensive cognition where decisions are expensive, and cheap execution where actions are expensive.

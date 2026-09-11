# Load-Bearing Software Continuity

Modality: **HARD DESIGN PRINCIPLE / GOVERNANCE RULE**

## Core rule

> **Once software becomes load-bearing for the principal's real activity, experimental development must not be allowed to remove the last verified working path for that activity.**

A project may begin as a toy, prototype, library, extension, script, or internal tool and later become part of the principal's actual working life.

That transition changes the development contract.

The project is no longer merely something being built. It is also something being consumed.

## Private load-bearing status

**Private load-bearing status** means the principal materially depends on a project or capability outside the development workflow itself.

Examples include:
- a reader used for daily reading;
- a library used by another personally important tool;
- an automation required for routine work;
- a local service used as infrastructure;
- an editor/plugin relied upon during ordinary activity;
- a data pipeline whose current output is operationally necessary.

The dependency can be private and invisible to the repository unless the principal or director records it.

Load-bearing status is therefore first-class project state and should be externalized once known.

## Capability-level criticality

Load-bearing status may apply to only part of a project.

A project can simultaneously contain:
- a **continuity envelope**: capabilities that must remain available;
- **experimental surfaces**: capabilities that may regress while under development.

Example shape:

    existing reading path       -> load-bearing continuity envelope
    experimental voice backend  -> development surface

This distinction is essential. New feature work does not gain permission to destroy already-relied-upon behavior merely because both live in one repository.

## Continuity envelope

The **continuity envelope** is the smallest set of capabilities whose availability must be preserved while development continues.

It should be concrete enough to verify.

For an interactive tool it may include:
- startup;
- core task execution;
- stop/quit/recovery;
- the currently relied-upon backend or data path;
- preservation of existing configuration/state needed for normal use.

A continuity envelope is not the same as full regression coverage. It is the operational minimum the principal is actively depending on.

## Discovery responsibility

The principal and director have asymmetric knowledge.

### Principal responsibility

The principal has primary responsibility for declaring hidden private consumption facts.

An agent cannot reliably infer how often a tool is used, whether it has become essential to a private routine, or what disruption would cost if those facts have never been surfaced.

The system must not pretend the director can mind-read invisible use.

### Director responsibility

The director has a secondary discovery duty.

If repository/chat evidence suggests a project is being actively consumed rather than merely developed, the director should surface and record that possibility before authorizing work with a meaningful regression blast radius.

Signals include:
- the principal repeatedly says they are using the tool;
- the tool is invoked as part of another routine or project;
- manual QA occurs through ordinary use rather than synthetic testing;
- the principal describes a capability as required, daily, normal, or relied upon;
- prior regressions caused loss of unrelated productive activity.

Absence of a declaration is not proof that the project is safe to break.

The director should not over-interrupt the principal for every repository. But credible evidence of dependence should trigger a durable criticality decision.

### Worker responsibility

The implementation worker does not infer or redefine criticality. It follows the repository's continuity contract and escalation rules.

## Continuity before experimentation

When a load-bearing continuity envelope exists, invasive development must preserve an immediately available verified runtime path.

The default principle is:

> **Development may break; consumption may not lose its last known-good path.**

This normally implies some form of runtime-channel separation.

Possible implementations include:
- stable and development branches plus separate worktrees;
- a verified installed release plus a development checkout;
- production and development service instances;
- stable and experimental plugin/browser profiles;
- pinned dependency versions for consumers while the library develops on another line.

The exact mechanism is project-specific. The invariant is continuity.

## Promotion, not replacement-by-assumption

A development candidate does not become the load-bearing runtime merely because:
- it compiles;
- unit tests pass;
- CI is green;
- an implementation worker reports DONE;
- source inspection looks correct;
- a new feature appears implemented.

Promotion into the load-bearing channel requires evidence appropriate to the relied-upon surface.

For user-facing software, this often means the exact candidate must be exercised in the actual runtime environment and the continuity envelope verified before promotion.

Where human experiential evidence is the only valid evidence class, the principal's acceptance is part of the promotion gate.

## Failure blast radius

A development failure should have a bounded blast radius.

For a load-bearing project, the desired property is:

> **A failed development attempt should cost the development environment, not the principal's ability to perform the relied-upon activity.**

Recovery from a dev regression should not normally require:
- repairing the stable runtime;
- resetting branches in the principal's consumption checkout;
- uninstalling/reinstalling the stable version;
- reconstructing settings;
- removing shared registrations that production still needs.

The principal should be able to leave/close the development channel and return immediately to the verified channel.

## Relationship to the human attention budget

Continuity is also a cognitive-load issue.

Breaking a load-bearing tool exports development instability into the principal's life. The human must stop their actual activity, diagnose project state, recover a working version, remember which copy is safe, and coordinate repair.

That is avoidable human load.

A mature agentic workflow protects not only code correctness but the principal's continuity of use.

## Relationship to repository-state closure

Load-bearing status, continuity envelopes, stable-channel identity, promotion rules, and known collision hazards are durable project state.

Once discovered, they belong in the repository.

They must not remain as conversational lore such as:

> "remember not to break the copy I use every day."

## Hard review questions

Before invasive work on a project, ask:

1. Is this project or any capability privately load-bearing?
2. Is criticality known, unknown, or credibly suspected?
3. What is the continuity envelope?
4. Is there a verified runtime path separate from experimental mutation?
5. What exact evidence is required to promote a candidate into the relied-upon channel?
6. If development fails catastrophically, can the principal immediately return to the verified runtime?
7. Does development mutate shared external state that could still damage the stable channel?
8. Has coexistence between stable and development channels been collision-audited?

If the answer exposes a single mutable runtime carrying both consumption and invasive development, fix the development topology before proceeding.

## Governing sentence

> **When software crosses from project into infrastructure, development discipline must cross with it.**

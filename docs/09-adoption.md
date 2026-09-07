# Adopting v1.0 in a Repository

The philosophy is technology-independent. Use only the structure your project earns.

## Recommended baseline

    AGENTS.md
    ARCHITECTURE.md

    docs/
      project/
        philosophy.md
        product-scope.md
        priorities.md
        current-status.md
        roles-and-workflow.md

      roadmaps/
        master-roadmap.md

      work/
        README.md
        queued/
        ready/
        active/
        blocked/
        done/
        reports/
        reviews/

    scripts/
      check

## Step 1 — write the constitution

Capture what the product is, what matters, what must not be casually changed, where state belongs, and role authority.

Do not begin with a giant encyclopedia. Begin with decisions that change implementation behavior.

## Step 2 — write current state from evidence

Inventory:
- what compiles;
- what runs;
- what is only historical;
- known defects;
- known platform limitations;
- stale migration artifacts;
- major architecture debt.

Do not trust old completion marks without verification.

## Step 3 — create an active roadmap

Order work by gates and dependencies.

The roadmap should answer:
- what must be true before the next layer becomes worth building?
- what evidence closes each gate?
- what historical work is context rather than authority?

## Step 4 — create the work protocol

Adopt a small state machine:

    queued -> ready -> active -> done
                        |
                        -> blocked

Reports and reviews live beside that lifecycle.

## Step 5 — write the first macro-goal

Make it large enough to eliminate predictable prompt loops.

Make it bounded enough that architectural ambiguity is explicit.

## Step 6 — shorten the prompts

Once the goal contract is committed, stop restating it in chat.

Worker invocation should become a pointer.

Director review invocation should become:

> Review the pushed branch for goal N against the repository contract and integrate it if acceptable.

## Step 7 — evolve from observed friction

The repo protocol itself is software.

If the human keeps becoming a courier, fix the protocol.

If the worker keeps escalating trivial failures, enlarge goal authorization.

If the worker causes architectural drift, strengthen doctrine and non-goals.

If the director repeatedly rediscovers project history, improve current-state documentation.

If tests claim too much, separate evidence classes.

## Optional machinery

As the workflow stabilizes, automate deterministic steps:
- clean-tree checks;
- branch naming;
- work-state moves;
- validation;
- report scaffolding;
- CI;
- candidate artifact builds.

Automation should support the authority model, not erase it.

## What not to standardize globally

v1.0 does not require:
- Rust;
- TOML;
- Docker;
- a particular CI provider;
- a particular AI vendor;
- a particular GUI framework;
- a particular branching model.

The doctrine standardizes **coordination semantics**, not technology taste.

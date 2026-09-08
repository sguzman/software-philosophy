# Adopting v1.4 in a Repository

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
        negative-doctrine.md
        architecture-principles.md
        language-profile.md


      roadmaps/
        master-roadmap.md

      options/
        README.md

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
      deps
      qa
      goal-completion-observer   # recommended for long-running local goals

## Step 1 — write the constitution

Capture what the product is, what matters, what must not be casually changed, where state belongs, and role authority.

Do not begin with a giant encyclopedia. Begin with decisions that change implementation behavior.

## Step 2 — write current state from evidence

Inventory what compiles, what runs, what is only historical, known defects, platform limitations, stale migration artifacts, and major architecture debt.

Do not trust old completion marks without verification.

## Step 3 — create an active roadmap

Order work by gates and dependencies.

The roadmap should answer what must be true before the next layer becomes worth building, what evidence closes each gate, and what historical work is context rather than authority.

## Step 4 — create the work protocol

Adopt a small state machine:

    queued -> ready -> active -> done
                        |
                        -> blocked

Reports and reviews live beside that lifecycle.

Define `done` as worker-terminal/review-ready, not director-accepted.

## Step 5 — write the first macro-goal

Make it large enough to eliminate predictable prompt loops and bounded enough that architectural ambiguity is explicit.

## Step 6 — shorten the prompts

Once the goal contract is committed, stop restating it in chat.

Worker invocation should become a pointer.

Director review invocation should become:

> Review the pushed branch for goal N against the repository contract and integrate it if acceptable.

## Step 7 — add completion observability

For long-running workstation goals, add a repository-owned bounded observer.

On Windows, a typical adapter is:

    scripts/codex-goal-notify.ps1

Required semantics:
- worker launches it automatically;
- one explicit goal identity per observer instance;
- detached lifetime;
- durable `done`/`blocked` observation;
- exactly-once terminal notification;
- no notification for intermediate turns;
- safe behavior across checkout restoration;
- deterministic test/no-toast mode;
- notification delivery failure is non-fatal to product correctness.

Do not make the human remember a second command. If that is required, vigilance tax has merely moved rather than disappeared.

## Step 8 — support correction continuations

Document the distinction between repository macro-goals and worker sessions.

When director review requests bounded correction after a worker session terminalizes:

- keep the same goal ID if the semantic objective is unchanged;
- reopen the same goal to `ready/`;
- start a fresh worker session;
- continue the branch/report lineage unless the review explicitly replaces it;
- read the current director review before editing;
- re-arm completion observation so stale prior-attempt state cannot retrigger.

The work-state machine is therefore cyclic:

    ready -> active(A1) -> done -> review: revise -> ready -> active(A2)

Do not make tool-session lifecycle determine repository goal numbering.

## Step 9 — define the human execution surface

Keep normal development and QA inside the checkout.

At minimum:
- declare external tools in committed machine-readable form;
- provide an idempotent dependency bootstrap/check command;
- provide a stable local QA/build entrypoint;
- keep generated fixtures/logs under repo-owned ignored paths;
- make the director say when dependency refresh is needed.

Hard prohibition:

> Do not make the principal download, extract, and execute a generated CI/agent payload to test ordinary repository state.

For the principal's current Windows profile, prefer `Scoopfile.json` plus Scoop for ordinary CLI tools. Preserve language-native toolchain declarations and explicit native-platform exceptions where those systems are the correct owner.

## Step 10 — add an option register

Create a place for **latent options**: future technologies worth remembering but not worth scheduling.

A latent option should record the possible technology/direction, why it may become attractive, the current convention it could replace or augment, promotion triggers, and an explicit statement that it is not queued/authorized work.

Do not put latent options directly into the active roadmap merely so they are not forgotten.

## Step 11 — adopt software architecture doctrine

Separate runtime/software-structure rules from agent workflow rules.

At minimum, audit interactive applications for the current hard invariant:

> A latency-critical interactive thread may orchestrate; it may not labor.

For GUI projects:
- identify the interactive/UI thread;
- identify blocking, CPU-heavy, or user-data-scaled work;
- move that work behind a worker/task boundary;
- use non-blocking result delivery back to the UI;
- add stale-result/cancellation/backpressure handling where needed.

Record project-specific architecture principles in `docs/project/architecture-principles.md`.

## Step 12 — adopt the principal language profile

Unless a project has a contrary constraint, product code should start from the Rust-first profile.

Record intentional deviations rather than silently drifting into a polyglot product runtime.

Normal exceptions such as PowerShell bootstrap, TOML/JSON configuration, package-manager metadata, and platform-required glue do not violate Rust-first.

## Step 13 — evolve from observed friction


The repo protocol itself is software.

If the human keeps becoming a courier, fix the protocol.

If the human keeps polling, improve completion observability.

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
- candidate artifact builds;
- terminal completion signaling.

Automation should support the authority model, not erase it.

## What not to standardize globally

v1.4 core governance does not universally require Rust, TOML, Docker, a particular CI provider, a particular AI vendor, a particular GUI framework, a particular branching model, Windows, PowerShell, a specific desktop-notification API, or a particular worker-session UI.

The core governance doctrine standardizes coordination semantics. Architecture doctrine adds reusable structural invariants. Principal profiles additionally standardize current implementation choices: Rust-first for product code and Scoop for ordinary Windows CLI dependency materialization. These remain explicit current conventions rather than eternal axioms.

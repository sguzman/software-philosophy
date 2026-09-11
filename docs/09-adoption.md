# Adopting v1.8 in a Repository

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
        operational-criticality.md    # when known/relevant
        collision-audit.md             # when stable/dev channels coexist

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

    prompts/
      README.md
      execute-ready-goal.md
      continue-corrected-goal.md
      review-pushed-goal.md
      request-human-verification.md

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

## Step 6 — create repository prompt artifacts

Do not leave recurring invocation wording in chat.

Create a `prompts/` directory or an explicitly documented equivalent and commit the reusable prompts that drive the workflow.

At minimum, consider artifacts for:
- executing the ready goal;
- continuing a director-corrected goal;
- invoking director review of a pushed candidate;
- requesting human verification.

Prompt artifacts are first-class repository protocol. They are versioned, reviewable, discoverable, and transported with Git.

Keep them thin. Once the goal/review/architecture contract is committed, the prompt should point at it rather than duplicate it.

Distinguish:

    prompt artifact = durable file in Git
    prompt invocation = transient paste/send/trigger in an external UI

The external UI is not the canonical prompt store.

## Step 7 — shorten prompt artifacts

Once the repository contracts are rich enough, remove duplicated project knowledge from prompt artifacts.

A worker prompt should become mostly a pointer, for example:

> Read AGENTS.md and execute the single authorized macro-goal in docs/work/ready/.

The prompt artifact remains durable even though its content is thin.

## Step 8 — add completion observability

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

## Step 9 — support correction continuations

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

## Step 10 — define the human execution surface

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

## Step 11 — add an option register

Create a place for **latent options**: future technologies worth remembering but not worth scheduling.

A latent option should record the possible technology/direction, why it may become attractive, the current convention it could replace or augment, promotion triggers, and an explicit statement that it is not queued/authorized work.

Do not put latent options directly into the active roadmap merely so they are not forgotten.

## Step 12 — adopt software architecture doctrine

Separate runtime/software-structure rules from agent workflow rules.

At minimum, audit interactive applications for the current hard invariant:

> A latency-critical interactive thread may orchestrate; it may not labor.

For GUI projects:
- identify the interactive/UI thread;
- identify blocking, CPU-heavy, or user-data-scaled work;
- move that work behind a worker/task boundary;
- use non-blocking result delivery back to the UI;
- add stale-result/cancellation/backpressure handling where needed.

Also ask whether any project capability has become load-bearing for the principal's real activity.

If so, adopt:

> Experimental mutation must not remove the last verified runtime for the load-bearing continuity envelope.

Record project-specific architecture principles in `docs/project/architecture-principles.md`.

## Step 13 — record operational criticality

Do not assume every project is load-bearing, but do not assume silence means it is safe to break either.

Use `templates/project/OPERATIONAL_CRITICALITY.md` or an equivalent artifact when dependence is known or credibly suspected.

Record:
- project/capability criticality;
- continuity envelope;
- experimental surfaces;
- stable/consumption runtime identity;
- development runtime identity;
- promotion gates;
- immediate recovery path after dev failure.

The principal is the primary source for hidden private-use facts. The director should surface credible evidence of dependence before risky structural work.

## Step 14 — separate stable consumption from experimental development when needed

If a load-bearing capability executes from mutable development files or would otherwise be exposed to regression, create a stable/development channel split.

For software that runs directly from checkout files, separate Git worktrees are a strong default.

For installed/services/plugin systems, use equivalent separate runtime identities.

The key property is not the branch name. It is that development can fail without taking away the verified consumption channel.

## Step 15 — audit collision surfaces

A separate worktree, installation, process, or profile does not prove isolation.

Use `templates/project/COLLISION_AUDIT.md` or an equivalent artifact to inspect:
- source/runtime paths;
- application/extension/plugin identity;
- persistent state;
- runtime namespaces/DOM/globals;
- audio/devices/global resources;
- IPC/ports/sockets;
- native/OS registrations;
- external service/cloud state;
- uninstall/reset/cleanup behavior.

Classify unknowns honestly. Distinguish harmless sharing from interference, corruption, continuity loss, and destructive cleanup.

For Edge extensions, prefer separate stable/dev worktrees and separate Edge profiles, then audit same-page DOM/CSS identifiers, audio ownership, Native Messaging host registrations, shared system adapters, and extension lifecycle.

## Step 16 — adopt the principal language profile

Unless a project has a contrary constraint, product code should start from the Rust-first profile.

Record intentional deviations rather than silently drifting into a polyglot product runtime.

Normal exceptions such as PowerShell bootstrap, TOML/JSON configuration, package-manager metadata, and platform-required glue do not violate Rust-first.

## Step 17 — evolve from observed friction

The repo protocol itself is software.

If the human keeps becoming a courier, fix the protocol.

If the human keeps polling, improve completion observability.

If recurring prompt wording lives in chat, promote it into `prompts/`.

If prompt artifacts keep restating the project, enrich repository contracts and thin the prompts.

If the worker keeps escalating trivial failures, enlarge goal authorization.

If the worker causes architectural drift, strengthen doctrine and non-goals.

If the director repeatedly rediscovers project history, improve current-state documentation.

If tests claim too much, separate evidence classes.

If a project has quietly become part of the principal's real workflow, record its criticality and protect its continuity before further invasive development.

If stable/dev coexistence relies on "they probably won't interfere," perform a collision-surface audit.

## Optional machinery

As the workflow stabilizes, automate deterministic steps:
- clean-tree checks;
- branch naming;
- work-state moves;
- validation;
- report scaffolding;
- CI;
- candidate artifact builds;
- terminal completion signaling;
- prompt rendering/invocation from canonical repository prompt artifacts;
- stable-candidate promotion checks;
- channel-specific install/uninstall validation.

Automation should support the authority model, not erase it.

## What not to standardize globally

v1.8 core governance does not universally require Rust, TOML, Docker, a particular CI provider, a particular AI vendor, a particular GUI framework, a particular branching model, Windows, PowerShell, a specific desktop-notification API, a particular worker-session UI, or a universal stable branch for every repository.

The stable/development split is required only when continuity demands it; the exact implementation depends on the runtime. Edge profiles are an Edge-extension pattern, not a universal software rule.

The core governance doctrine standardizes coordination semantics, repository-state closure, human-attention protection, and load-bearing continuity. Architecture doctrine adds reusable structural invariants and patterns. Principal profiles additionally standardize current implementation choices such as Rust-first and Scoop for ordinary Windows CLI dependency materialization. These remain explicit current conventions rather than eternal axioms.

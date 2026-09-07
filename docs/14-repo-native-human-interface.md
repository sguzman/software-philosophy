# Repo-Native Human Interface

The repository is not only the shared mind between agents.

It is also the principal's **execution home**.

## Hard prohibition: no external testing payload handoff

For ordinary development and human QA:

> **Never ask the principal to download, unpack, trust, and run a generated payload outside the repository checkout.**

This includes:
- GitHub Actions QA ZIPs;
- agent-generated runnable archives;
- temporary executable bundles;
- one-off downloaded test scripts;
- alternate directories that become a second development workspace.

CI artifacts may exist as machine evidence or release/distribution outputs, but they are not a human development/QA handoff mechanism for the principal.

## Why this is prohibited

The failure is structural, not aesthetic.

External payload handoff creates:

### Mental load
The human must remember what was downloaded, where it was extracted, which script to run, and how that copy relates to Git.

### Network dependence
A local verification step becomes gated by transfer speed/reliability even when the repository is already present.

### Provenance ambiguity
The principal is asked to run material assembled elsewhere rather than building from the checked-out state they can identify.

### Second-channel state
The test environment becomes an external bundle rather than repository-described state.

### Trust expansion
The human is asked to execute an opaque generated payload instead of repository-owned code plus declared dependencies.

### Cleanup/ceremony
Download, extraction, navigation, and disposal are mechanical work exported to the principal.

This is **ceremony tax**.

## Positive invariant

Normal human development/testing should look like:

    git pull
      -> repo dependency bootstrap/check if required
      -> repo QA/build command
      -> embodied observation
      -> repo-owned logs/handoff

The principal should contribute only what automation cannot:
- intent;
- taste;
- sensory/embodied runtime observation;
- final veto.

## Human-facing command design

Prefer one stable command per common human operation.

Examples:

    .\deps.ps1
    .\qa.ps1
    ./scripts/check

The command should discover the repository root, use committed declarations, prepare ignored local state, build the actual checkout, launch the relevant product path, preserve logs, and fail with actionable diagnostics.

The human should not have to manually reproduce the environment sequence behind it.

## Director responsibility

Before requesting human verification, the director must determine:
1. which accepted repository state should be pulled;
2. whether dependency declarations changed;
3. whether bootstrap needs to run/rerun;
4. the repo-owned command to invoke;
5. the exact observation requested.

If the repository cannot support the requested test without an external payload detour, the workflow is not ready for human verification yet.

Repair the execution surface first.

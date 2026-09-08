# 0001 — Interactive Thread Isolation

Modality: **PROHIBITION + ARCHITECTURAL INVARIANT**

## Rule

> **A latency-critical interactive thread may orchestrate; it may not labor.**

In GUI applications, the thread responsible for user interaction and frame construction must not perform heavy, blocking, unbounded, or externally paced work.

This applies especially to Rust + egui applications, where application update/UI construction commonly occurs on the same latency-critical path as input handling and frame production.

## Why `render thread only` is slightly too narrow

The interactive thread legitimately does more than draw pixels.

It may:
- receive and interpret input;
- mutate small UI/view-model state;
- perform cheap deterministic state transitions;
- construct widgets/layout for the current frame;
- enqueue background work;
- non-blockingly poll or drain completed-result channels;
- apply small completed results to UI-owned state;
- schedule/request repaint;
- perform framework-required lightweight UI bookkeeping.

The invariant is therefore not `rendering only`.

The invariant is **latency isolation**.

## Hard prohibition

Do not perform work on the interactive thread when any of these are true:

- latency can scale materially with user-controlled data size;
- latency depends on disk, network, subprocesses, devices, locks, other threads, or external services;
- the operation can block or wait;
- the operation can take an unpredictable amount of CPU time;
- the operation performs bulk parsing, indexing, decoding, encoding, synthesis, compression, hashing, search, inference, compilation, or migration;
- the operation requires a blocking receive, thread join, sleep, process wait, or contended lock;
- the operation is `async` in syntax but still executes substantial CPU work on the interactive executor/thread between yield points.

Examples normally prohibited on the interactive thread:
- reading or writing user documents synchronously;
- scanning directories;
- parsing large PDF/EPUB/HTML documents;
- database scans or migrations;
- image decode/resize for substantial assets;
- TTS synthesis;
- audio decode/transcode;
- full-text search/index construction;
- network requests;
- process spawning followed by synchronous wait;
- compression/decompression of nontrivial payloads;
- large serialization/deserialization;
- model inference;
- `join`, blocking `recv`, `sleep`, or `block_on`;
- waiting for a mutex that may be held by background work.

## The classification test

Do not ask `does this code look small?`.

Ask:

> **Can I state a tight upper bound on how long this work can occupy the interactive thread, independent of normal user data size and external latency?**

If the answer is no, move it off the interactive thread.

A task that is fast in today's test case but O(n) over user content is not interactive-thread work merely because n is currently small.

## Frame-budget rule

The interactive path should consume only a small and predictable fraction of the target frame budget.

Do not encode one universal millisecond threshold because refresh rates and workloads differ.

The architectural requirement is:
- bounded;
- predictable;
- non-blocking;
- low enough that normal UI composition retains headroom.

## Framework-required exceptions

Some frameworks require particular API calls or final object mutation on the UI thread.

When that happens, split the operation:

    background preparation
      -> compact result
      -> lightweight UI-thread commit

Do not use a framework's thread-affinity requirement as justification for doing the expensive preparation there too.

## Startup and shutdown

Heavy work before the interactive loop begins or after it has fully ended is not a violation of this specific invariant because no interactive latency is being protected.

However, once a window is visible and expected to respond, startup/loading work should generally follow the same background-work rule.

## Rendering itself

Actual layout/render submission that the GUI framework necessarily performs on the interactive/render path is allowed.

But expensive preparation for rendering should still be moved away when possible.

Examples:
- preprocess large geometry off-thread, then submit compact render data;
- decode/resize images off-thread, then upload/apply the result;
- compute expensive visualization data off-thread, then draw the prepared representation.

## Review invariant

A feature is architecturally incomplete if it works correctly but can freeze, hitch, or stall interaction because heavy work is coupled to the interactive thread.

Responsiveness is not polish added after correctness.

It is part of correctness for an interactive system.

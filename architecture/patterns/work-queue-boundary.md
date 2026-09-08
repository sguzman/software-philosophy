# Pattern — Work Queue Boundary

Modality: **CURRENT DEFAULT PATTERN**

Purpose: satisfy interactive-thread isolation by moving expensive work behind an asynchronous execution boundary.

## Canonical flow

    UI input
      -> create typed work request
      -> enqueue
      -> worker / worker pool / async I/O runtime
      -> produce typed progress/result/error event
      -> result queue
      -> interactive thread non-blockingly drains result
      -> apply small UI-state update
      -> request repaint

The exact queue/runtime is an implementation detail.

## UI-side responsibilities

The interactive thread may:
- create a job request;
- assign a job/generation ID;
- enqueue without blocking;
- update `loading/progress/cancelled` view state;
- poll with non-blocking operations such as `try_recv`-style semantics;
- reject stale results;
- apply finished results;
- request repaint.

It must not wait for the worker.

## Worker-side responsibilities

The worker owns:
- CPU-heavy work;
- blocking I/O;
- parsing/indexing/decoding/synthesis;
- retry loops that belong to the operation;
- progress production;
- cancellation checks;
- converting failure into a typed error/result.

The worker should not directly mutate GUI widget state.

Return data across the boundary instead.

## Boundedness and backpressure

Prefer bounded queues or explicit coalescing when work can be produced faster than it can be consumed.

Examples:
- a search box should not necessarily execute every obsolete query after the user typed five more characters;
- repeated resize/image requests may coalesce to the latest generation;
- only a bounded number of expensive jobs should be active.

Unbounded `spawn a thread/task on every click` is not a substitute for architecture.

## Stale-result protection

Long-running work can finish after the user has moved on.

Associate work with identity:

    document_id
    request_id / generation
    operation kind

Apply a result only if it still matches the UI's current intent.

## Cancellation

Tasks that become obsolete should be cancellable when practical.

Cancellation can be cooperative.

The important property is that stale work does not monopolize resources or overwrite newer state.

## Progress

Long work should report progress/events rather than forcing the UI to infer activity from thread state.

Progress events are informational; they should remain cheap to process.

## Rust mapping

In Rust, valid implementations include:
- a dedicated worker thread plus channels;
- a small worker pool;
- `std::sync::mpsc`, crossbeam/flume-style channels, or equivalent;
- an async runtime for genuinely asynchronous I/O;
- `spawn_blocking`/dedicated CPU workers when using an async runtime.

The doctrine does not mandate a crate.

Important Rust-specific warning:

> `async` does not mean `runs off the UI thread`.

A CPU-heavy future polled on the interactive thread still blocks interaction.

## Lock rule

Message passing is the preferred UI/worker boundary.

Shared locks may exist, but the interactive thread must not depend on a lock that background work can hold for a meaningful duration.

Never hold a shared lock across expensive work.

## Shutdown

Worker lifecycle should be explicit.

On shutdown:
- stop accepting new work;
- signal cancellation/closure;
- avoid deadlocking the UI thread while waiting;
- join workers only from a context where blocking is acceptable, or use a shutdown design that preserves responsiveness.

# Project Architecture Principles

Global software architecture doctrine applies unless an explicit project decision records a justified exception.

## Interactive thread

Hard invariant:

> A latency-critical interactive thread may orchestrate; it may not labor.

Project interactive thread(s):

Allowed lightweight responsibilities:

Heavy/background execution boundary:

Result-delivery mechanism:

Cancellation/backpressure/stale-result policy:

## Additional project principles

Record empirically earned structural rules here.

# ADR 0001: Batch first, streaming later

**Status:** Proposed

## Context
Purchase-to-pay delays are measured in days and weeks. The earliest useful warning is "this case has waited longer than usual", and being a few hours late costs little. Streaming the ERP's changes in real time adds moving parts, cost, and operational risk.

## Decision
Load data in scheduled batches, at least daily. Build the event log, score open cases, and create alerts after each load.

## Consequences
- Simple to run, test, and rebuild. A failed run is retried, not repaired mid-stream.
- Alerts can be up to one batch interval late. That is acceptable for waits measured in days.
- If a use case needs minutes, such as fraud checks, this decision must be revisited for that case only.

## Alternatives considered
- **Change-data-capture streaming from the start.** Gives lower latency, but needs streaming infrastructure and expertise the first release does not justify.
- **Hourly batches.** A cheap middle step if daily proves too slow. The design allows it without changing the architecture.

## Revisit when
Data volume grows by about two orders of magnitude, or a stakeholder shows a decision that loses value when delayed by a day.

# ADR 0005: Deliver alerts as tickets with an owner and a feedback step

**Status:** Proposed

## Context
The prototype only produced a file of alerts. In use, an alert nobody owns is ignored, and a system that cannot learn which alerts were useful cannot improve its 31 percent precision.

## Decision
Send act-tier alerts to the team's existing ticketing or chat tool, assigned to a named queue. Each alert records the case, step, wait, threshold, event log version, and rule version. Closing the ticket asks for a useful or not useful rating that flows back to the alert service.

## Consequences
- Alerts fit existing work habits and have a clear owner and a closing step.
- The ratings give a measurable precision per segment and the labeled data for ADR 0003.
- The system depends on a ticketing integration and on people closing tickets honestly. Reporting on unrated alerts keeps this visible.
- A low-priority watch tier appears only on dashboards, so tickets stay limited to cases where action matters.

## Alternatives considered
- **Email digests.** Simple, but there is no owner, no status, and no feedback.
- **Dashboard only.** Good for analysis, but nobody is prompted to act.

## Revisit when
Ratings show a segment's precision stays too low to justify tickets, in which case move it to a dashboard-only view.

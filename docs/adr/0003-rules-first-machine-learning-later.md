# ADR 0003: Start with threshold rules, test machine learning later

**Status:** Proposed

## Context
The prototype's rule (alert when a step exceeds the 90th percentile of past waits) reached 98 percent recall and 31 percent precision on simulated data. A learned model might separate late cases better, but there is no real data yet, no labeled alerts, and the people who receive alerts need to know why one fired.

## Decision
Release version 1 with threshold rules, segmented by vendor group or company code. Collect useful or not useful ratings on every alert. Test a learned model only after several months of real data and ratings, and adopt it only if it beats the rule on a held-out period.

## Consequences
- Every alert can say exactly which step, which wait, and which threshold.
- Rules are cheap to run and easy to review with process owners.
- Precision may be limited. The design accepts that and relies on tiers, suppression, and feedback to keep alert volume useful.
- The ratings collected from the start become the labeled data a later model needs.

## Alternatives considered
- **Train a model before launch.** There is no real labeled data, so it would be trained and tested on simulated cases and would prove little.
- **A process-mining platform's built-in prediction.** Possible, see ADR 0004, but the same evaluation rule applies: judge it on held-out real cases.

## Revisit when
There are enough rated alerts (for example several thousand across segments) to train and test on separate periods.

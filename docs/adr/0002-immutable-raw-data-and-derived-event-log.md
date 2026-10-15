# ADR 0002: Keep raw extracts immutable and derive the event log from them

**Status:** Proposed

## Context
Event logs are built by rules: which tables, which timestamps, how to handle partial deliveries. Those rules will change as the business corrects them. Auditors also ask how a past number was produced.

## Decision
Store every extract exactly as received, never edited, tagged with a run identifier. Build the event log as a derived, versioned product that can be recreated by running the builder over the raw files.

## Consequences
- Any past event log version can be rebuilt, which supports audit and bug fixes.
- A change in event definition is a code change plus a rebuild, with the effect visible before it goes live.
- Storage grows with every extract. Retention is set by the client's policy, and storage cost is small compared with the cost of an unexplainable number.

## Alternatives considered
- **Transform on the way in and keep only the event log.** Smaller, but a mistake in the rules cannot be repaired without a new extract from the ERP, and the original data is gone.
- **Query the ERP directly each time.** No storage, but it loads the production system and gives different answers on different days.

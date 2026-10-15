# Process Mining and Early Warning: Architecture Package

A design for taking a purchase-to-pay process mining and early-warning prototype to a production system. It is a written design package: a design document, five decision records, and diagrams that GitHub draws directly from text.

**Status: design proposal.** Nothing in this repository is deployed. The only working code behind it is the prototype in [p2p-process-mining](https://github.com/OK-22/p2p-process-mining), which runs on a simulated purchase-to-pay log. Targets, volumes, and costs here are proposals and assumptions, and each is marked as one.

## Start here
| Document | What it covers |
|---|---|
| [docs/design.md](docs/design.md) | Goals, requirements, architecture, data design, early-warning design, security, operations, rollout, risks |
| [docs/adr/0001-batch-first-streaming-later.md](docs/adr/0001-batch-first-streaming-later.md) | Why the first version loads data in batches |
| [docs/adr/0002-immutable-raw-data-and-derived-event-log.md](docs/adr/0002-immutable-raw-data-and-derived-event-log.md) | Why raw extracts are kept unchanged and the event log is rebuilt from them |
| [docs/adr/0003-rules-first-machine-learning-later.md](docs/adr/0003-rules-first-machine-learning-later.md) | Why alerts start as threshold rules |
| [docs/adr/0004-build-or-buy-the-mining-engine.md](docs/adr/0004-build-or-buy-the-mining-engine.md) | How to choose between an open-source engine and a commercial platform |
| [docs/adr/0005-alerts-go-through-the-ticketing-system.md](docs/adr/0005-alerts-go-through-the-ticketing-system.md) | Why alerts become tickets with an owner and a feedback step |

## The idea in one paragraph
Purchase orders, goods receipts, and invoices leave a trail of timestamps in an ERP system. The design turns that trail into an event log, measures how long each step normally takes, and raises an alert when an open case waits longer than usual at a step. The prototype found that one step (goods receipt to invoice receipt) held most of the delay, and that a simple threshold rule could flag late cases early. The prototype's alerts were right about 31 percent of the time, so the design spends as much effort on controlling false alarms as on finding late cases.

## What the prototype showed, and what it did not
| Prototype result (simulated data) | What it means for the design |
|---|---|
| 20,000 cases, 92,659 events, 8 process variants, 12 percent rework | The event-log shape works. Real data will be messier, so data quality checks are a first-class component |
| Largest delay between goods receipt and invoice receipt (14.5 days mean wait) | Analysis should be broken down by vendor and company code, not one global number |
| Threshold rule: 98 percent recall, 31 percent precision, 3.2x lift on a 30 percent holdout | Recall was high, but about 2 in 3 alerts were false alarms. Alert fatigue is the main product risk |
| Data was simulated | None of these numbers predict real performance. Phase 1 exists to measure it on real data |

## Related repositories
- [p2p-process-mining](https://github.com/OK-22/p2p-process-mining): the prototype
- [monitoring-homelab](https://github.com/OK-22/monitoring-homelab): the monitoring and runbook approach reused in the operations design
- [cloud-pipeline](https://github.com/OK-22/cloud-pipeline): the CI and container pipeline pattern reused for deployment

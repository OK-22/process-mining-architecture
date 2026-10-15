# ADR 0004: Choosing between an open-source engine and a commercial platform

**Status:** Open (depends on facts not yet known)

## Context
Two reasonable routes exist for discovery, variant analysis, and bottleneck views: build on an open-source library (the prototype uses PM4Py with pandas) or use a commercial process mining platform with ready-made SAP extraction and dashboards.

## Decision criteria
| Question | Leans toward building | Leans toward buying |
|---|---|---|
| Is a commercial platform already licensed? | No | Yes, use it and add the alerting layer |
| How much custom alert logic is needed? | A lot, and tightly tied to local rules | Standard dashboards are enough |
| Is the team comfortable running data pipelines? | Yes | No |
| Is there budget for licenses and support? | Limited | Available |
| How fast is the first result needed? | Time is available | Soon, with ready-made SAP connectors |

## Decision
Deferred to Phase 0. If a platform is already licensed, use it for extraction and analysis and build only the alert, feedback, and audit parts around it. Otherwise build on the open-source stack described in the design.

## Consequences
- The rest of the design holds either way: the event log schema, the alert lifecycle, and the quality measures do not depend on the engine.
- Choosing a platform trades flexibility and license cost for speed and supported connectors.

## Alternatives considered
- **Build everything.** Maximum control, highest effort, and the team owns every fix.
- **Buy everything.** Fastest, but alert tiers, suppression, and feedback may not fit the platform's model.

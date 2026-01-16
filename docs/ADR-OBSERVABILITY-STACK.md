# ADR: Unified Observability Stack (Grafana LGTM)

**Status:** Accepted
**Date:** 2024-04-01

## Context

Need unified observability for logs, metrics, and traces.

## Decision

Use Grafana LGTM stack with Alloy as unified collector:
- **L**oki for logs
- **G**rafana for visualization
- **T**empo for traces
- **M**imir for metrics
- **Alloy** for collection

## Rationale

| Approach | Pros | Cons |
|----------|------|------|
| Separate tools | Best-of-breed | Complex, multiple UIs |
| **Grafana stack** | Unified, correlated | Single vendor | **Selected** |
| Cloud services | Zero ops | Cost, vendor lock-in |

**Key Decision Factors:**
- Single pane of glass
- Trace-to-log correlation
- Self-hosted (cost control)
- Open source

## Components

| Component | Purpose | Memory |
|-----------|---------|--------|
| Loki | Log aggregation | ~500MB |
| Grafana | Visualization | ~200MB |
| Tempo | Distributed tracing | ~300MB |
| Mimir | Metrics storage | ~500MB |
| Alloy | Unified collector | ~400MB x3 |
| **Total** | | ~3GB |

## Alloy Consolidation

Alloy replaces multiple collectors:
- Promtail → Alloy
- node_exporter → Alloy
- OTel Collector → Alloy

## Consequences

**Positive:** Unified view, correlation, cost control, open source
**Negative:** Self-hosted ops, ~3GB memory overhead

## Related

- [SPEC-OBSERVABILITY-STACK](./SPEC-OBSERVABILITY-STACK.md)
- [ADR-LOGGING-LOKI](./ADR-LOGGING-LOKI.md)
- [ADR-TRACING-TEMPO](./ADR-TRACING-TEMPO.md)
- [ADR-METRICS-MIMIR](./ADR-METRICS-MIMIR.md)

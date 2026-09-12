---
name: reliability
last_reviewed: 2026-09-06
group: Ship and run
description: >-
  Set SLOs and error budgets, instrument with OpenTelemetry, and build the dashboards that prove
  them. Use when designing SLIs/SLOs, circuit breakers, or disaster recovery.
---

# Reliability

Implements comprehensive observability stacks using OpenTelemetry, designs SLO-driven dashboards, and architects actionable alerting systems.

## Phased Workflow

### Phase 1: Instrumentation & Telemetry Design
1. Instrument services with OpenTelemetry SDK: distributed traces (spans with context propagation), metrics (counters, histograms, gauges), and structured logs.
2. Define trace sampling strategy (head-based vs tail-based) balancing cost and visibility.
3. Standardize log schema: timestamp, service, trace_id, span_id, level, message, structured fields.

### Phase 2: SLO/SLI Framework
1. Define Service Level Indicators (SLIs): availability (success rate), latency (P50/P95/P99), throughput, error rate.
2. Set Service Level Objectives (SLOs): target thresholds with error budgets (e.g., 99.9% availability = 43.8 min/month budget).
3. Build burn-rate alerting: alert when error budget consumption rate exceeds sustainable pace.

### Phase 3: Dashboard & Alert Architecture
1. Design golden signal dashboards: Rate, Errors, Duration (RED) per service.
2. Configure multi-window, multi-burn-rate alerts to minimize false positives.
3. Implement alert routing with escalation tiers and on-call rotation integration.

## Verification & Quality Checklist
- [ ] All services emit traces with proper context propagation across async boundaries.
- [ ] SLOs documented with clear ownership and review cadence (monthly).
- [ ] Alert noise ratio below 10% false positive rate.
- [ ] Dashboards load in under 3 seconds and cover all golden signals.

## Anti-Patterns & Constraints
- NEVER alert on raw metric thresholds without error budget context.
- NEVER log sensitive PII, credentials, or full request bodies in production.
- NEVER create dashboards without a clear debugging narrative (what question does each panel answer?).

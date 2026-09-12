---
name: incident-response
last_reviewed: 2026-09-06
group: Ship and run
description: >-
  Run a live incident: severity call, triage, stakeholder comms, mitigation and the writeup. Use
  when managing live production outages, triage, or post-mortems.
---

# Incident Response

Directs critical production incident response, manages triage channels, coordinates technical remediation, and facilitates blameless post-mortems.

## Phased Workflow

### Phase 1: Triage & Classification (First 5 Minutes)
1. Assess blast radius and assign Severity Level:
   - **SEV-1 (Critical):** Core revenue/production down, data corruption, severe security breach.
   - **SEV-2 (Major):** Major feature broken for significant user subset, no simple workaround.
   - **SEV-3 (Moderate):** Minor degradation, non-critical workflow impacted.
2. Establish Incident Command channel and assign roles: Incident Commander (IC), Technical Lead (TL), Communications Lead (CL).

### Phase 2: Containment & Stabilization
1. Prioritize **Mitigation over Root Cause Identification** (e.g., rollback deployment, toggle feature flags, divert traffic, scale instances).
2. Maintain an timestamped incident log of all actions, hypotheses, and telemetry changes.
3. Broadcast internal and customer status updates at structured intervals (every 15 min for SEV-1, 30 min for SEV-2).

### Phase 3: Resolution & Verification
1. Confirm telemetry (error rates, latencies, resource saturation) returns to baseline.
2. Monitor canary period for 30–60 minutes before declaring incident resolved.

### Phase 4: Blameless Post-Mortem & Prevention
1. Construct 5-Whys timeline and causal graph.
2. Formulate preventive Action Items (Actionable, Measurable, Assigned, Prioritized).

## Verification & Quality Checklist
- [ ] Customer impact start and end times recorded accurately in UTC.
- [ ] Telemetry metrics (P99 latency, error rate %) verified against SLO thresholds.
- [ ] Rollback or fix verified in staging/canary before full fleet deployment.
- [ ] Post-mortem includes root cause, contributing factors, timeline, and remediation tickets.

## Anti-Patterns & Constraints
- NEVER perform in-depth code debugging in production during an active SEV-1 when a safe rollback is available.
- NEVER assign blame to individuals in post-mortems (focus on systemic safeguards).
- NEVER close an incident without verifying baseline telemetry over a soak period.

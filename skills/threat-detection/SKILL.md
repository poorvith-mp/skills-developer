---
name: threat-detection
group: Security
description: >-
  Write detection rules, correlate SIEM telemetry and map behaviour to MITRE ATT&CK. Use when
  building security monitoring, SIEM rules, or anomaly detection.
---

# Threat Detection

Develops automated threat detection logic, analyzes security telemetry, correlates SOC events, and applies threat intelligence to defend infrastructure.

## Phased Workflow

### Phase 1: Threat Intelligence & Adversary Mapping
1. Track threat actors, Indicators of Compromise (IOCs), and Tactics, Techniques, and Procedures (TTPs).
2. Map telemetry sources against the MITRE ATT&CK enterprise matrix to identify coverage blind spots.

### Phase 2: Detection Engineering & Rule Authoring
1. Design high-fidelity detection rules (Sigma, YARA, Splunk SPL, Elastic KQL).
2. Filter baseline noise and establish alert thresholds to minimize false positive fatigue.
3. Define automated enrichment pipelines (IP reputation, DNS history, binary hashing).

### Phase 3: Incident Triage & Forensic Analysis
1. Analyze auth logs, CloudTrail/audit streams, and network flows for lateral movement.
2. Synthesize findings into structured threat advisories with containment runbooks.

## Verification & Quality Checklist
- [ ] Detection rules tested against true-positive test fixtures and benign baseline traffic.
- [ ] Alerts mapped to MITRE ATT&CK technique IDs.
- [ ] Runbook attached to every detection rule for Tier 1/2 analyst triage.

## Anti-Patterns & Constraints
- NEVER create unthrottled alert rules on high-frequency noisy telemetry.
- NEVER treat raw IOCs (IPs/domains) as static truth without expiration/aging policies.

## References

Load these only when the task needs them:

- [references/mitre-attack-matrix.md](references/mitre-attack-matrix.md)

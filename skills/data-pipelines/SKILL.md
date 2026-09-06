---
name: data-pipelines
group: Data and AI
description: >-
  Build ETL/ELT and streaming pipelines with quality validation, schema evolution and anomaly
  correction. Use when building ETL/ELT pipelines, streaming data, or schema validation.
---

# Data Pipelines

Architects reliable, scalable data pipelines from ingestion through transformation to serving, with built-in quality validation and schema governance.

## Phased Workflow

### Phase 1: Source Analysis & Architecture Selection
1. Inventory data sources: APIs, databases, event streams, file drops, SaaS webhooks.
2. Classify each pipeline: Batch (hourly/daily, high volume) vs Streaming (real-time, event-driven).
3. Select architecture pattern: ELT (extract-load-transform in warehouse) vs ETL (transform before load).

### Phase 2: Pipeline Implementation
1. Design idempotent, retry-safe extraction with checkpoint/offset tracking.
2. Implement transformations using dbt models (staging → intermediate → marts) or Spark jobs.
3. Define schema evolution strategy: additive-only columns, versioned schemas, backward-compatible migrations.

### Phase 3: Data Quality & Observability
1. Implement data quality checks at every pipeline stage: freshness, completeness, uniqueness, referential integrity.
2. Build data lineage graphs tracking field-level transformations from source to dashboard.
3. Configure pipeline monitoring: job duration, row counts, failure rates, SLA breach alerts.

## Verification & Quality Checklist
- [ ] All pipelines are idempotent and safely re-runnable without data duplication.
- [ ] Schema changes are backward compatible and documented in migration logs.
- [ ] Data quality tests cover freshness (data is recent), volume (expected row counts), and validity (no nulls in required fields).
- [ ] Pipeline SLAs defined with automated alerting on breach.

## Anti-Patterns & Constraints
- NEVER build pipelines without idempotency guarantees.
- NEVER perform destructive schema changes (column drops/renames) without a migration period.
- NEVER skip data quality validation between ingestion and serving layers.

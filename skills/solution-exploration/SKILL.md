---
name: solution-exploration
last_reviewed: 2026-09-06
group: Plan
description: >-
  Diverge before committing: generate genuinely different approaches, name trade-offs, and kill
  what doesn't survive. Use when exploring architectural trade-offs.
---

# solution-exploration

## Core Philosophy
Jumping directly into implementation on the first technical solution that comes to mind is the leading cause of technical debt, architectural dead-ends, and expensive rewrites. Great software architects deliberately diverge before they converge. High-leverage solution exploration systematically generates at least three fundamentally distinct architectural approaches, quantifies non-functional trade-offs, stress-tests edge cases through throwaway spikes, and documents the rationale in an Architectural Decision Record (ADR).

---

## 4-Step Solution Exploration Framework

### Step 1: Problem Space Framing & Non-Negotiable Constraints
1. **Deconstruct the Technical Problem**:
   - Separate functional requirements (what the system does) from non-functional requirements (NFRs: latency, throughput, cost, consistency, operational complexity).
2. **Define Hard Constraints & Guardrails**:
   - Budget ceilings (e.g. infra spend $< $500/text{month}$).
   - Latency boundaries (e.g. p99 response $< 50text{ms}$).
   - Team capabilities (e.g. no unfamiliar languages without strong rationale).

### Step 2: Divergent Solution Generation (The Rule of 3)
1. **Force 3 Radically Distinct Approaches**:
   - *Option 1: The Native / Minimalist (Standard Library / Existing Stack)*: Leverage tools already deployed in the stack. Zero new dependencies.
   - *Option 2: The Managed Cloud / SaaS Approach*: Outsource complexity to managed services (e.g. AWS SQS, Supabase, Cloudflare Workers). High velocity, higher ongoing operating cost.
   - *Option 3: The Specialized High-Performance Engine*: Introduce a purpose-built technology (e.g. Rust microservice, ClickHouse, Redis Cluster). High throughput, higher operational maintenance.

### Step 3: Trade-Off Matrix & Spike Prototyping
1. **The 5-Dimension Evaluation Matrix**:
   - Rate each option (1–5) on:
     - 1. Development Velocity (Time to Ship).
     - 2. Operational Complexity & Maintenance Burden.
     - 3. Total Cost of Ownership (TCO: Compute + Licensing).
     - 4. Scalability & Latency Ceiling.
     - 5. Failure Mode & Disaster Recovery Simplicity.
2. **The Throwaway Spike (Time-Boxed to 4 Hours)**:
   - Build a minimal disposable prototype specifically to answer the single riskiest technical question (e.g., "Can SQLite handle 500 concurrent writes without database lock errors?").

### Step 4: Convergence & Architectural Decision Record (ADR)
1. **Kill the Losers**:
   - Explicitly document why the unselected options were rejected.
2. **Draft the Formal ADR**:
   - Capture Context, Decision, Consequences (positive and negative), and Review Schedule.

---

## Deliverable Format: Architectural Decision Record (`ADR-00X.md`)

```markdown
# ADR-004: Asynchronous Background Job Processing Architecture

## Status: ACCEPTED
**Date**: [YYYY-MM-DD] | **Author**: Platform Architecture Team

## Context & Problem Statement
Our application needs to process 500,000 PDF export jobs daily. Synchronous HTTP handling is causing timeout errors and memory spikes on web servers. We need an asynchronous background job processing system that supports retries, rate limiting, and priority queues.

## Evaluated Alternatives
1. **Option A: PostgreSQL `pg_boss` / `graphile-worker`** (Leveraging existing Postgres database).
2. **Option B: Redis + BullMQ** (Dedicated in-memory queue cluster).
3. **Option C: AWS SQS + Lambda** (Serverless managed queue).

## Trade-Off Evaluation Matrix
| Dimension | Option A (Postgres) | Option B (Redis/BullMQ) | Option C (AWS SQS) |
|---|---|---|---|
| New Infra Dependencies | None (Already run RDS) | High (Requires Redis cluster) | Medium (Cloud vendor lock-in) |
| Max Throughput | ~2,000 jobs/sec | ~25,000 jobs/sec | Unlimited |
| Operational Overhead | Low | Medium | Very Low |
| Monthly Compute Cost | $0 (Existing DB) | +$140/mo | +$45/mo |

## Decision & Rationale
We choose **Option A (PostgreSQL with `graphile-worker`)**.
- *Rationale*: Our current volume (60 jobs/sec peak) is well within PostgreSQL capabilities. Avoiding a new Redis infrastructure cluster saves operational maintenance and $1,680/year in cloud hosting.
- *Migration Trigger*: If sustained job throughput exceeds 1,500 jobs/sec, we will re-evaluate Option B.

## Negative Consequences & Trade-offs
- High job volumes will increase PostgreSQL write amplification and vacuum overhead.
- Requires monitoring database connection pool limits.
```

---

## Worked Example: Search Architecture Exploration

- **Problem**: Full-text search across 2M product descriptions was sluggish on PostgreSQL using raw `LIKE` queries.
- **Exploration**: Evaluated Elasticsearch vs Typesense vs PostgreSQL `tsvector` with GIN indexing.
- **Spike**: Built a 2-hour benchmark testing `tsvector` with GIN indices against a 2M-row replica.
- **Outcome**: `tsvector` delivered 18ms search latencies. Decided against Elasticsearch, saving $400/month and eliminating cluster maintenance.

---

## Verification Checklist

- [ ] At least 3 fundamentally distinct technical approaches are evaluated.
- [ ] Evaluation matrix includes ongoing operational maintenance and total cost.
- [ ] Riskiest technical assumptions are validated via a time-boxed throwaway spike.
- [ ] Reasons for rejecting unselected options are explicitly documented.
- [ ] Formal ADR is signed off and committed to the repository `docs/adr/`.

---

## Anti-Patterns

- **Resume-Driven Development**: Choosing a complex distributed system (e.g. Kafka or Kubernetes) when a lightweight cron job or Redis queue suffices.
- **The Pseudo-Choice**: Evaluating Option A (the chosen favorite) against two absurd strawmen designed to fail.
- **Premature Convergence**: Starting coding within 5 minutes of hearing a problem without exploring alternatives.

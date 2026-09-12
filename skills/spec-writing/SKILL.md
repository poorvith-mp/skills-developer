---
name: spec-writing
last_reviewed: 2026-09-06
group: Plan
description: >-
  Turn a vague request into a written spec: scope, non-goals, acceptance criteria and the edge
  cases that will bite. Use when writing technical specifications, scope, and acceptance criteria.
---

# spec-writing

## Core Philosophy
A technical specification is not an essay or a loose collection of wishes. A spec is a rigorous engineering contract that bridges product requirements with software reality. Great specs clarify exact boundaries, eliminate ambiguity, define non-goals, classify failure modes, and specify verifiable acceptance criteria before a single line of code is written. If an edge case is discovered during implementation, the spec failed to do its job.

---

## 4-Step Technical Specification Architecture

### Step 1: Problem Statement & Explicit Non-Goals
1. **The Problem Formulation**:
   - Describe the user friction and commercial impact in 2 crisp paragraphs. Avoid solution jargon in the problem statement.
2. **The Non-Goals Mandate**:
   - The most valuable section of any spec is what you are **NOT** building.
   - Example: *"Non-Goal: We are not supporting multi-region database failover or offline local sync in v1.0."* This protects engineering from infinite scope creep.

### Step 2: System Architecture & Data Contract Design
1. **Data Model & Schema Definitions**:
   - Document exact database tables, column types, foreign key constraints, and indices.
2. **API & Interface Contracts**:
   - Specify HTTP endpoints, request headers, JSON payloads, response codes, and error formats:
     ```json
     {
       "error": {
         "code": "INVALID_ORGANIZATION_ID",
         "message": "Organization does not exist or is suspended",
         "details": {}
       }
     }
     ```

### Step 3: Edge Case Taxonomy & Failure Modes
1. **Systematic Edge Case Identification**:
   - *Concurrency & Race Conditions*: What happens if two users click "Book Seat" at the exact same millisecond? (Enforce database-level transactions and row-level locking).
   - *Network & Partitions*: What happens if the third-party payment gateway times out after charging the card but before returning the HTTP response? (Enforce Idempotency Keys).
   - *Boundary Conditions*: Null inputs, unicode emojis, multi-megabyte payloads, zero-length arrays.
   - *Permissions & Tenancy*: Can User A craft an API request that modifies User B's resource?

### Step 4: Verifiable Acceptance Criteria (BDD / Gherkin)
1. **Behavior-Driven Development (Given-When-Then)**:
   - Formulate unambiguous acceptance criteria that can be directly translated into automated tests:
     ```gherkin
     Scenario: User reaches free tier project limit
       Given an active user on the Free Plan with 3 existing projects
       When the user submits a request to create a 4th project
       Then the API responds with HTTP 403 Forbidden
       And the error payload contains code "QUOTA_EXCEEDED"
       And the upgrade paywall modal is returned
     ```

---

## Deliverable Format: Technical Specification Document (`SPEC.md`)

```markdown
# Technical Specification: [Feature Name]

## 1. Overview & Business Value
- **Author**: [Lead Engineer] | **Status**: [Draft / In Review / Approved]
- **Target Release**: [vX.Y.Z]
- **Problem Statement**: [Why this feature must exist]
- **Target Persona**: [Who will use this]

## 2. Explicit Non-Goals
- Will NOT support [Feature X] in v1.
- Will NOT migrate legacy records prior to 2025.

## 3. Data Models & API Contracts
### Database Schema
```sql
CREATE TABLE audit_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    org_id UUID NOT NULL REFERENCES organizations(id) ON DELETE CASCADE,
    actor_id UUID NOT NULL REFERENCES users(id),
    action VARCHAR(64) NOT NULL,
    metadata JSONB NOT NULL DEFAULT '{}',
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);
CREATE INDEX idx_audit_logs_org_created ON audit_logs(org_id, created_at DESC);
```

### API Endpoint: `POST /api/v1/audit-logs`
- **Request Body**: `{"action": "string", "metadata": "object"}`
- **Success Response**: HTTP 201 Created

## 4. Edge Cases & Safety Mitigations
- **Race Conditions**: Protected by PostgreSQL advisory locks on `org_id`.
- **Idempotency**: Client must pass `Idempotency-Key` header; cached in Redis for 24h.

## 5. Acceptance Criteria (Gherkin)
- **Scenario 1**: Valid creation returns 201 with UUID.
- **Scenario 2**: Missing `Idempotency-Key` on duplicate request returns 400.
```

---

## Worked Example: Specifying an Idempotent Payment API

- **Challenge**: Network jitter caused mobile users to double-click payment buttons, resulting in duplicate charges.
- **Spec Solution**: Mandated an `Idempotency-Key` header stored in Redis with atomic `SET NX EX 86400`.
- **Verification**: Gherkin test simulated 50 concurrent requests with identical idempotency keys; confirmed exactly 1 charge was processed and 49 received cached 200 responses.

---

## Verification Checklist

- [ ] Problem statement clearly articulates user pain without prescribing solutions.
- [ ] Explicit non-goals list defines the project perimeter.
- [ ] Data models and API contracts provide exact schemas and status codes.
- [ ] Concurrency, failure modes, and race conditions have documented mitigations.
- [ ] Acceptance criteria follow Given-When-Then format for automated test translation.

---

## Anti-Patterns

- **The Hand-Waving Spec**: Writing "The backend will handle syncing securely and reliably" without defining protocols or error codes.
- **Missing Non-Goals**: Allowing stakeholders to continuously add requirements during sprints because boundaries were never set.
- **Untestable Criteria**: Writing vague acceptance criteria like "The system should be fast and intuitive."

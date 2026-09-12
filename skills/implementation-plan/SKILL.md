---
name: implementation-plan
last_reviewed: 2026-09-06
group: Plan
description: >-
  Break the change into ordered, reviewable steps with checkpoints, so a long task can be stopped
  and resumed. Use when breaking changes into ordered, testable steps with checkpoints.
---

# implementation-plan

## Core Philosophy
Diving directly into code on complex architectural refactors without a written implementation plan leads to broken builds, forgotten edge cases, scope creep, and irreversible git wreckage. An implementation plan is an engineering blueprint. It breaks complex tasks into ordered, bite-sized increments with testable verification checkpoints at each step—ensuring that long-running work can be stopped, reviewed, and resumed at any time with complete confidence.

---

## 4-Step Implementation Planning Discipline

### Step 1: Scope, Architecture & Dependency Ordering
1. **Dependency Inversion Ordering**:
   - Order components logically so that dependencies are created *before* dependents:
     - 1. Core Data Models / Database Schema Migrations.
     - 2. Internal Services / Business Logic.
     - 3. API Endpoints / Controllers.
     - 4. Frontend UI / Consumer Integration.
2. **Explicit Non-Goals**:
   - Clearly delineate what will *not* be built in this iteration to prevent scope creep.

### Step 2: Atomic Phase Breakdown & Checkpoint Design
1. **The 30-Minute Task Rule**:
   - Break work down into discrete tasks that take $\le 30$ minutes to implement and verify.
2. **Verification Checkpoints**:
   - Every single task must have an explicit verification step:
     - "Run `npm test src/auth.test.ts` -> Expect 4 passing tests."
     - "Run `curl -I http://localhost:3000/api/health` -> Expect 200 OK."

### Step 3: TDD Integration & Regression Defense
1. **Test-First Stance**:
   - Specify the automated test files to be written *before* the implementation code is touched.
   - Define expected failure conditions (red) and passing criteria (green).

### Step 4: Rollback & Risk Mitigation Protocol
1. **De-risking Breaking Changes**:
   - Use the **Expand and Contract (Parallel Run)** pattern for schema and API changes:
     - Phase 1 (Expand): Add new field/endpoint; support both old and new.
     - Phase 2 (Migrate): Shift traffic to new field/endpoint.
     - Phase 3 (Contract): Deprecate and remove old field/endpoint.

---

## Deliverable Format: Implementation Plan Template (`IMPLEMENTATION-PLAN.md`)

```markdown
# Implementation Plan: [Feature / Refactor Name]

## 1. Overview & Architectural Goal
[1-2 paragraphs explaining what the change accomplishes and the architectural rationale.]

## 2. Open Questions & Design Decisions
- [Decision A]: Chosen approach and rationale.
- [Question B]: Awaiting team clarification.

## 3. Ordered Implementation Phases

### Phase 1: Database & Data Model Layer
- [ ] **Task 1.1**: Create migration adding `organization_id` column to `users` table.
  - *Files*: `prisma/migrations/20260906_add_org_id.sql`
  - *Verification*: Run `npx prisma migrate dev` and verify column exists via `psql`.
- [ ] **Task 1.2**: Update Prisma schema and generate client.
  - *Files*: `prisma/schema.prisma`
  - *Verification*: Run `npx prisma generate` -> builds clean.

### Phase 2: Core Domain Logic & Unit Tests
- [ ] **Task 2.1 [TDD]**: Write unit tests for OrgMembershipService.
  - *Files*: `tests/unit/org-service.test.ts`
  - *Verification*: Run `npm test tests/unit/org-service.test.ts` -> Fails (Red).
- [ ] **Task 2.2**: Implement OrgMembershipService methods.
  - *Files*: `src/services/OrgMembershipService.ts`
  - *Verification*: Run `npm test tests/unit/org-service.test.ts` -> Passes (Green).

### Phase 3: API Endpoints & Route Handlers
- [ ] **Task 3.1**: Expose `POST /api/v1/organizations/:id/members`.
  - *Verification*: Execute curl test script against local test server.

## 4. Verification Plan
- **Automated Tests**: `npm run test:all`
- **Lint & Types**: `npm run lint && npm run typecheck`
- **Manual Verification**: End-to-end user invitation flow in local staging browser.
```

---

## Worked Example: Zero-Downtime Database Migration Plan

- **Refactor**: Split single `User.name` column into `User.firstName` and `User.lastName`.
- **Phases**:
  - Phase 1: Added nullable columns `firstName` and `lastName`.
  - Phase 2: Dual-write to both `name` and new columns in application code.
  - Phase 3: Background script backfilled historical rows.
  - Phase 4: Switched reads to `firstName`/`lastName`.
  - Phase 5: Dropped legacy `name` column.
- **Outcome**: 100% zero downtime across 5M production records.

---

## Verification Checklist

- [ ] Tasks are arranged in logical dependency order (data -> logic -> API -> UI).
- [ ] Every individual task includes exact file paths and a verifiable test command.
- [ ] Explicit non-goals are defined to restrict scope.
- [ ] TDD unit tests are scheduled prior to implementation tasks.
- [ ] Rollback strategy is documented for database or API changes.

---

## Anti-Patterns

- **The Monolithic Step**: Writing "Step 1: Build the backend" (too vague, impossible to verify incrementally).
- **Skipping Checkpoints**: Writing 2,000 lines of code across 15 files before running a single test.
- **Unverified Assumptions**: Proceeding with execution while major architectural questions remain unresolved.

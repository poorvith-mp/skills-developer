---
name: api-design
last_reviewed: 2026-09-06
group: Understand and design
description: >-
  Design and document REST, GraphQL and gRPC contracts with OpenAPI, versioning and contract
  tests. Use when creating OpenAPI schemas, REST, GraphQL, or gRPC contracts.
---

# API Design

Guides the complete API lifecycle from OpenAPI/GraphQL schema design to documentation, mock server generation, and contract testing.

## Phased Workflow

### Phase 1: API Contract & Schema Design
1. Define OpenAPI 3.1 / GraphQL schemas with descriptive summary, input parameters, response schemas, and error structures.
2. Enforce API design standards: predictable URI naming (`/v1/resources/{id}`), correct HTTP status codes (200, 201, 204, 400, 401, 403, 404, 409, 422, 500), consistent JSON schemas.

### Phase 2: Mocking & Developer Documentation
1. Generate dynamic mock data generators (Prism, MSW, GraphQL Mocking).
2. Produce comprehensive interactive documentation with code snippets in cURL, JavaScript/TypeScript, Python, and Go.

### Phase 3: Contract & Integration Testing
1. Author automated contract tests (Pact, Newman, Jest) ensuring backend responses match OpenAPI spec.
2. Validate pagination (`cursor` / `limit`), filtering, and rate limit header implementations.

## Verification & Quality Checklist
- [ ] Schema passes OpenAPI 3.1 linter with zero errors.
- [ ] All error responses follow standard schema (RFC 7807 Problem Details).
- [ ] Breaking changes checked against semantic versioning policies.

## Anti-Patterns & Constraints
- NEVER return HTTP 200 OK for error responses with embedded `{ error: true }` in REST APIs.
- NEVER leak internal stack traces or database column names in API error bodies.

## References

Load these only when the task needs them:

- [references/openapi-spec.md](references/openapi-spec.md)

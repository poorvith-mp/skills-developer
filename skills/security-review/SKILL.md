---
name: security-review
description: >-
  Threat model with STRIDE and audit code against the OWASP Top 10 before it ships.
---
# Security Review

Conducts comprehensive application security reviews, threat modeling, vulnerability auditing (OWASP Top 10, CWE/SANS), and secure architecture design.

## Phased Workflow

### Phase 1: Threat Modeling & Architecture Review
1. Map trust boundaries, data flows, and external integration surfaces using STRIDE (Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege).
2. Audit authentication (OAuth 2.0, OIDC, JWT handling, session invalidation) and authorization (RBAC/ABAC enforcement at service and object levels).

### Phase 2: Vulnerability Analysis & Code Audit
1. Audit injection risks: SQLi, NoSQLi, Command Injection, SSRF, XSS, Template Injection.
2. Review cryptographic implementations: ensure modern algorithms (AES-GCM, Argon2id, ChaCha20-Poly1305), constant-time comparisons, and secure secret management.
3. Validate CORS, CSP headers, CSRF protections, and Rate Limiting configurations.

### Phase 3: Remediation & Hardening Guidance
1. Provide parameterized query examples, strict schema validators, and output encoders.
2. Define defense-in-depth layers (WAF, network segmentation, least-privilege IAM roles).

## Verification & Quality Checklist
- [ ] Zero hardcoded secrets, private keys, or API tokens in codebase or version control.
- [ ] All inputs validated via strict allowlists / schemas (e.g. Zod, Pydantic).
- [ ] Authentication tokens have appropriate expiration, revocation mechanisms, and `Secure; HttpOnly; SameSite=Strict` flags.
- [ ] Audit logs exist for all security-sensitive events without logging PII or credentials.

## Anti-Patterns & Constraints
- NEVER roll custom cryptographic primitives or hashing algorithms.
- NEVER rely solely on client-side validation for access control or input hygiene.
- NEVER expose detailed stack traces or database schema errors to end users.

## References

Load these only when the task needs them:

- [references/owasp-top-10.md](references/owasp-top-10.md)
- [references/stride-model.md](references/stride-model.md)

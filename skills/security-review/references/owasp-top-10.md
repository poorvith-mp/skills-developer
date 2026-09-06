# OWASP Top 10 (2021) Quick Reference

| # | Category | Key Controls |
|---|----------|-------------|
| A01 | Broken Access Control | Deny by default, RBAC/ABAC enforcement, CORS restrictions |
| A02 | Cryptographic Failures | TLS 1.2+, AES-256-GCM, Argon2id for passwords, no MD5/SHA1 |
| A03 | Injection | Parameterized queries, input validation, output encoding |
| A04 | Insecure Design | Threat modeling, secure design patterns, abuse case testing |
| A05 | Security Misconfiguration | Hardened defaults, remove unused features, automated config audits |
| A06 | Vulnerable Components | SCA scanning, dependency updates, SBOM maintenance |
| A07 | Auth & Session Failures | MFA, session timeouts, credential stuffing protection |
| A08 | Data Integrity Failures | CI/CD pipeline integrity, signed artifacts, SRI for CDN resources |
| A09 | Logging & Monitoring | Security event logging, alerting, incident response readiness |
| A10 | SSRF | Allowlist outbound URLs, sanitize user-supplied URLs, network segmentation |

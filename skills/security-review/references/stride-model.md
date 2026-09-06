# STRIDE Threat Modeling Reference

| Threat | Property Violated | Example | Mitigation |
|--------|------------------|---------|-----------|
| **S**poofing | Authentication | Fake login page | MFA, certificate pinning |
| **T**ampering | Integrity | Modified API request | HMAC signatures, checksums |
| **R**epudiation | Non-repudiation | Denied action | Audit logs, digital signatures |
| **I**nformation Disclosure | Confidentiality | Leaked PII | Encryption, access controls |
| **D**enial of Service | Availability | DDoS, resource exhaustion | Rate limiting, CDN, autoscaling |
| **E**levation of Privilege | Authorization | Admin access bypass | Least privilege, RBAC validation |

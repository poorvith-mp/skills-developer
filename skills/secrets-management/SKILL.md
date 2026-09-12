---
name: secrets-management
last_reviewed: 2026-09-06
group: Security
description: >-
  Handle keys properly: vaults, rotation, `.env` hygiene, pre-commit scanning, and purging a key
  already in git history. Use when managing environment secrets, Vault, KMS, or key rotation.
---

# secrets-management

## Core Philosophy
Hardcoding API keys, database passwords, or private encryption keys into source code or unencrypted configuration files is an existential security threat. Secrets must never be stored in plaintext, never committed to version control, and never shared over insecure channels. Modern secrets management requires centralized key vaults (HashiCorp Vault, AWS Secrets Manager), automated rotation, strict local `.env` hygiene, pre-commit entropy scanning, and rapid eradication procedures when a secret is accidentally exposed.

---

## 4-Step Secrets Management Architecture

### Step 1: Centralized Vault & Runtime Injection
1. **Dynamic Secret Generation & Key Vaults**:
   - Store production secrets in a dedicated vault (AWS Secrets Manager, GCP Secret Manager, HashiCorp Vault, or 1Password Developer).
   - Authenticate services using cloud IAM roles (AWS IRSA, GCP Workload Identity) rather than static credentials.
2. **Runtime Environment Injection**:
   - Inject secrets into container runtimes at launch as environment variables or ephemeral in-memory volume mounts.
   - Never write production secrets to configuration files committed to git.

### Step 2: Local Developer Hygiene & `.env` Standards
1. **The Three-File `.env` Protocol**:
   - `.env.example`: Committed to Git. Contains all required variable keys with empty or fake mock values (documentation for developers).
   - `.env.local`: Ignored by Git. Contains developer's personal local credentials.
   - `.gitignore`: Must explicitly include:
     ```gitignore
     .env
     .env.*
     !.env.example
     *.pem
     *.key
     id_rsa
     ```

### Step 3: Shift-Left Secret Scanning (Pre-Commit & CI Gates)
1. **Local Pre-Commit Entropy Scanning**:
   - Configure tools like `gitleaks` or `trufflehog` in local git hooks:
     ```bash
     gitleaks protect --verbose --staged
     ```
2. **CI/CD Scanning & Branch Gating**:
   - Run automated secret scans on every pull request. If a secret pattern (e.g. `sk-proj-...`, `ghp_...`, `AKIA...`) is detected, fail the build immediately and block merging.

### Step 4: Incident Response & Secret Eradication
1. **The Tainted Secret Rule**:
   - Once a secret is committed to Git (even for 30 seconds on a private branch), **it must be considered compromised**.
   - Immediate Remediation Steps:
     - 1. **Revoke & Rotate**: Revoke the credential in the source provider immediately and issue a new one.
     - 2. **Audit Access Logs**: Check cloud provider access logs for unauthorized usage during the exposure window.
     - 3. **Purge Git History**: Use `git-filter-repo` (never basic git commit amending) to rewrite repository history:
       ```bash
       git filter-repo --invert-paths --path-match .env
       ```

---

## Deliverable Format: Secrets Management Specification (`SECRETS-SPEC.md`)

```markdown
# Secrets Management Architecture: [System / Application]

## 1. Centralized Vault & Key Topology
- **Vault Provider**: AWS Secrets Manager / HashiCorp Vault
- **Authentication**: IAM Role-based Workload Identity (Zero static root keys)
- **Rotation Cadence**: Automated 30-day rotation for database passwords

## 2. Secrets Registry & Environment Mapping
| Secret Key Name | Storage Vault Path | Scope | Rotation Method |
|---|---|---|---|
| `DATABASE_URL` | `prod/api/db_conn` | Backend Service | Automated RDS Master Rotation |
| `STRIPE_SECRET_KEY` | `prod/api/stripe` | Billing Worker | Manual Bi-annual Rotation |
| `JWT_PRIVATE_KEY` | `prod/auth/jwt_rsa` | Auth Service | KMS Asymmetric Key Pair |

## 3. Pre-Commit Secret Scanner Configuration (`.gitleaks.toml`)
```toml
[allowlist]
description = "Allowed mock keys in test suites"
paths = [
  '''tests/fixtures/.*'''
]
```

## 4. Emergency Rotation Runbook
1. Access AWS Secrets Manager console -> Select secret -> Click "Rotate Secret Immediately".
2. Deploy rolling restart of ECS services to pick up new credential.
3. Verify application health check returns 200 OK.
```

---

## Worked Example: Automated Git Secret Eradication

- **Incident**: A junior developer committed an AWS IAM Access Key to a feature branch.
- **Response**:
  1. Revoked key in AWS IAM within 4 minutes.
  2. Executed `git-filter-repo` to permanently erase the commit from all branches and tags.
  3. Force-pushed updated reflog to remote; notified all developers to prune local clones.
  4. Installed `gitleaks` pre-commit hook across all team repositories.
- **Outcome**: Zero unauthorized AWS access detected in CloudTrail; recurrence eliminated.

---

## Verification Checklist

- [ ] `.gitignore` explicitly blocks `.env`, `.env.*`, and private key files.
- [ ] `.env.example` provides an up-to-date manifest of all required keys with dummy values.
- [ ] Pre-commit hook runs `gitleaks` or `trufflehog` on staged changes.
- [ ] Production secrets are fetched at runtime via IAM-authenticated vaults.
- [ ] Documented rotation runbook exists for all third-party API credentials.

---

## Anti-Patterns

- **The "Private Repo" Fallacy**: Assuming hardcoded keys are safe because the GitHub repository is currently private.
- **Committing and Amending**: Making a new commit that deletes the secret without purging the commit history where the key remains readable.
- **Slack/Email Secret Sharing**: Pasting production passwords into Slack DMs or email threads.

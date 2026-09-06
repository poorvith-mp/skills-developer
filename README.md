# skills-developer

Developer skills collection for Claude Code, Cursor, Codex, Gemini CLI, and `npx skills` — part of [Skillary](https://github.com/poorvith-mp/skillary) by [Poorvith M P](https://github.com/poorvith-mp).

- **Version**: `v3.0.0`
- **Total Skills**: `58`
- **License**: MIT
- **Hub Repository**: [poorvith-mp/skillary](https://github.com/poorvith-mp/skillary)

## Install

Install the entire collection via `npx skills`:
```bash
npx skills add poorvith-mp/skills-developer
```

Or install individual skills directly:
```bash
npx skills add poorvith-mp/skills-developer --skill <skill-id>
```

## Skills in this Collection

### Understand and design

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `api-design` | [API Design](skills/api-design/SKILL.md) | Design and document REST, GraphQL and gRPC contracts with OpenAPI, versioning and contract tests. |
| `codebase-map` | [Codebase Map](skills/codebase-map/SKILL.md) | Map an unfamiliar codebase: entry points, data flow, key abstractions and where the first change goes safely. |
| `database` | [Database](skills/database/SKILL.md) | Design schemas with the right relationships, indexes and normalisation, then fix the queries that turn out slow. |
| `stack-choice` | [Stack Choice](skills/stack-choice/SKILL.md) | Evaluate technology options against requirements, team skill, scale and total cost, and record why. |
| `system-design` | [System Design](skills/system-design/SKILL.md) | Design the whole system: service boundaries, domain model, patterns, and the decision record behind each choice. |

### Plan

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `implementation-plan` | [Implementation Plan](skills/implementation-plan/SKILL.md) | Break the change into ordered, reviewable steps with checkpoints, so a long task can be stopped and resumed. |
| `solution-exploration` | [Solution Exploration](skills/solution-exploration/SKILL.md) | Diverge before committing: generate genuinely different approaches, name the trade-off each makes, and kill what doesn't survive. |
| `spec-writing` | [Spec Writing](skills/spec-writing/SKILL.md) | Turn a vague request into a written spec: scope, non-goals, acceptance criteria and the edge cases that will bite. |

### Build

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `backend-build` | [Backend Build](skills/backend-build/SKILL.md) | Implement services and business logic: request handling, validation, transaction boundaries, caching, queues and background workers. |
| `frontend-build` | [Frontend Build](skills/frontend-build/SKILL.md) | Implement web UIs in React, Vue or Angular with attention to performance, state and correctness. |
| `minimal-diff` | [Minimal Diff](skills/minimal-diff/SKILL.md) | Make the smallest correct change that fixes the problem, resisting every incidental refactor. |
| `mobile-build` | [Mobile Build](skills/mobile-build/SKILL.md) | Build mobile apps native or cross-platform, with real depth in Swift/SwiftUI and Kotlin/Compose. |
| `port-code` | [Port Code](skills/port-code/SKILL.md) | Translate code between languages, or migrate JavaScript to TypeScript, preserving behaviour and coverage. |
| `prototype` | [Prototype](skills/prototype/SKILL.md) | Build something working fast, choosing throwaway shortcuts deliberately and marking what must be rebuilt. |
| `realtime-systems` | [Realtime Systems](skills/realtime-systems/SKILL.md) | Build WebSocket, SSE and pub/sub features: presence, fan-out, reconnection and backpressure. |
| `refactor` | [Refactor](skills/refactor/SKILL.md) | Find structural smells and apply named refactorings without changing behaviour. |

### Data and AI

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `data-pipelines` | [Data Pipelines](skills/data-pipelines/SKILL.md) | Build ETL/ELT and streaming pipelines with quality validation, schema evolution and anomaly correction. |
| `llm-evals` | [Llm Evals](skills/llm-evals/SKILL.md) | Build evaluation harnesses: regression sets, scoring rubrics, drift detection and benchmarks. |
| `ml-deployment` | [Ml Deployment](skills/ml-deployment/SKILL.md) | Train, serve, evaluate and integrate models into production systems. |
| `model-audit` | [Model Audit](skills/model-audit/SKILL.md) | Independently review a model end to end: documentation, data reconstruction, replication and challenge. |
| `speech-pipelines` | [Speech Pipelines](skills/speech-pipelines/SKILL.md) | Build voice pipelines from audio ingestion through Whisper-style or cloud ASR to structured output. |

### Quality

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `code-review` | [Code Review](skills/code-review/SKILL.md) | Review a change for correctness, performance, security, readability, coverage and architectural fit. |
| `debugging` | [Debugging](skills/debugging/SKILL.md) | Turn a trace into a plain explanation, then isolate the cause by binary search and hypothesis testing. |
| `load-testing` | [Load Testing](skills/load-testing/SKILL.md) | Design and run load tests with realistic traffic patterns against a stated baseline. |
| `performance-audit` | [Performance Audit](skills/performance-audit/SKILL.md) | Profile and fix slowness across Core Web Vitals, backend queries and infrastructure. |
| `test-suite` | [Test Suite](skills/test-suite/SKILL.md) | Write tests for happy paths, edge cases and failure modes, and produce the run output as proof. |

### Security

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `audit-readiness` | [Audit Readiness](skills/audit-readiness/SKILL.md) | Prepare for SOC 2, ISO 27001, HIPAA or PCI-DSS: control mapping, gap analysis and evidence. |
| `authentication` | [Authentication](skills/authentication/SKILL.md) | Implement OAuth 2.0, OIDC, sessions, token lifetimes, MFA and password storage without rolling your own crypto. |
| `cloud-security` | [Cloud Security](skills/cloud-security/SKILL.md) | Design identity boundaries, network segmentation, key management and workload isolation. |
| `dependency-audit` | [Dependency Audit](skills/dependency-audit/SKILL.md) | Check dependencies for CVEs, license conflicts and breaking-change risk before upgrading. |
| `pen-test` | [Pen Test](skills/pen-test/SKILL.md) | Run authorised penetration tests and red team exercises against apps, networks and cloud. |
| `secrets-management` | [Secrets Management](skills/secrets-management/SKILL.md) | Handle keys properly: vaults, rotation, `.env` hygiene, pre-commit scanning, and purging a key already in git history. |
| `security-review` | [Security Review](skills/security-review/SKILL.md) | Threat model with STRIDE and audit code against the OWASP Top 10 before it ships. |
| `threat-detection` | [Threat Detection](skills/threat-detection/SKILL.md) | Write detection rules, correlate SIEM telemetry and map behaviour to MITRE ATT&CK. |

### Ship and run

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `ci-pipelines` | [CI Pipelines](skills/ci-pipelines/SKILL.md) | Build CI/CD with build, test, security scan and deploy stages across common providers. |
| `cloud-cost` | [Cloud Cost](skills/cloud-cost/SKILL.md) | Cut cloud spend with unit economics, rightsizing, showback and commitment planning. |
| `deployment` | [Deployment](skills/deployment/SKILL.md) | Ship it: platform config for Vercel, Netlify, Fly, Railway, Cloudflare or AWS, env and secrets, the pre/post checklist, and rollback. |
| `developer-platform` | [Developer Platform](skills/developer-platform/SKILL.md) | Build golden paths and self-service provisioning so teams stop rebuilding the same scaffolding. |
| `incident-response` | [Incident Response](skills/incident-response/SKILL.md) | Run a live incident: severity call, triage, stakeholder comms, mitigation and the writeup. |
| `infrastructure` | [Infrastructure](skills/infrastructure/SKILL.md) | Write Terraform, Pulumi or CloudFormation and automate provisioning, state and drift detection. |
| `job-scheduling` | [Job Scheduling](skills/job-scheduling/SKILL.md) | Design scheduled jobs with timezone handling, overlap prevention, alerting and dependency order. |
| `reliability` | [Reliability](skills/reliability/SKILL.md) | Set SLOs and error budgets, instrument with OpenTelemetry, and build the dashboards that prove them. |

### Migrate and modernise

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `migration` | [Migration](skills/migration/SKILL.md) | Map the debt, plan a strangler migration, and execute the zero-downtime cutover. |
| `monorepo` | [Monorepo](skills/monorepo/SKILL.md) | Structure a monorepo with build caching, affected-module detection and workspace boundaries. |

### Repo hygiene

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `branching-strategy` | [Branching Strategy](skills/branching-strategy/SKILL.md) | Design the branching and release model: trunk-based or GitFlow, protection rules, review policy, tracker traceability. |
| `change-notes` | [Change Notes](skills/change-notes/SKILL.md) | Write commit messages, PR descriptions and changelog entries from the diff itself. |
| `git-operations` | [Git Operations](skills/git-operations/SKILL.md) | Do the actual git work: branch, stage, commit, rebase, resolve conflicts, and recover with reflog and reset. |
| `github-workflow` | [Github Workflow](skills/github-workflow/SKILL.md) | Open and land PRs, respond to review comments, manage issues, labels, tags and releases through the `gh` CLI. |
| `repo-docs` | [Repo Docs](skills/repo-docs/SKILL.md) | Write the README, setup guide and comments that explain intent rather than restate the code. |

### Domain-specific

| Skill ID | Title | Description |
|:---------|:------|:------------|
| `accessibility-fix` | [Accessibility Fix](skills/accessibility-fix/SKILL.md) | Audit and refactor code for WCAG 2.1/2.2 AA and AAA: ARIA, keyboard operability, screen readers. |
| `commerce-platform` | [Commerce Platform](skills/commerce-platform/SKILL.md) | Architect CMS commerce: cart pipeline, checkout, payment gateways and PCI boundaries. |
| `error-handling` | [Error Handling](skills/error-handling/SKILL.md) | Design boundaries, fallbacks, retries, circuit breakers and graceful degradation paths. |
| `firmware` | [Firmware](skills/firmware/SKILL.md) | Write bare-metal and RTOS firmware for ESP32, ARM Cortex-M, STM32 and Nordic nRF. |
| `regex` | [Regex](skills/regex/SKILL.md) | Build and explain regular expressions with a breakdown of what each part matches and misses. |
| `salesforce` | [Salesforce](skills/salesforce/SKILL.md) | Architect Salesforce: multi-cloud design, integration patterns, governor limits and deployment. |
| `smart-contract-audit` | [Smart Contract Audit](skills/smart-contract-audit/SKILL.md) | Audit contracts for reentrancy, access control flaws and oracle manipulation. |
| `smart-contracts` | [Smart Contracts](skills/smart-contracts/SKILL.md) | Write Solidity for EVM: contract architecture, gas optimisation, upgradeable proxies and DeFi patterns. |
| `webhooks` | [Webhooks](skills/webhooks/SKILL.md) | Build webhook receivers with signature verification, idempotency, retries and dead letter queues. |

## License

MIT © [Poorvith M P](https://github.com/poorvith-mp)

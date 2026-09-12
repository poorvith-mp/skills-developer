# skills-developer

Developer skills collection for Claude Code, Cursor, Codex, Gemini CLI, and `npx skills` — part of [Skillary](https://github.com/poorvith-mp/skillary) by [Poorvith M P](https://github.com/poorvith-mp).

- **Version**: `v4.0.0`
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

### Domain-specific

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `accessibility-fix` | [Accessibility Fix](skills/accessibility-fix/SKILL.md) | Audit and refactor code for WCAG 2.1/2.2 AA and AAA: ARIA, keyboard operability, screen readers. Use when auditing or remediating WCAG 2.1/2.2 AA/AAA accessibility issues. | 2026-09-06 |
| `commerce-platform` | [Commerce Platform](skills/commerce-platform/SKILL.md) | Architect CMS commerce: cart pipeline, checkout, payment gateways and PCI boundaries. Use when developing Shopify apps, Liquid themes, or Headless commerce. | 2026-09-06 |
| `error-handling` | [Error Handling](skills/error-handling/SKILL.md) | Design boundaries, fallbacks, retries, circuit breakers and graceful degradation paths. Use when designing error boundaries, custom exceptions, or retry policies. | 2026-09-06 |
| `firmware` | [Firmware](skills/firmware/SKILL.md) | Write bare-metal and RTOS firmware for ESP32, ARM Cortex-M, STM32 and Nordic nRF. Use when writing embedded C/C++, RTOS, microcontroller, or IoT code. | 2026-09-06 |
| `regex` | [Regex](skills/regex/SKILL.md) | Build and explain regular expressions with a breakdown of what each part matches and misses. Use when creating, debugging, or optimizing regular expressions. | 2026-09-06 |
| `salesforce` | [Salesforce](skills/salesforce/SKILL.md) | Architect Salesforce: multi-cloud design, integration patterns, governor limits and deployment. Use when developing Apex, Lightning Web Components, or Salesforce flows. | 2026-09-06 |
| `smart-contract-audit` | [Smart Contract Audit](skills/smart-contract-audit/SKILL.md) | Audit contracts for reentrancy, access control flaws and oracle manipulation. Use when auditing smart contracts for reentrancy, gas, or exploit risks. | 2026-09-06 |
| `smart-contracts` | [Smart Contracts](skills/smart-contracts/SKILL.md) | Write Solidity for EVM: contract architecture, gas optimisation, upgradeable proxies and DeFi patterns. Use when developing Solidity or EVM smart contracts and token standards. | 2026-09-06 |
| `webhooks` | [Webhooks](skills/webhooks/SKILL.md) | Build webhook receivers with signature verification, idempotency, retries and dead letter queues. Use when implementing, verifying, or signing incoming/outgoing webhooks. | 2026-09-06 |

### Understand and design

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `api-design` | [API Design](skills/api-design/SKILL.md) | Design and document REST, GraphQL and gRPC contracts with OpenAPI, versioning and contract tests. Use when creating OpenAPI schemas, REST, GraphQL, or gRPC contracts. | 2026-09-06 |
| `codebase-map` | [Codebase Map](skills/codebase-map/SKILL.md) | Map an unfamiliar codebase: entry points, data flow, key abstractions and where the first change goes safely. Use when onboarding to an unfamiliar codebase or mapping architecture. | 2026-09-06 |
| `database` | [Database](skills/database/SKILL.md) | Design schemas with the right relationships, indexes and normalisation, then fix the queries that turn out slow. Use when designing schemas, indexing strategies, or optimizing slow queries. | 2026-09-06 |
| `stack-choice` | [Stack Choice](skills/stack-choice/SKILL.md) | Evaluate technology options against requirements, team skill, scale and total cost, and record why. Use when evaluating technologies, frameworks, or database trade-offs. | 2026-09-06 |
| `system-design` | [System Design](skills/system-design/SKILL.md) | Design the whole system: service boundaries, domain model, patterns, and the decision record behind each choice. Use when designing system architecture, domain models, or service boundaries. | 2026-09-06 |

### Security

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `audit-readiness` | [Audit Readiness](skills/audit-readiness/SKILL.md) | Prepare for SOC 2, ISO 27001, HIPAA or PCI-DSS: control mapping, gap analysis and evidence. Use when preparing evidence and technical controls for SOC 2 or ISO 27001. | 2026-09-06 |
| `authentication` | [Authentication](skills/authentication/SKILL.md) | Implement OAuth 2.0, OIDC, sessions, token lifetimes, MFA and password storage without rolling your own crypto. Use when implementing auth flows, OAuth, JWT, MFA, or sessions. | 2026-09-06 |
| `cloud-security` | [Cloud Security](skills/cloud-security/SKILL.md) | Design identity boundaries, network segmentation, key management and workload isolation. Use when configuring cloud security, IAM least-privilege, or VPC perimeters. | 2026-09-06 |
| `dependency-audit` | [Dependency Audit](skills/dependency-audit/SKILL.md) | Check dependencies for CVEs, license conflicts and breaking-change risk before upgrading. Use when scanning dependencies for CVEs, license conflicts, or supply-chain risks. | 2026-09-06 |
| `pen-test` | [Pen Test](skills/pen-test/SKILL.md) | Run authorised penetration tests and red team exercises against apps, networks and cloud. Use when planning or executing penetration tests and vulnerability validation. | 2026-09-06 |
| `secrets-management` | [Secrets Management](skills/secrets-management/SKILL.md) | Handle keys properly: vaults, rotation, `.env` hygiene, pre-commit scanning, and purging a key already in git history. Use when managing environment secrets, Vault, KMS, or key rotation. | 2026-09-06 |
| `security-review` | [Security Review](skills/security-review/SKILL.md) | Threat model with STRIDE and audit code against the OWASP Top 10 before it ships. Use when reviewing application code and endpoints for vulnerabilities. | 2026-09-06 |
| `threat-detection` | [Threat Detection](skills/threat-detection/SKILL.md) | Write detection rules, correlate SIEM telemetry and map behaviour to MITRE ATT&CK. Use when building security monitoring, SIEM rules, or anomaly detection. | 2026-09-06 |

### Build

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `backend-build` | [Backend Build](skills/backend-build/SKILL.md) | Implement services and business logic: request handling, validation, transactions, caching, queues and workers. Use when implementing backend services or APIs. | 2026-09-06 |
| `frontend-build` | [Frontend Build](skills/frontend-build/SKILL.md) | Implement web UIs in React, Vue or Angular with attention to performance, state and correctness. Use when implementing web user interfaces, client state, or components. | 2026-09-06 |
| `minimal-diff` | [Minimal Diff](skills/minimal-diff/SKILL.md) | Make the smallest correct change that fixes the problem, resisting every incidental refactor. Use when fixing bugs with the smallest surgical change, avoiding refactors. | 2026-09-06 |
| `mobile-build` | [Mobile Build](skills/mobile-build/SKILL.md) | Build mobile apps native or cross-platform, with real depth in Swift/SwiftUI and Kotlin/Compose. Use when developing mobile applications in Swift, SwiftUI, Kotlin, or React Native. | 2026-09-06 |
| `port-code` | [Port Code](skills/port-code/SKILL.md) | Translate code between languages, or migrate JavaScript to TypeScript, preserving behaviour and coverage. Use when translating code across languages or migrating to TypeScript. | 2026-09-06 |
| `prototype` | [Prototype](skills/prototype/SKILL.md) | Build something working fast, choosing throwaway shortcuts deliberately and marking what must be rebuilt. Use when rapidly building proof-of-concept prototypes or MVPs. | 2026-09-06 |
| `realtime-systems` | [Realtime Systems](skills/realtime-systems/SKILL.md) | Build WebSocket, SSE and pub/sub features: presence, fan-out, reconnection and backpressure. Use when building WebSockets, SSE, pub/sub, presence, or live feeds. | 2026-09-06 |
| `refactor` | [Refactor](skills/refactor/SKILL.md) | Find structural smells and apply named refactorings without changing behaviour. Use when restructuring code to improve cleanliness without changing behaviour. | 2026-09-06 |

### Repo hygiene

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `branching-strategy` | [Branching Strategy](skills/branching-strategy/SKILL.md) | Design the branching and release model: trunk-based or GitFlow, protection rules, review policy, tracker traceability. Use when establishing Git flow, trunk-based development, or merge policies. | 2026-09-06 |
| `change-notes` | [Change Notes](skills/change-notes/SKILL.md) | Write commit messages, PR descriptions and changelog entries from the diff itself. Use when generating CHANGELOGs, release notes, or semver summaries. | 2026-09-06 |
| `git-operations` | [Git Operations](skills/git-operations/SKILL.md) | Do the actual git work: branch, stage, commit, rebase, resolve conflicts, and recover with reflog and reset. Use when resolving merge conflicts, complex rebases, or git history repairs. | 2026-09-06 |
| `github-workflow` | [Github Workflow](skills/github-workflow/SKILL.md) | Open and land PRs, respond to review comments, manage issues, labels, tags and releases through the `gh` CLI. Use when automating GitHub issues, PR templates, labels, or project boards. | 2026-09-06 |
| `repo-docs` | [Repo Docs](skills/repo-docs/SKILL.md) | Write the README, setup guide and comments that explain intent rather than restate the code. Use when writing READMEs, architecture summaries, or CONTRIBUTING guides. | 2026-09-06 |

### Ship and run

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `ci-pipelines` | [CI Pipelines](skills/ci-pipelines/SKILL.md) | Build CI/CD with build, test, security scan and deploy stages across common providers. Use when setting up GitHub Actions, GitLab CI, or build pipelines. | 2026-09-06 |
| `cloud-cost` | [Cloud Cost](skills/cloud-cost/SKILL.md) | Cut cloud spend with unit economics, rightsizing, showback and commitment planning. Use when optimizing AWS/GCP bills, right-sizing, or FinOps practices. | 2026-09-06 |
| `deployment` | [Deployment](skills/deployment/SKILL.md) | Ship it: platform config for Vercel, Netlify, Fly, Railway, AWS, env secrets, checklists, and rollback. Use when deploying applications to cloud environments. | 2026-09-06 |
| `developer-platform` | [Developer Platform](skills/developer-platform/SKILL.md) | Build golden paths and self-service provisioning so teams stop rebuilding the same scaffolding. Use when building internal developer portals, CLI scaffolds, or dev tooling. | 2026-09-06 |
| `incident-response` | [Incident Response](skills/incident-response/SKILL.md) | Run a live incident: severity call, triage, stakeholder comms, mitigation and the writeup. Use when managing live production outages, triage, or post-mortems. | 2026-09-06 |
| `infrastructure` | [Infrastructure](skills/infrastructure/SKILL.md) | Write Terraform, Pulumi or CloudFormation and automate provisioning, state and drift detection. Use when writing Terraform, OpenTofu, Pulumi, or cloud IaC manifests. | 2026-09-06 |
| `job-scheduling` | [Job Scheduling](skills/job-scheduling/SKILL.md) | Design scheduled jobs with timezone handling, overlap prevention, alerting and dependency order. Use when configuring cron jobs, distributed schedulers, or Celery/Temporal. | 2026-09-06 |
| `reliability` | [Reliability](skills/reliability/SKILL.md) | Set SLOs and error budgets, instrument with OpenTelemetry, and build the dashboards that prove them. Use when designing SLIs/SLOs, circuit breakers, or disaster recovery. | 2026-09-06 |

### Quality

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `code-review` | [Code Review](skills/code-review/SKILL.md) | Review a change for correctness, performance, security, readability, coverage and architectural fit. Use when reviewing pull requests, diffs, or commits before merging. | 2026-09-06 |
| `debugging` | [Debugging](skills/debugging/SKILL.md) | Turn a trace into a plain explanation, then isolate the cause by binary search and hypothesis testing. Use when diagnosing bugs, stack traces, race conditions, or failures. | 2026-09-06 |
| `load-testing` | [Load Testing](skills/load-testing/SKILL.md) | Design and run load tests with realistic traffic patterns against a stated baseline. Use when stress-testing systems with k6, Locust, or concurrency benchmarks. | 2026-09-06 |
| `performance-audit` | [Performance Audit](skills/performance-audit/SKILL.md) | Profile and fix slowness across Core Web Vitals, backend queries and infrastructure. Use when auditing application performance, Core Web Vitals, or latency bottlenecks. | 2026-09-06 |
| `test-suite` | [Test Suite](skills/test-suite/SKILL.md) | Write tests for happy paths, edge cases and failure modes, and produce the run output as proof. Use when writing unit, integration, or regression test suites. | 2026-09-06 |

### Data and AI

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `data-pipelines` | [Data Pipelines](skills/data-pipelines/SKILL.md) | Build ETL/ELT and streaming pipelines with quality validation, schema evolution and anomaly correction. Use when building ETL/ELT pipelines, streaming data, or schema validation. | 2026-09-06 |
| `llm-evals` | [Llm Evals](skills/llm-evals/SKILL.md) | Build evaluation harnesses: regression sets, scoring rubrics, drift detection and benchmarks. Use when building LLM evaluation harnesses, scoring rubrics, or drift benchmarks. | 2026-09-06 |
| `ml-deployment` | [Ml Deployment](skills/ml-deployment/SKILL.md) | Train, serve, evaluate and integrate models into production systems. Use when deploying, serving, or monitoring machine learning models in production. | 2026-09-06 |
| `model-audit` | [Model Audit](skills/model-audit/SKILL.md) | Independently review a model end to end: data reconstruction, replication and challenge. For legal compliance, see ai-governance. Use when auditing ML models, bias, or data integrity. | 2026-09-06 |
| `speech-pipelines` | [Speech Pipelines](skills/speech-pipelines/SKILL.md) | Build voice pipelines from audio ingestion through Whisper-style or cloud ASR to structured output. Use when building voice, ASR, Whisper, or audio processing pipelines. | 2026-09-06 |

### Plan

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `implementation-plan` | [Implementation Plan](skills/implementation-plan/SKILL.md) | Break the change into ordered, reviewable steps with checkpoints, so a long task can be stopped and resumed. Use when breaking changes into ordered, testable steps with checkpoints. | 2026-09-06 |
| `solution-exploration` | [Solution Exploration](skills/solution-exploration/SKILL.md) | Diverge before committing: generate genuinely different approaches, name trade-offs, and kill what doesn't survive. Use when exploring architectural trade-offs. | 2026-09-06 |
| `spec-writing` | [Spec Writing](skills/spec-writing/SKILL.md) | Turn a vague request into a written spec: scope, non-goals, acceptance criteria and the edge cases that will bite. Use when writing technical specifications, scope, and acceptance criteria. | 2026-09-06 |

### Migrate and modernise

| Skill ID | Title | Description | Reviewed |
|:---------|:------|:------------|:---------|
| `migration` | [Migration](skills/migration/SKILL.md) | Map the debt, plan a strangler migration, and execute the zero-downtime cutover. Use when migrating legacy systems, databases, or frameworks safely. | 2026-09-06 |
| `monorepo` | [Monorepo](skills/monorepo/SKILL.md) | Structure a monorepo with build caching, affected-module detection and workspace boundaries. Use when configuring Turborepo, Nx, package boundaries, or monorepo tooling. | 2026-09-06 |

## License

MIT © [Poorvith M P](https://github.com/poorvith-mp)

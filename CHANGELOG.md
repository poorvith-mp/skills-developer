# Changelog

## v3.0.0 — September 2026

Major integrity, security, and portability release across Skillary:
- **Markdown Integrity**: Cleaned escaped markdown artifacts and normalized table formatting across all `SKILL.md` files.
- **Portability**: Standardized relative references; eliminated vendor lock-in paths for universal execution across Claude Code, Cursor, Codex, and Gemini CLI.
- **Verified Boundaries**: Synced manifests, references, and taxonomy checklists to strict 3.0.0 specification standards.
- **Curated Catalog**: Pruned non-target skills and synchronized skill indexes directly with hub distribution.

## v0.2 — July 2026

- Added `ci-cd-pipeline-builder` skill — GitHub Actions / GitLab CI / CircleCI pipeline config generation
- Added `iac-provisioner` skill — Dockerfiles, docker-compose, Terraform, and Kubernetes manifests
- Added `android-developer` skill — native Android/Kotlin/Jetpack Compose development
- Added `ios-developer` skill — native iOS/Swift/SwiftUI development
- Added `graphql-api-designer` skill — GraphQL schema, resolver, and query/mutation design
- Added `load-testing-engineer` skill — load/stress test planning with k6, Locust, JMeter
- Added `dependency-upgrade-auditor` skill — dependency manifest review and safe upgrade sequencing
- Skill count synced to **88** in README

## v0.1 — July 2026

- Initial public import of `skills-developer` by Poorvith M P
- 81 skills rewritten to skill-creator layout (`SKILL.md` + empty `references/` + `assets/`)
- Duplicates collapsed; pack index pages excluded; third-party credits stripped
- MIT License

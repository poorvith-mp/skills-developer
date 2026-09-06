---
name: branching-strategy
group: Repo hygiene
description: >-
  Design the branching and release model: trunk-based or GitFlow, protection rules, review policy,
  tracker traceability. Use when establishing Git flow, trunk-based development, or merge
  policies.
---
# Branching Strategy

Design a branching and release process that matches how the team actually ships.

## Process
1. **Start from release cadence.** Continuous deployment and quarterly releases need different models; picking GitFlow for a team that deploys hourly creates permanent merge pain.
2. **Default to trunk-based with short-lived branches** unless there is a concrete reason not to — long-lived branches are where merge conflicts and stale reviews come from.
3. **Set branch protection to match the real review capacity.** A two-approver rule on a three-person team blocks work rather than improving it.
4. **Make the release state unambiguous.** Tags, not branch names, should answer "what is in production".
5. **Define the hotfix path explicitly** before it is needed at 2am.
6. **Automate what the convention requires** — commit message format, branch naming, changelog — or it will be followed inconsistently.

## Deliverables
- Branching model with rationale tied to release cadence
- Protection rules and required checks
- Release and tagging convention
- Hotfix runbook

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

## Anti-Patterns & Constraints

- NEVER weaken or skip a failing test to make a change land.
- NEVER swallow errors silently or leave unhandled rejections in production paths.
- NEVER introduce a breaking API change without a version bump and migration path.

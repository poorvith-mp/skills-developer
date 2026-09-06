---
name: cloud-security
group: Security
description: >-
  Design identity boundaries, network segmentation, key management and workload isolation. Use
  when configuring cloud security, IAM least-privilege, or VPC perimeters.
---
# Cloud Security

Design cloud security around blast radius, not around a control checklist.

## Process
1. **Establish identity boundaries first.** Who and what can assume which roles, and across which accounts. Over-broad trust policies undo every other control.
2. **Apply least privilege to workloads, not just people.** Machine identities usually hold the widest permissions and get the least review.
3. **Segment so that one compromise is contained.** Separate accounts or projects per environment and per sensitivity tier beat network rules inside one flat account.
4. **Get key management right**: managed KMS, rotation, and no long-lived static credentials anywhere a short-lived one will do.
5. **Make the data perimeter explicit.** Which storage can be reached from the internet, and prove it rather than assume it.
6. **Log centrally to an account the workload cannot write to**, or an attacker deletes their own trail.
7. **Detect drift.** Configuration that was correct at deploy will not stay correct.

## Deliverables
- Identity and trust boundary map across accounts
- Segmentation model with justification per boundary
- Key management and credential lifecycle plan
- Logging architecture with tamper resistance

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

## Anti-Patterns & Constraints

- NEVER weaken or skip a failing test to make a change land.
- NEVER swallow errors silently or leave unhandled rejections in production paths.
- NEVER introduce a breaking API change without a version bump and migration path.

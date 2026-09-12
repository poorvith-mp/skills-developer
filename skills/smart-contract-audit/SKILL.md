---
name: smart-contract-audit
last_reviewed: 2026-09-06
group: Domain-specific
description: >-
  Audit contracts for reentrancy, access control flaws and oracle manipulation. Use when auditing
  smart contracts for reentrancy, gas, or exploit risks.
---

# Smart Contract Audit

Audit smart contracts for the failure modes that actually drain funds.

## Process
1. **Map value flow and trust boundaries first.** Where does value enter, leave, and who can move it? Most exploits live at a boundary the developer did not think of as one.
2. **Check access control on every state-changing function.** Missing or wrong modifiers remain the most common serious finding.
3. **Trace reentrancy paths**, including cross-function and cross-contract. Verify checks-effects-interactions ordering rather than trusting a guard.
4. **Examine every external call**: return values checked, gas assumptions, and what happens if the callee is malicious or reverts.
5. **Scrutinise price and oracle dependencies.** Spot prices from an AMM are manipulable within a transaction; require time-weighting or multiple sources.
6. **Review upgradeability**: storage layout compatibility, initialiser protection, and who holds the upgrade key.
7. **Model the economics, not just the code.** Flash-loan-funded manipulation is a design flaw, not a bug.

## Deliverables
- Findings by severity with a concrete exploit path per issue
- Proof-of-concept test for each critical and high finding
- Remediation with the fix and why it closes the path

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

## Anti-Patterns & Constraints

- NEVER weaken or skip a failing test to make a change land.
- NEVER swallow errors silently or leave unhandled rejections in production paths.
- NEVER introduce a breaking API change without a version bump and migration path.

---
name: prototype
group: Build
description: >-
  Build something working fast, choosing throwaway shortcuts deliberately and marking what must be
  rebuilt. Use when rapidly building proof-of-concept prototypes or MVPs.
---

# Prototype

Build the smallest thing that answers the question, and be explicit that it is disposable.

## Process
1. **State the question the prototype answers.** "Will users understand this flow?" and "will this scale?" need completely different prototypes.
2. **Pick the shortest path to that answer** — hardcode data, skip auth, use one file, fake the backend. Every shortcut is fine if it does not affect the question.
3. **Do not build what you are not testing.** Error handling, edge cases and configuration are not part of a prototype whose question is about desirability.
4. **Mark the shortcuts in the code** as you take them, naming what would need to be real.
5. **Set a time box** and stop at it. A prototype that becomes a project has stopped answering the question.
6. **Decide explicitly: keep, rewrite or discard.** Prototypes that drift into production without that decision are how the worst codebases start.

## Deliverables
- The question, written down before building
- Working prototype with shortcuts marked
- Answer to the question, and the keep/rewrite/discard call

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

## Anti-Patterns & Constraints

- NEVER weaken or skip a failing test to make a change land.
- NEVER swallow errors silently or leave unhandled rejections in production paths.
- NEVER introduce a breaking API change without a version bump and migration path.

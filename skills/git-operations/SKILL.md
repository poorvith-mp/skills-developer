---
name: git-operations
last_reviewed: 2026-09-06
group: Repo hygiene
description: >-
  Do the actual git work: branch, stage, commit, rebase, resolve conflicts, and recover with
  reflog and reset. Use when resolving merge conflicts, complex rebases, or git history repairs.
---

# git-operations

## Core Philosophy
Git is not a magical black box where you type random commands found on StackOverflow hoping your branch fixes itself. Git is a content-addressable, immutable directed acyclic graph (DAG) of snapshot objects. Mastering Git operations means understanding object pointers, commits, trees, and the reflog—enabling you to resolve any merge conflict cleanly, rewrite messy commit history safely, and recover from accidental deletions with zero panic.

---

## 4-Step Professional Git Operations Discipline

### Step 1: Atomic Branching & Clean Commit Craft
1. **The Principle of Atomic Commits**:
   - Each commit represents exactly one logical change that compiles cleanly and passes tests.
   - Use interactive staging (`git add -p`) to review and stage distinct chunks rather than running blind `git add .`.
2. **Conventional Commit Standard**:
   - Format: `<type>(<scope>): <short imperative summary>`
   - Types: `feat`, `fix`, `refactor`, `perf`, `test`, `docs`, `chore`.
   - Rule: Imperative present tense ("add user validation", not "added" or "adds").

### Step 2: Interactive Rebasing & History Rewriting
1. **Squashing & Cleaning Feature Branches**:
   - Never merge a branch with 14 "fix typo" or "WIP" commits into main.
   - Rebase interactively onto upstream main:
     ```bash
     git fetch origin main
     git rebase -i origin/main
     ```
   - Rebase Commands:
     - `pick`: Use commit as-is.
     - `reword`: Change commit message.
     - `squash` / `fixup`: Meld commit into previous commit (`fixup` discards commit message).
2. **The Golden Rule of Rebasing**:
   - Never rebase a public shared branch (e.g. `main` or `production`). Only rebase local feature branches.

### Step 3: Complex 3-Way Merge Conflict Resolution
1. **Enabling Modern Conflict Markers**:
   - Configure Git to show the common ancestor base in conflict diffs:
     ```bash
     git config --global merge.conflictstyle zdiff3
     ```
2. **Systematic Conflict Resolution Protocol**:
   - Identify the 3 states: `<<<<<<< HEAD` (your changes), `||||||| base` (original state before both branched), `>>>>>>> incoming` (their changes).
   - Verify code compiles and passes unit tests before staging:
     ```bash
     git add <resolved-file>
     git rebase --continue
     ```
   - Abort cleanly if lost: `git rebase --abort` or `git merge --abort`.

### Step 4: Emergency Recovery with Git Reflog & Reset
1. **Recovering Lost Commits**:
   - Git almost never deletes committed objects immediately. The reference log (`reflog`) records every movement of `HEAD`.
   - View history of HEAD movements:
     ```bash
     git reflog
     ```
   - Restore branch state to prior snapshot:
     ```bash
     git reset --hard HEAD@{2}
     ```
2. **Safely Undoing Mistakes**:
   - Undo last commit but keep changes staged: `git reset --soft HEAD~1`.
   - Undo last commit and unstage changes: `git reset HEAD~1`.

---

## Deliverable Format: Git Runbook & Conflict Log (`GIT-RUNBOOK.md`)

```markdown
# Git Incident Recovery & Rebase Runbook

## 1. Branch Health & Clean History Strategy
- **Target Branch**: `feature/auth-refactor` -> `main`
- **Rebase Base**: `origin/main` (latest commit `e4f1a09`)
- **Action Plan**: Interactive rebase squashing 8 WIP commits into 2 atomic commits.

## 2. Conflict Resolution Walkthrough
| File | Conflict Nature | Resolution Chosen | Verification |
|---|---|---|---|
| `src/auth.ts` | Overlapping imports | Combined both imports | `npm run build` passed |
| `prisma/schema.prisma` | Conflicting model fields | Kept both fields; reordered | `npx prisma validate` |

## 3. Disaster Recovery Plan (Reflog Snapshot)
- Pre-rebase HEAD: `HEAD@{1}: commit 7b2a9c1 "feat(auth): initial oauth scaffolding"`
- Emergency recovery command: `git reset --hard 7b2a9c1`
```

---

## Worked Example: Rescuing a Detached HEAD State

- **Problem**: Engineer accidentally checked out a commit hash directly, made 4 commits, and could not find them after switching back to `main`.
- **Diagnosis**: Ran `git reflog`, identified the lost commit hash `a81f3d2`.
- **Remediation**: Executed `git branch feature/recovered-work a81f3d2`.
- **Result**: All 4 commits restored to a proper named branch with zero code loss in 60 seconds.

---

## Verification Checklist

- [ ] Feature branch rebased cleanly on latest `origin/main` prior to PR review.
- [ ] Commits are squashed into atomic, logically distinct units with conventional commit messages.
- [ ] `merge.conflictstyle zdiff3` configured to inspect common ancestor during conflicts.
- [ ] All unit and integration tests pass cleanly after conflict resolution.
- [ ] Pre-rebase state noted from `reflog` before executing destructive operations.

---

## Anti-Patterns

- **Force-Pushing Shared Branches**: Running `git push --force` on `main`, destroying teammates' commits. (Always use `--force-with-lease`).
- **Committing Secrets**: Adding `.env` files or API credentials into git tracking.
- **Giant Merge Dumps**: Merging a 40-commit branch full of "wip", "fixed bug", "test" messages directly to main.

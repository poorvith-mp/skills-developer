---
name: setup-codex-precheck
description: >-
  Runs pre-flight checks before a Codex session: environment, dependencies, credentials and repo
  state. Use when preparing a repository for agent-driven work.
---

# Setup codex pre-check
You install (and verify) a codex "double-check" gate into the **current project only**: a
`PreToolUse` hook that pipes every proposed `Edit`/`Write`/`MultiEdit` to the `codex` CLI for
an independent review before it is written. codex returns `VERDICT: APPROVE` (edit proceeds)
or `VERDICT: BLOCK` (edit denied, concerns fed back to Claude). It **fails open** — if codex
is missing/logged-out/erroring, edits are allowed with a warning, never blocked.
Configure the hook cleanly in the project directory.
## What it configures (in the current project)
- Pre-tool hook script — pipes proposed edits to `codex exec` for independent verification.
- Hook configuration — registers the hook for edit tools without clobbering existing settings.
- Project guidelines — records pre-check expectations for coding agents.
At runtime, the hook records an append-only audit trail and hashes already-approved changes to avoid redundant reviews.
## Process
1. **Verify prerequisites**: confirm `python3` and `codex` CLI are available and authenticated.
2. **Configure project hook**: install the pre-check script into the project's hooks directory.
3. **If codex is logged out or not installed**, inform the user that the gate will fail open with a warning until `codex login` is executed.
4. **Smoke test**: verify live connectivity with:
```bash
printf 'Reply exactly: VERDICT: APPROVE' | codex exec --skip-git-repo-check -s read-only -
```
5. **Remind the user to reload the session environment** so newly registered hooks take effect.
## Critical Rules
1. **Current project only.** Scope configurations locally; never touch global user configurations without approval.
2. **Idempotent.** Do not clobber existing settings.
3. **Fail-open is intentional.** Never hard-block when the validator CLI is temporarily unavailable.
4. **Flag latency trade-offs.** Per-edit checks add latency; recommend batch or stop-hooks for large changesets.
## Final Note
Arguments specify the target project directory (defaulting to the current working directory).
---


## Output format
- Lead with the result the user asked for.
- Use clear headings and bullet lists where helpful.
- Call out assumptions and open questions at the end.
- Stay specific to the Setup Codex Precheck workflow; avoid generic filler.

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

## Anti-Patterns & Constraints

- NEVER weaken or skip a failing test to make a change land.
- NEVER swallow errors silently or leave unhandled rejections in production paths.
- NEVER introduce a breaking API change without a version bump and migration path.

---
name: new-client-system
description: >-
  Sets up the onboarding system for a new client engagement: intake, access, environments,
  communication cadence and deliverable tracking. Use when starting client work.
---

# New Client System
You are scaffolding a **fresh frontend + backend pair** for a new client, modeled on the Shiney automations template. The output is structural only: auth, dashboard shell, design system, integration clients, and an empty automations registry. Automations are intentionally **not** scaffolded here — they're added in a later step once the client's domain is understood.
The stack couples Next.js, React, Trigger.dev, Composio, Anthropic, NextAuth, Tailwind, and MongoDB.
## Workflow
### Step 1 — Gather context (ALWAYS first)
Before touching the filesystem, collect the client parameters:
1. **Client display name** (e.g. "Acme Co") — used in titles, sidebar, login copy
2. **Client email domain** (e.g. "acme.com") — used to restrict auth (only `*@acme.com` can sign in)
3. **Output directory** — absolute path where the two project folders will be created (default: current working directory)
Then derive:
- `CLIENT_SLUG` = lowercase, dashes (e.g. "Acme Co" → "acme")
- `EMAIL_FROM` = `noreply@<domain>` (confirm if user wants different)
- `COMPOSIO_USER_ID` = the operator email
- `BUSINESS_EMAIL` = `billing@<domain>`
- `MONGODB_DB` = the slug
If any derived value is non-obvious or could go either way, confirm with one follow-up question. Otherwise proceed.
### Step 2 — Run the scaffold script
Call the bash script with all collected values:
```bash
 \
  --out "<OUT_DIR>" \
  --client-name "<Display Name>" \
  --client-domain "<domain>" \
  --client-slug "<slug>" \
  --email-from "<email>" \
  --composio-user-id "<email>" \
  --business-email "<email>" \
  --mongodb-db "<dbname>"
```
This:
1. Copies `templates/frontend/` → `<OUT_DIR>/<slug>/`
2. Copies `templates/backend/` → `<OUT_DIR>/<slug>_backend/`
3. Substitutes all `{{PLACEHOLDER}}` tokens via `sed`
4. Warns if any unsubstituted placeholders remain
The script refuses to overwrite existing folders — fail loudly is correct.
### Step 3 — Verify
After scaffolding, run a quick check:
```bash
grep -rE '\{\{[A-Z_]+\}\}' <OUT_DIR>/<slug> <OUT_DIR>/<slug>_backend || echo "All placeholders substituted."
```
Also verify both projects' `package.json` parse cleanly with `node -e "JSON.parse(require('fs').readFileSync('<path>/package.json'))"`.
### Step 4 — Report and next steps
Tell the user, concisely:
- The two folder paths created
- Required env vars they need to fill in (`.env.local` for frontend, `.env` for backend) — point to the `.example` files
- The four bootstrap commands (don't run them — just list):
```plain text
  cd <slug>           && npm install
  cd <slug>_backend   && npm install
  cd <slug>_backend   && npm run connect   # Composio OAuth for Gmail + Drive
  cd <slug>           && npm run dev       # http://localhost:3000
```
- That **no automations are scaffolded yet**, and the next step (when ready) is to add one under `<slug>_backend/src/automations/<auto-slug>/` with a matching entry in `<slug>/src/config/automations.ts` and route under `<slug>/src/app/(dashboard)/dashboard/automations/<auto-slug>/`.
## Critical Rules
1. **Always gather context first** — never scaffold with guessed values.
2. **Do not invent placeholders** — only defined client parameters are substituted.
3. **Do not scaffold automations** — the template has an empty automations registry on purpose.
4. **Do not modify the templates** during scaffolding — substitution is the only change.
5. **Do not run `npm install` automatically** — list it as a next step.
6. **Refuse to overwrite** existing destination folders.
7. **Both projects share the same Trigger.dev project** — `TRIGGER_PROJECT_REF` and `TRIGGER_SECRET_KEY` must match between frontend `.env.local` and backend `.env`.
8. **Stack conventions** — Next.js, NextAuth, Tailwind.
9. **The Composio user ID** defaults to the operator running the scaffold.
10. **Schema mirroring** — when automations are eventually added, Zod schemas are duplicated between `<slug>/src/lib/automations/<auto>/schema.ts` and `<slug>_backend/src/automations/<auto>/schema.ts`. Both must stay in sync.
## Final Note
This skill is **standalone** — the `templates/` directory contains the full source for both projects with placeholders. It does not depend on the original `aisystem` or `aisystem_backend` folders existing. Use `$ARGUMENTS` (if provided) as a hint for the client name, but always confirm via `AskUserQuestion` before scaffolding.
---


## Output format
- Lead with the result the user asked for.
- Use clear headings and bullet lists where helpful.
- Call out assumptions and open questions at the end.
- Stay specific to the New Client System workflow; avoid generic filler.

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

## Anti-Patterns & Constraints

- NEVER weaken or skip a failing test to make a change land.
- NEVER swallow errors silently or leave unhandled rejections in production paths.
- NEVER introduce a breaking API change without a version bump and migration path.

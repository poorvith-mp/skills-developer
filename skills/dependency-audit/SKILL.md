---
name: dependency-audit
description: >-
  Check dependencies for CVEs, license conflicts and breaking-change risk before upgrading.
---
# Dependency Audit

Upgrading a dependency is a tradeoff between staying current (security patches, new features, avoiding end-of-life versions) and stability risk (breaking changes, transitive dependency conflicts). Your job is to make that tradeoff visible and sequence it safely, not to blindly recommend "upgrade everything to latest."

## Workflow

1. **Read the actual manifest and lockfile** if provided, rather than asking the user to list dependencies manually — versions, and ideally the lockfile's resolved transitive tree, tell you more than the user's summary would.
2. **Classify each outdated dependency by semver jump:**
   - **Patch** (x.x.PATCH) — near-zero risk, safe to batch-upgrade.
   - **Minor** (x.MINOR.x) — should be backward-compatible per semver convention, but check the changelog for any "deprecated" notices signaling a future breaking change.
   - **Major** (MAJOR.x.x) — assume breaking changes until the changelog says otherwise. Never batch major upgrades together; do them one at a time so a regression is traceable to a specific package.
3. **Flag security-relevant upgrades separately and with higher priority** — a known CVE in a current version should jump the queue regardless of how large the version jump is, and this should be called out explicitly rather than buried in a general list.
4. **Check for deprecated or end-of-life packages** — a package with no maintenance activity or an explicit deprecation notice is worth flagging even if the current version has no known vulnerability, since it's a growing risk over time.
5. **Sequence the upgrade plan**: patches and minors first (batch, low risk), then majors one at a time with a note on what to test after each, prioritized by security relevance.
6. **Watch for transitive conflicts** — upgrading one package can force a peer dependency into a version range that conflicts with another package's requirement. Flag this if visible in the lockfile/error output rather than assuming a clean upgrade.

## Anti-Patterns & Constraints

- Don't recommend upgrading to the absolute latest version of everything by default — "safe and current" isn't the same as "bleeding edge," and unnecessary churn has its own cost.
- Don't claim a major-version upgrade is safe without either reading its changelog/migration guide or explicitly flagging that you haven't verified it and the user should check before merging.
- Don't silently skip a package just because it looks hard to upgrade — flag it explicitly as deferred, with the reason, so it doesn't quietly become permanently stale.

## Output format

```markdown
## Dependency audit: <project>

**Security-relevant (upgrade first):**
| Package | Current | Target | CVE/reason |

**Safe batch (patch/minor):**
| Package | Current | Target |

**Major upgrades (one at a time, test after each):**
| Package | Current | Target | Known breaking changes |

**Deferred / flagged:**
| Package | Reason |
```

See `references/semver-risk-guide.md` for how to read changelogs for real (vs. nominal) breaking-change risk.

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

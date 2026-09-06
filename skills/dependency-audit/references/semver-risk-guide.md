# Reading changelogs for real breaking-change risk

Semver is a convention, not a guarantee — packages violate it, intentionally or by mistake. Treat the stated version bump as a starting signal, not the final word.

## Signals a "minor" bump is actually riskier than it looks
- Changelog mentions "deprecated" without removal yet — safe now, but signals a future major bump will remove it; worth updating call sites proactively.
- New required peer dependency, even if the package's own version only bumped minor.
- Changed default behavior of an existing option (not a new option, an existing default flipping) — this breaks code relying on the old default even though no signature changed.

## Signals a "major" bump might be lower-risk than assumed
- Changelog explicitly says the breaking change only affects a specific edge case or deprecated API path your usage doesn't touch.
- Package has a documented codemod/migration script (common in large frameworks) that automates the bulk of the change.

## General sequencing rule
Upgrade one major-version dependency at a time, run the test suite, and only move to the next once the current one is confirmed stable. Batch major upgrades make it much harder to trace a regression back to its source.

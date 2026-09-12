---
name: regex
last_reviewed: 2026-09-06
group: Domain-specific
description: >-
  Build and explain regular expressions with a breakdown of what each part matches and misses. Use
  when creating, debugging, or optimizing regular expressions.
---

# Regex

Regular expressions fail on edge cases and catastrophic backtracking (ReDoS). Always specify the dialect (PCRE, JS, Python `re`), anchor boundary intent, and test positive matches against false positives.
## Process
1. Understand the matching requirement and target regex dialect.
2. Build the pattern incrementally: character classes, anchors, quantifiers.
3. Test against sample inputs (both expected matches and near-misses).
4. Analyze quantifier safety to prevent catastrophic backtracking.
5. Provide usage examples with proper flags and escaping.
## Output Format
### Regex Pattern
```javascript
/your-pattern/flags
```
### Explanation
| Component | Meaning |
|---|---|
| `^` | Start of string |
| `[a-z]` | Lowercase letter |
| `+` | One or more times |
### Test Cases
**✅ Should match:**
- `example1` → match
- `example2` → match
**❌ Should NOT match:**
- `invalid1` → no match
- `invalid2` → no match
### Usage Examples
**JavaScript:**
```javascript

const regex = /pattern/flags;

const result = regex.test(string);

```
**Python:**
```python

import re

result = re.match(r'pattern', string)

```
## Instructions
When the user describes a pattern:
- Always provide the regex with appropriate flags
- Explain every component clearly
- Include both positive and negative test cases
- Provide code examples in the user's language of choice
- Warn about any performance considerations
- Offer a simpler alternative if the regex is complex
## Regex Explanation Format
Always break down the regex into labeled components:
```javascript
Pattern: ^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$

Breakdown:
^               → Start of string
[a-zA-Z0-9._%+-]+  → One or more valid email chars
@               → Literal @ sign
[a-zA-Z0-9.-]+  → Domain name
\.              → Literal dot (escaped)
[a-zA-Z]{2,}    → TLD: 2 or more letters
$               → End of string
```
Always provide 3-5 test cases showing what the regex matches and doesn't match.

## Critical rules
1. Prefer concrete, actionable steps over vague advice — the user needs executable output.
2. Ask for missing context only when it blocks a correct answer; otherwise state assumptions.
3. Do not invent personal identities, third-party credits, or external source claims.

## Verification & Quality Checklist

- [ ] Code compiles and all automated tests and typechecks pass without new warnings.
- [ ] Edge cases, boundary conditions, and error states handled explicitly rather than assumed.
- [ ] No hardcoded secrets, credentials, or insecure defaults introduced.
- [ ] Changes are covered by a test that fails without them.

## Anti-Patterns & Constraints

- NEVER weaken or skip a failing test to make a change land.
- NEVER swallow errors silently or leave unhandled rejections in production paths.
- NEVER introduce a breaking API change without a version bump and migration path.

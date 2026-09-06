---
name: accessibility-fix
description: >-
  Audit and refactor code for WCAG 2.1/2.2 AA and AAA: ARIA, keyboard operability, screen readers.
---
# Accessibility Fix

Audits, validates, and remediates accessibility issues across web applications according to WCAG 2.1/2.2 AA and AAA standards, Section 508, and ADA guidelines.

## Phased Workflow

### Phase 1: Discovery & Audit
1. Inspect DOM hierarchy, landmark elements (`<main>`, `<nav>`, `<header>`, `<footer>`), and heading order (`h1` through `h6`).
2. Verify color contrast ratios (minimum 4.5:1 for normal text, 3:1 for large text / UI controls under WCAG AA).
3. Test keyboard navigation: ensure all interactive elements receive visible `:focus-visible` rings and logical tab sequence without keyboard traps.
4. Check screen reader compatibility: audit `alt` attributes, `aria-label`, `aria-labelledby`, `aria-describedby`, and live regions (`aria-live`).

### Phase 2: Remediation & Code Modification
1. Replace non-semantic HTML (`<div onClick=...>`) with semantic elements (`<button>`, `<a>`, `<input>`).
2. Add necessary ARIA attributes only where semantic HTML is insufficient (Rule 1 of ARIA: Do not use ARIA when semantic HTML exists).
3. Ensure dynamic content changes announce properly via `aria-live="polite"` or `"assertive"`.
4. Fix modal focus trapping and restore focus to trigger button upon close.

### Phase 3: Validation & Reporting
1. Generate compliance report mapping issues to WCAG Success Criteria (e.g., 1.1.1 Non-text Content, 1.4.3 Contrast, 2.1.1 Keyboard).
2. Provide code diffs with before/after comparisons and remediation verification steps.

## Verification & Quality Checklist
- [ ] All interactive elements are focusable via `Tab` and operable via `Enter` / `Space`.
- [ ] No positive `tabindex` values (use `tabindex="0"` or `"-1"` only).
- [ ] Form inputs have associated `<label>` tags with matching `id`/`for` attributes.
- [ ] Color is not used as the sole conveyor of information (include icons or text indicators).
- [ ] Contrast ratios verified with a contrast calculator tool.

## Anti-Patterns & Constraints
- NEVER strip focus outlines (`outline: none` or `outline: 0`) without providing an equally visible custom focus state.
- NEVER use generic `aria-label="button"` or duplicate accessible names.
- NEVER rely solely on automated audits (automated tools catch only ~30-40% of accessibility issues; always test manual keyboard flow).

## References

Load these only when the task needs them:

- [references/wcag-checklist.md](references/wcag-checklist.md)

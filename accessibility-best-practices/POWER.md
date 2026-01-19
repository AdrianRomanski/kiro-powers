---
name: "accessibility-best-practices"
displayName: "Accessibility Expert"
description: "Expert guidance for building accessible web applications following WCAG standards"
keywords:
  - accessibility
  - a11y
  - wcag
  - aria
  - screen reader
  - keyboard navigation
  - semantic html
---

# Onboarding

When this power activates:

1. Assume the user wants to build or audit for WCAG 2.1 AA compliance (minimum standard).
2. Prioritize semantic HTML over ARIA when possible.
3. Always consider keyboard navigation, screen readers, and visual accessibility.
4. Provide actionable, testable recommendations.

# Core Guidance

Refer to the steering files in `steering/`:

- Semantic HTML: `steering/semantic-html.md`
- ARIA Patterns: `steering/aria-patterns.md`
- Keyboard Navigation: `steering/keyboard-navigation.md`
- Visual Accessibility: `steering/visual-accessibility.md`
- Testing: `steering/testing.md`
- Forms: `steering/forms.md`

# Quick Reference

## WCAG 2.1 Levels
- **A**: Minimum level (must have)
- **AA**: Mid-range level (should have) - most common legal requirement
- **AAA**: Highest level (nice to have)

## Four Principles (POUR)
1. **Perceivable**: Information must be presentable to users in ways they can perceive
2. **Operable**: UI components must be operable by all users
3. **Understandable**: Information and UI operation must be understandable
4. **Robust**: Content must be robust enough for assistive technologies

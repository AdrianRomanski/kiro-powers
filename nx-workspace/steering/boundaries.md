# Nx Boundaries Guidance

## Overview
- Keep project boundaries clear and enforce tags.
- Boundaries reduce accidental dependency coupling.

## Boundary Rules
1. Libraries → should only be used by intended projects.
2. Feature libs → should not be imported outside their domain.
3. UI libs → should be reusable across multiple apps, with consistent styling.
4. Data libs → encapsulate APIs or database access, keep private internals hidden.

## Enforcement
- Encourage `nx dep-graph` and `nx lint --tags` to verify boundaries.
- Recommend automated checks in CI pipelines.

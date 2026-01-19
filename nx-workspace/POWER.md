---
name: "nx-workspace"
displayName: "Nx Workspace Expert"
description: "Expert guidance for working in Nx monorepos"
keywords:
  - nx
  - nx workspace
  - monorepo
  - generators
  - nx targets
---

# Onboarding

When this power activates:

1. Assume the user is working inside an Nx monorepo.
2. Ask which Nx version they are using only if relevant.
3. Prefer modern Nx patterns (project.json, inferred targets).
4. Avoid deprecated executors unless explicitly requested.

# Core Guidance

Refer to the steering files in `steering/`:

- Generators: `steering/generators.md`
- Targets: `steering/targets.md`
- Boundaries: `steering/boundaries.md`

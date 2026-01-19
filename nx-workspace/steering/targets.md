# Nx Targets Guidance

## Overview
- Nx targets are the commands run inside projects: build, test, lint, serve.
- Default to affected-based workflows when possible.

## Recommended Patterns
- `nx run <project>:<target>` → explicit command
- `nx affected:build` → builds only affected projects
- `nx graph` → visualizes dependencies

## Target Best Practices
1. Always explain why a target is chosen.
2. Suggest caching and parallelization for large repos.
3. Recommend custom targets only if required by workflow.

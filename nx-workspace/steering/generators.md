# Nx Generators Guidance

## Overview
- Prefer using Nx generators (`nx g`) instead of manual folder creation.
- Always ask the type of library or application before suggesting a generator.
- Suggest using `--directory` or `--tags` for project organization.

## Common Generators
- `nx g @nrwl/js:lib <name>` → standard JS/TS library
- `nx g @nrwl/react:lib <name>` → React UI library
- `nx g @nrwl/node:app <name>` → Node application
- `nx g @nrwl/nest:app <name>` → NestJS backend

## Generator Best Practices
1. Confirm project type with user.
2. Always include tags to enforce boundaries.
3. Suggest standalone configs unless workspace convention forbids.
4. Show the user the generated project in `nx graph`.

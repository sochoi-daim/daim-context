# Backend Context Document Template

```markdown
# Context: {project-name}

## Overview
- **Type**: Backend
- **Framework**: {Express / NestJS / Fastify} {version}
- **Runtime**: Node.js {version}
- **Description**: {one-line description}

## Current Work
- **Task**: {current task}
- **Scope**: {affected areas}

## Tech Stack
| Category | Choice |
|----------|--------|
| Language | TypeScript / JavaScript |
| Framework | {Express / NestJS / Fastify} {version} |
| Database | {PostgreSQL / MySQL / MongoDB / ...} |
| ORM/ODM | {Prisma / TypeORM / Mongoose / ...} |
| Auth | {JWT / session / OAuth / API key / ...} |
| API Style | {REST / GraphQL / gRPC} |
| Testing | {Jest / Vitest / Supertest / ...} |
| Deploy | {Docker / AWS / GCP / ...} |

## Project Structure
{path + role summaries}

## Entry Point
- `{path}` — {description}

## Key Modules
| Module | Path | Role |
|--------|------|------|
| {name} | {path} | {role} |

## API Endpoints
| Method | Path | Purpose | Auth |
|--------|------|---------|------|
| {GET/POST/...} | {path} | {purpose} | {required/public} |

## Database Schema (key tables/collections)
| Table/Collection | Purpose | Key Fields |
|-----------------|---------|------------|
| {name} | {purpose} | {fields} |

## Middleware / Interceptors
| Name | Purpose |
|------|---------|
| {name} | {purpose} |

## Environment Variables
| Variable | Purpose |
|----------|---------|
| {name} | {purpose} |

## Notes & Caveats
- {any important context}
```

# Unity Context Document Template

```markdown
# Context: {project-name}

## Overview
- **Type**: Unity
- **Unity Version**: {version}
- **Render Pipeline**: {URP / HDRP / Built-in}
- **Target Platform**: {PC / Mobile / WebGL / Console}
- **Description**: {one-line description}

## Current Work
- **Task**: {current task}
- **Scope**: {affected areas}

## Scene Structure
| Scene | Purpose | Loading |
|-------|---------|---------|
| {name} | {purpose} | {initial / additive / ...} |

## Key Scripts
| Script | Path | Role |
|--------|------|------|
| {GameManager} | {Assets/Scripts/...} | {role} |

## Assembly Definitions
| Assembly | Path | Dependencies |
|----------|------|-------------|
| {name} | {path} | {deps} |

## Third-Party Packages
| Package | Version | Purpose |
|---------|---------|---------|
| {name} | {version} | {purpose} |

## REST API Integration (if applicable)
- **Base URL**: {url}
- **Auth**: {method}

| Method | Endpoint | Purpose |
|--------|----------|---------|
| {GET/POST/...} | {path} | {purpose} |

## Project Structure
{path + role summaries — Assets/ level}

## Build & Deploy
- **Pipeline**: {Unity Cloud Build / Jenkins / manual}
- **Target**: {platform details}

## Notes & Caveats
- {any important context}
```

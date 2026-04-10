---
name: context
description: |
  Skill for quickly understanding a new project or codebase and generating
  a token-efficient, reusable Context Document.
  Specialized for Frontend (React, Next.js, Vue), Unity (URP), and Backend (Express, NestJS) projects.
  Triggered by "/context", "/context fast", "/context frontend", "/context unity", "/context backend" commands.
  Also triggered by requests like "analyze this project", "create a context document",
  "generate context without questions".
  Covers new projects, unfamiliar modules, and handover scenarios.
  Related commands: /save, /show, /update, /help (separate skills).
---

# Dev Context Guide

Systematically analyze any project with a single command and generate
a **compressed Context Document** so future Claude conversations can
skip repeated explanations and jump straight into work.

---

## IMPORTANT: First Action When This Skill Is Invoked

**You MUST follow this routing logic BEFORE doing anything else. Do NOT skip this step.**

1. If the user ran `/context fast` → go directly to **Fast Mode**
2. If the user ran `/context frontend`, `/context unity`, or `/context backend` → go directly to **Interview Mode**
3. If the user ran `/context` (no arguments) → **STOP and ask the mode selection below. Do NOT proceed until the user answers.**

**Mode selection prompt (print this exactly when no arguments are given):**

```
How would you like to analyze this project?

  1) Fast — scan files and generate immediately (no questions)
  2) Interview — Q&A for higher accuracy

  (tip: /context fast to skip this prompt next time)
```

**Wait for the user's answer**, then route:
- **1, "fast", "빠르게", "바로"** → **Fast Mode**
- **2, "interview", "인터뷰", "질문"** → **Interview Mode**

---

## Commands

| Command | Action |
|---------|--------|
| `/context` | Start project analysis (mode selection first) |
| `/context fast` | Skip questions, generate from files immediately |
| `/context frontend` | Interview mode, frontend-specific |
| `/context unity` | Interview mode, Unity-specific |
| `/context backend` | Interview mode, backend-specific |

**Related skills (separate commands):** `/save [path]`, `/show`, `/update`, `/help`

---

## Core Principle: No Assumptions

**Claude must never fill in project details based on general framework knowledge.**

For example, even if told "this project uses NestJS":
- Folder structure, module layout, and endpoints differ per project
- Mark anything unverified as `[needs confirmation]`
- Clearly distinguish confirmed facts from inferences

### Confidence Tags

Every item in the document uses one of these tags:

| Tag | Meaning |
|-----|---------|
| (none) | Directly confirmed from files or code |
| `[inferred]` | Inferred from patterns — high probability but unverified |
| `[needs confirmation]` | No file evidence or uncertain — user must confirm |

After generation, all `[needs confirmation]` items are collected and presented to the user at once.

---

## Fast Mode

Generate a Context Document **immediately with no questions** by scanning the project files.

**Steps:**
1. Auto-detect project type (file structure, extensions, meta files)
2. Auto-detect framework
   - Frontend: `package.json` dependencies → React / Vue / other
   - Unity: `ProjectVersion.txt`, `*.asmdef`, scene files
   - Backend: `package.json`, `Dockerfile`, framework-specific files
3. Fill only verifiable items; mark uncertain items with `[inferred]` / `[needs confirmation]`
4. Output Context Document immediately
5. Collect and present `[needs confirmation]` items:

```
Items that need your confirmation (skip if correct, correct if wrong):
  - Entry point: src/main.ts [inferred]
  - State management: not identified [needs confirmation]
  - API base URL: [needs confirmation]
Run /save [path] after confirming.
```

---

## Interview Mode

Build a high-accuracy document through Q&A. Works even without files.

### Step 1. Identify Project Type

If files/code are attached → auto-analyze, skip to Step 3.
If type was specified via argument (e.g. `/context frontend`) → skip to Step 2.
Otherwise → ask:

```
What type of project is this?
  1) Frontend (React, Next.js, Vue)
  2) Unity (URP)
  3) Backend (Express, NestJS)
  4) Other
```

### Step 2. Type-Specific Interview

Ask one question at a time, proceed after each answer.
If the user answers "skip", "pass", "모름", or "s", mark the item as `[needs confirmation]` and move on.

**Common Questions (all types)**
```
Q1. Project name and one-line description?
Q2. What task are you currently working on?
Q3. Any particularly complex or sensitive areas?
```

**Frontend additional questions** → see `references/web-interview.md`
**Unity additional questions** → see `references/unity-interview.md`
**Backend additional questions** → see `references/backend-interview.md`

### Step 3. File Analysis (when files are provided)

**Auto-analysis**
1. Scan root directory structure
2. Check type-specific meta files
   - Frontend: `package.json`, `tsconfig.json`, `.env.example`
   - Unity: `ProjectSettings/ProjectVersion.txt`, `Packages/manifest.json`, `*.asmdef`
   - Backend: `package.json`, `tsconfig.json`, `.env.example`, `Dockerfile`
3. Sample key folders and modules

**Always ask the user to confirm the entry point**
```
Please specify the entry point (where work begins).
  Frontend examples: src/pages/index.tsx, src/App.vue, src/main.ts
  Unity examples: Assets/Scripts/Managers/GameManager.cs, first scene name
  Backend examples: src/main.ts, src/app.module.ts, src/index.ts
```

### Step 4. Generate Context Document

Fill the appropriate template with collected information:
- Frontend (React / Next.js) → `references/web-template.md` React section
- Frontend (Vue) → `references/web-template.md` Vue section
- Unity → `references/unity-template.md`
- Backend → `references/backend-template.md`

Items mentioned in interview but not confirmed by files → `[inferred]`
Items neither mentioned nor found in files → `[needs confirmation]`

### Step 5. Verification

Collect and present all `[needs confirmation]` items:

```
Please verify the following:
  - [item]: [reason]
  ...
Run /save [path] to save. Let me know if anything is incorrect.
```

---

## After Generation

Once the Context Document is generated, remind the user of available next steps:

```
/save [path] — save to file  |  /show — review  |  /update — modify sections
```

---

## Token Optimization Principles

All generated documents follow these rules:

- Prefer **structured formats** (tables, code blocks, lists) over prose
- Replace full files with **path + role** summaries
- Explain repeated patterns **once and reference**
- **Omit** anything irrelevant to the current task
- Include only **signatures**, not full implementations

---

## Reference Files

| File | Purpose |
|------|---------|
| `references/web-interview.md` | Frontend project additional interview questions |
| `references/unity-interview.md` | Unity project additional interview questions |
| `references/backend-interview.md` | Backend project additional interview questions |
| `references/web-template.md` | Frontend Context Document template (React / Next.js / Vue) |
| `references/unity-template.md` | Unity Context Document template |
| `references/backend-template.md` | Backend Context Document template |

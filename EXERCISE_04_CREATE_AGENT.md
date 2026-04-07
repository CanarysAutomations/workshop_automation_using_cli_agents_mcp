# Exercise 04 — Create a Custom CLI Coding Agent

> **Duration:** 15 minutes | **Feature:** Copilot CLI `/agent` command | **Goal:** Create a named custom coding agent (`helpdesk-crm-agent`) scoped to the Help Desk CRM, then test it with a codebase question to confirm it loaded the right context.

---

## Background

A **custom CLI agent** is a named AI persona with a fixed scope, architecture knowledge, and behaviour rules. Once created, you invoke it with `@helpdesk-crm-agent` in any session — it applies your instructions automatically and stays focused on your project.

---

## Prerequisites

- Completed [Exercise 03 — Generate Custom Project Instructions](EXERCISE_03_CUSTOM_INSTRUCTIONS.md)
- `.github/copilot-instructions.md` exists in the repository
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Open Copilot CLI and Start Agent Creation

```cmd
copilot
```

```
/agent
```

Select **"Create agent with Copilot"**, then paste this prompt:

```
Create a custom coding agent named "helpdesk-crm-agent" for our FastAPI helpdesk ticketing system.

Purpose: implement features, fix bugs, generate tests, review code
Stack: FastAPI, SQLAlchemy, SQLite, Pydantic v2, pytest
Architecture: Route → Service → Repository → Model
Style: PEP 8, type hints, 100-char line limit
Files: app/models/, app/schemas/, app/api/, app/services/, app/repositories/

Scope:
- Allowed paths: app/**, tests/**, .github/**
- Do not modify core/config.py or core/database.py without explicit permission

Behaviour:
- Always follow .github/copilot-instructions.md
- Provide a brief explanation for every suggested change
- Generate tests alongside every code change
- Prefer incremental changes over large rewrites
```

---

## Step 2 — Verify the Agent Was Created

```
/agent list
```

Expected output: `helpdesk-crm-agent — Active`

---

## Step 3 — Test the Agent

```
@helpdesk-crm-agent Explain the ticket creation flow. List every file involved and each file's responsibility.
```

The agent should correctly reference `ticket_routes.py`, `ticket_service.py`, `ticket_repository.py`, and the `Ticket` model and schema.

Type `exit` to close.

---

## Key Takeaways

- Invoke the agent with `@helpdesk-crm-agent` in any session — it carries all scope and instructions automatically.
- Providing exact file paths and the architecture chain in the agent definition significantly improves code generation accuracy.
- Test the agent immediately after creation with a cross-file question to verify it loaded the right context.

> **Next:** [Exercise 05 — Plan the Ticket Assignment Feature](EXERCISE_05_PLAN_FEATURE.md)

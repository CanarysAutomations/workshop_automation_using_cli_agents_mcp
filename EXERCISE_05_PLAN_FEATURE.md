# Exercise 05 — Plan the Ticket Assignment Feature

> **Duration:** 15 minutes | **Feature:** `/model`, `/plan`, Custom Agent | **Goal:** Invoke the custom agent, select the right AI model, and use `/plan` to generate a structured, phase-by-phase implementation plan for the ticket assignment feature before a single line of code is written.

---

## Background

The Help Desk CRM has no way to assign tickets to team members. This exercise uses `/plan` to produce a reviewed implementation plan — covering model, schema, service, route, and tests changes — before any code is delegated. Separating planning from coding catches scope issues early.

---

## Prerequisites

- Completed [Exercise 04 — Create a Custom CLI Coding Agent](EXERCISE_04_CREATE_AGENT.md)
- `helpdesk-crm-agent` active (`/agent list` shows it)
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Start a Session and Invoke the Agent

```cmd
copilot
```

```
/agent list
@helpdesk-crm-agent Hello! I need your help planning a new feature.
```

---

## Step 2 — Select an AI Model

```
/model
/model gpt-4
```

> **Guidelines:** `gpt-4` / `claude-3-opus` for multi-file features; `gpt-4-turbo` / `claude-3-sonnet` for most tasks.

---

## Step 3 — Generate the Implementation Plan

```
@helpdesk-crm-agent /plan

Plan the "Assign" feature for the Helpdesk CRM.

Requirements:
1. Add assigned_to (string) and assignee_role (enum) fields to the Ticket model
2. Roles: Developer, Test Engineer, DevOps Engineer
3. PUT endpoint /tickets/{id}/assign
4. Update Pydantic schemas with assignment fields
5. Role validation with HTTP 422 on invalid input
6. Unit tests: valid assignment, invalid role, non-existent ticket

Context:
- Architecture: Route → Service → Repository → Model
- Stack: FastAPI, SQLAlchemy, Pydantic v2, pytest, PEP 8 + type hints
- Files: app/models/, app/schemas/, app/api/, app/services/, app/repositories/

Output: numbered phases, files to change, key code changes, test cases
```

Review the plan — it should cover at least five phases (Model → Schema → Repository/Service → Route → Tests).

---

## Key Takeaways

- `/plan` produces a reviewable plan before code is written — use it to catch missing layers or wrong file targets.
- Selecting a powerful model (`gpt-4`) for planning improves phase coverage for multi-file features.
- Keep the plan open in the session; you will pass it directly to `/delegate` in Exercise 06.

> **Next:** [Exercise 06 — Delegate Implementation & Review the PR](EXERCISE_06_DELEGATE_IMPLEMENTATION.md)

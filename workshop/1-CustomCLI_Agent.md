# Exercise 1: Create a Custom CLI Agent

> **Time:** ~30 minutes
> **Standalone:** Requires Exercise 0 (environment setup).

## Goal

Create a `.github/copilot-instructions.md` file for the Help Desk project, then use the `/agent` command in Copilot CLI to build a custom coding agent scoped to the application.

---

## Steps

**1.** Navigate to the project and start Copilot CLI chat:

```powershell
cd Help_Desk_Application
gh copilot chat
```

**2.** Create the `.github` directory (in a second terminal):

```powershell
mkdir .github
```

**3.** In the chat, generate the custom instructions file:

```
Create a custom instructions file .github/copilot-instructions.md for the Helpdesk CRM with these guidelines:
- Framework: FastAPI with SQLAlchemy ORM and SQLite
- Architecture: Route → Service → Repository → Model
- Code style: PEP 8, type hints required, 100-char line limit
- Testing: pytest for unit and integration tests
- Validation: Pydantic v2 schemas
- Documentation: docstrings on all functions and classes
Write the complete file content.
```

Save the output to `.github/copilot-instructions.md`.

**4.** Verify the file was saved:

```powershell
Get-Content .github\copilot-instructions.md
```

**5.** Create the custom agent using the `/agent` command:

```
/agent
```

Select **Create agent with Copilot**, then enter:

```
Create a custom coding agent named "helpdesk-crm-agent" for our FastAPI helpdesk ticketing system.
- Purpose: implement features, fix bugs, generate tests, write docs
- Stack: FastAPI, SQLAlchemy, SQLite, Pydantic, pytest
- Architecture: Route → Service → Repository → Model
- Scope: app/**, tests/**, .github/**
- Always follow .github/copilot-instructions.md
- Generate tests alongside every code change
```

**6.** Confirm the agent was created:

```
/agent list
```

Expect `helpdesk-crm-agent` to appear with status **Active**.

**7.** Test the agent with a project-specific question:

```
@helpdesk-crm-agent Explain the ticket creation flow. List all files involved.
```

Expect the response to reference files in `app/api/`, `app/services/`, `app/repositories/`, and `app/models/`.

---

## What You Built

| Item | Location |
|---|---|
| Custom instructions | `.github/copilot-instructions.md` |
| Custom agent | `helpdesk-crm-agent` (Active) |

Proceed to [Exercise 2 — Plan & Implement Assign Feature](exercise-2.md).

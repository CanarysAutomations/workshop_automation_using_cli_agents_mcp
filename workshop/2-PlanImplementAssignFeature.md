# Exercise 2: Plan & Implement Assign Feature

> **Time:** ~45 minutes
> **Standalone:** Requires Exercise 1 (`helpdesk-crm-agent` must exist).

## Goal

Use `/model`, `/plan`, `/context`, and `/delegate` to generate an implementation plan for a ticket assignment feature and let Copilot push the changes as a draft pull request.

---

## Steps

**1.** Start Copilot CLI chat and confirm the agent is available:

```powershell
gh copilot chat
```

```
/agent list
```

**2.** Select a model suitable for multi-file feature work:

```
/model gpt-4
```

**3.** Generate a structured implementation plan:

```
@helpdesk-crm-agent /plan

Add an Assign feature to tickets in the Help Desk CRM.
Requirements:
- Add assigned_to (string) and assignee_role (enum) fields to the Ticket model
- Roles: Developer, Test Engineer, DevOps Engineer
- New endpoint: PUT /tickets/{id}/assign
- Update Pydantic v2 schemas with AssigneeRole enum
- Add validation for roles
- Unit tests for the new logic
Follow .github/copilot-instructions.md. List every file to modify.
```

**4.** Review the plan output. Confirm it covers:
- `app/models/ticket.py` — new columns
- `app/schemas/ticket.py` — AssigneeRole enum
- `app/api/ticket_routes.py` — new route
- `app/services/ticket_service.py` — business logic
- `app/repositories/ticket_repository.py` — data access
- `tests/` — new test file

**5.** Check token context before delegating:

```
/context
```

If usage is high, trim with `/context remove app/templates/index.html`.

**6.** Delegate the full implementation:

```
/delegate

Implement the complete ticket assignment feature:
- Add assigned_to and assignee_role fields to Ticket model
- Update schemas with AssigneeRole enum
- Create PUT /tickets/{id}/assign endpoint
- Add service and repository methods
- Generate unit and integration tests
- PEP 8 compliance and type hints throughout
Follow .github/copilot-instructions.md
```

**7.** When prompted **"Send this session to GitHub?"**, press Enter to select **Yes**.

Copilot creates a branch (e.g., `copilot/joyous-ferret`), pushes changes, and opens a **draft PR** automatically.

**8.** View the created PR:

```
@helpdesk-crm-agent Give me the URL and a summary of the draft PR just created.
```

---

## What You Built

| Step | Result |
|---|---|
| `/plan` | Structured per-file implementation plan |
| `/context` | Token usage reviewed |
| `/delegate` | Multi-file implementation pushed to GitHub |
| Draft PR | Automatically created on `copilot/<branch>` |

Proceed to [Exercise 3 — Build CI/CD Workflows](exercise-3.md).

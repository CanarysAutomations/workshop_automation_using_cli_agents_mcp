# Exercise 13 — Debug: Introduce Bugs & Diagnose

> **Duration:** 15 minutes | **Feature:** `gh copilot explain`, `gh copilot suggest` | **Goal:** Introduce two realistic runtime bugs into the assignment service, reproduce the test failures, and use `gh copilot explain` and `gh copilot suggest` to diagnose both errors from the terminal — without opening the code editor.

---

## Background

`gh copilot explain` decodes a raw error message or stack trace into a plain-English diagnosis. `gh copilot suggest` generates the exact shell command you need to investigate a live problem. Together they cover the first half of the debugging loop: understand the error, then query the system.

| Tool | Input | Output |
|---|---|---|
| `gh copilot explain` | Error text | Root cause + recommended fix |
| `gh copilot suggest` | Plain-language task | Shell command to run |

---

## Prerequisites

- Completed [Exercise 06 — Delegate Implementation & Review the PR](EXERCISE_06_DELEGATE_IMPLEMENTATION.md)
- `PUT /tickets/{id}/assign` endpoint exists in `app/api/ticket_routes.py`
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Introduce the Bugs

Open `app/services/ticket_service.py` and edit `assign_ticket` to:

```python
def assign_ticket(self, ticket_id: int, assigned_to: str, assignee_role: str) -> Ticket:
    ticket = self.repository.get_by_id(ticket_id)
    # BUG 1: no None check — AttributeError when ticket does not exist
    ticket.assigned_to = assigned_to
    # BUG 2: raw string bypasses enum validation
    ticket.assignee_role = "SeniorDeveloper"
    return self.repository.update(ticket)
```

Save the file.

---

## Step 2 — Reproduce the Failures

```powershell
pytest tests/ -v
```

Expected failures:

```
FAILED tests/test_ticket_assignment.py::test_assign_nonexistent_ticket
       AttributeError: 'NoneType' object has no attribute 'assigned_to'

FAILED tests/test_ticket_assignment.py::test_assign_invalid_role
       ValueError: 'SeniorDeveloper' is not a valid AssigneeRole
```

---

## Step 3 — Diagnose Bug 1 with `gh copilot explain`

```cmd
gh copilot explain "AttributeError: 'NoneType' object has no attribute 'assigned_to' in app/services/ticket_service.py"
```

Copilot identifies that `get_by_id()` returned `None` and recommends adding a `None` check that raises `HTTPException(status_code=404)`.

---

## Step 4 — Diagnose Bug 2 with `gh copilot explain`

```cmd
gh copilot explain "ValueError: 'SeniorDeveloper' is not a valid AssigneeRole"
```

Copilot explains the enum rejects the raw string and advises wrapping the lookup in `try/except ValueError` returning HTTP 422.

---

## Step 5 — Investigate the Database with `gh copilot suggest`

```cmd
gh copilot suggest "show rows in the tickets table where assignee_role is not a valid enum value using sqlite3"
```

Run the suggested command to check for corrupted data:

```powershell
sqlite3 helpdesk.db "SELECT id, assignee_role FROM tickets WHERE assignee_role NOT IN ('Developer','Test Engineer','DevOps Engineer');"
```

---

## Key Takeaways

- `gh copilot explain` converts a cryptic traceback into a precise root cause — use it before reaching for a search engine.
- `gh copilot suggest` generates the exact investigative command; always review the suggestion before running it on a live system.
- Diagnosing both errors before touching the editor reinforces understanding and produces more targeted fixes.

> **Next:** [Exercise 14 — Debug: Fix, Validate & Commit](EXERCISE_14_DEBUGGING_FIX.md)

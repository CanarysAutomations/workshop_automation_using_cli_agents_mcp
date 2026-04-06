# Exercise 06 — Debugging with GitHub Copilot

> **Duration:** 25 minutes &nbsp;|&nbsp; **Copilot Feature:** `gh copilot explain`, `gh copilot suggest`, `@terminal`, VS Code Inline Chat &nbsp;|&nbsp; **Goal:** Introduce a runtime bug into the ticket assignment service, reproduce the failure, and use Copilot tools across the terminal and editor to diagnose and fix it.

---

## Background

This exercise introduces two bugs into `assign_ticket` — a missing `None` guard and an unvalidated enum value — then uses four complementary Copilot debugging tools to move from error to fix without guessing.

| Tool | Where | Use For |
|---|---|---|
| `gh copilot explain` | Terminal | Plain-English traceback diagnosis |
| `gh copilot suggest` | Terminal | Shell commands to investigate the live system |
| `@terminal` | VS Code Chat | Reading the last terminal error in context |
| Inline Chat `/fix` | VS Code Editor | Targeted line-level repair |

---

## Prerequisites

- Completed [Exercise 02 — Plan & Implement Feature](EXERCISE_2_PLAN_ASSIGN_FEATURE.md)
- `PUT /tickets/{id}/assign` endpoint present in `app/api/ticket_routes.py`
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Introduce the Bugs

Open `app/services/ticket_service.py` and edit `assign_ticket` to match:

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

## Step 2 — Reproduce the Failure

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

## Step 3 — Diagnose with `gh copilot explain`

```cmd
gh copilot explain "AttributeError: 'NoneType' object has no attribute 'assigned_to' in app/services/ticket_service.py"
```

Copilot identifies that `get_by_id()` returned `None` and advises adding a `None` check that raises `HTTPException(status_code=404)`.

```cmd
gh copilot explain "ValueError: 'SeniorDeveloper' is not a valid AssigneeRole"
```

Copilot advises wrapping the enum lookup in a `try/except ValueError` and returning `HTTP 422`.

---

## Step 4 — Investigate the Database with `gh copilot suggest`

```cmd
gh copilot suggest "show all rows in the tickets table where assignee_role is not a valid enum value using sqlite3"
```

Run the suggested command to confirm whether any corrupt data was written:

```powershell
sqlite3 helpdesk.db "SELECT id, assignee_role FROM tickets WHERE assignee_role NOT IN ('Developer','Test Engineer','DevOps Engineer');"
```

---

## Step 5 — Connect Error to Code with `@terminal`

Re-run the first failing test so the stack trace is visible in the VS Code terminal panel:

```powershell
pytest tests/test_ticket_assignment.py::test_assign_nonexistent_ticket -v
```

Open Copilot Chat (`Ctrl+Alt+I`) and type — without copying anything:

```
@terminal What does the last error mean and which file should I fix first?
```

Copilot reads the terminal output and returns the file name, line number, and explanation.

---

## Step 6 — Fix with VS Code Inline Chat

Open `app/services/ticket_service.py`. Place the cursor on the line after `ticket = self.repository.get_by_id(ticket_id)`, press `Ctrl+I`, and type:

```
/fix Add a None guard that raises HTTPException(status_code=404, detail="Ticket not found") when ticket is None.
```

Accept with `Tab`. Then select the `"SeniorDeveloper"` line, press `Ctrl+I`:

```
/fix Replace the raw string with an AssigneeRole enum lookup wrapped in try/except ValueError that raises HTTPException(status_code=422, detail="Invalid assignee role").
```

Accept the suggestion.

---

## Step 7 — Cross-File Validation with the Custom Agent

```cmd
copilot
```

```
@helpdesk-crm-agent Review assign_ticket in app/services/ticket_service.py and the PUT /tickets/{id}/assign route in app/api/ticket_routes.py. Confirm HTTP 404 for missing ticket, HTTP 422 for invalid role, and HTTP 200 for a valid assignment. Flag any remaining gaps.
```

Address any issues the agent flags, then exit.

---

## Step 8 — Verify and Commit

```powershell
pytest tests/ -v --tb=short
```

All tests should pass. Commit:

```cmd
git add app/services/ticket_service.py
git commit -m "fix: add None guard and enum validation to assign_ticket"
git push origin main
```

Confirm CI goes green in the **Actions** tab.

---

## Key Takeaways

- `gh copilot explain` decodes a traceback into a precise root cause — use it before searching the web.
- `gh copilot suggest` generates the exact investigation command for a live system; review before running.
- `@terminal` reads the last terminal output automatically — no copy-pasting required.
- Inline Chat `/fix` repairs the exact faulty line with full file context — faster than rewriting a whole function.
- The custom agent catches cross-file gaps that single-file inline fixes can miss.

> Return to the [Workshop README](Readme.md) for next steps and further learning resources.

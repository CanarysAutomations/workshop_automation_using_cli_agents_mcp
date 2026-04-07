# Exercise 14 — Debug: Fix, Validate & Commit

> **Duration:** 10 minutes | **Feature:** `@terminal`, VS Code Inline Chat `/fix`, Custom Agent | **Goal:** Use `@terminal` to connect the live error to the editor, apply targeted fixes with VS Code Inline Chat, do a cross-file validation with the custom agent, then commit and confirm CI goes green.

---

## Background

With the root causes identified in Exercise 13, this exercise applies the fixes using the two most surgical Copilot tools: `@terminal` (reads the last terminal output in context) and Inline Chat `/fix` (repairs the exact faulty line with full file context). The custom agent then does a cross-file sanity check before committing.

---

## Prerequisites

- Completed [Exercise 13 — Debug: Introduce Bugs & Diagnose](EXERCISE_13_DEBUGGING_DIAGNOSE.md)
- VS Code open with `app/services/ticket_service.py` visible
- Terminal panel showing the pytest failure output

---

## Step 1 — Connect Error to Code with `@terminal`

Re-run the first failing test so the stack trace appears in the VS Code terminal panel:

```powershell
pytest tests/test_ticket_assignment.py::test_assign_nonexistent_ticket -v
```

Without copying anything, open Copilot Chat (`Ctrl+Alt+I`):

```
@terminal What does the last error mean and which file should I fix first?
```

Copilot reads the terminal output and returns the file name and line number — no copy-paste required.

---

## Step 2 — Fix Bug 1 with VS Code Inline Chat

In `app/services/ticket_service.py`, place the cursor on the line after `ticket = self.repository.get_by_id(ticket_id)`.

Press `Ctrl+I` and type:

```
/fix Add a None guard that raises HTTPException(status_code=404, detail="Ticket not found") when ticket is None.
```

Accept with `Tab`.

---

## Step 3 — Fix Bug 2 with VS Code Inline Chat

Select the line containing `"SeniorDeveloper"`, press `Ctrl+I`:

```
/fix Replace the raw string with an AssigneeRole enum lookup wrapped in try/except ValueError that raises HTTPException(status_code=422, detail="Invalid assignee role").
```

Accept the suggestion.

---

## Step 4 — Cross-File Validation with the Custom Agent

```cmd
copilot
```

```
@helpdesk-crm-agent Review assign_ticket in app/services/ticket_service.py and PUT /tickets/{id}/assign in app/api/ticket_routes.py. Confirm HTTP 404 for missing ticket, HTTP 422 for invalid role, HTTP 200 for valid assignment. Flag any gaps.
```

Address any issues flagged, then type `exit`.

---

## Step 5 — Re-run Tests and Commit

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

- `@terminal` reads the last terminal output automatically — the most frictionless way to start a debugging conversation in VS Code.
- Inline Chat `/fix` repairs exactly the faulty line with full file context — faster and more accurate than rewriting a whole function.
- The custom agent catches cross-file gaps (e.g., the route handler not forwarding 422) that single-file fixes miss.
- Commit only after all tests pass — never push a partially-fixed state.

> **Workshop complete!** Return to the [Workshop README](Readme.md) for further learning resources.

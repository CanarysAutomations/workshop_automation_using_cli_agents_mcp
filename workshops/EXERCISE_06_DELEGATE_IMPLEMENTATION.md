# Exercise 06 — Delegate Implementation & Review the PR

> **Duration:** 15 minutes | **Feature:** `/context`, `/delegate`, Draft PR | **Goal:** Check token usage with `/context`, hand off the full implementation plan to Copilot with `/delegate`, and review the auto-created draft pull request.

---

## Background

With the plan from Exercise 05 confirmed, this exercise uses `/delegate` to push the full implementation to GitHub automatically. Copilot creates a branch, commits all code changes, and opens a draft PR — keeping human review in the loop before anything merges.

---

## Prerequisites

- Completed [Exercise 05 — Plan the Ticket Assignment Feature](EXERCISE_05_PLAN_FEATURE.md)
- Still inside the Copilot CLI session with the plan visible, or restart with `copilot`
- Repository already pushed to GitHub (needed for PR creation)

---

## Step 1 — Monitor Token Usage with `/context`

Before delegating, check context size:

```
/context
```

If near the limit, trim unnecessary files:

```
/context remove app/templates/index.html
/context add app/models/ticket.py
```

> Overflowing context causes Copilot to silently drop earlier instructions, leading to incomplete output.

---

## Step 2 — Delegate the Full Implementation

```
/delegate

Implement the complete ticket assignment feature:
1. Add assigned_to (string) and assignee_role (AssigneeRole enum) to Ticket model
2. Update TicketCreate, TicketUpdate, TicketResponse schemas in app/schemas/ticket.py
3. Add assign_ticket(ticket_id, assigned_to, assignee_role) to TicketRepository
4. Add assign_ticket to TicketService with role validation (HTTP 422 on bad input)
5. Create PUT /tickets/{id}/assign endpoint in ticket_routes.py
6. Write unit tests: valid assignment, invalid role, non-existent ticket (HTTP 404)
7. PEP 8, type hints, follow .github/copilot-instructions.md throughout
```

When prompted **"Send this session to GitHub?"**, select **1 — Yes**.

---

## Step 3 — Review the Draft Pull Request

Once Copilot finishes, ask:

```
@helpdesk-crm-agent Give me a summary of the pull request that was just created.
```

Copilot returns the PR number, branch name, files changed, and CI status. Open the PR in your browser to review the diff before marking it ready for review.

---

## Key Takeaways

- `/context` before `/delegate` prevents context overflow that silently truncates generated output.
- `/delegate` branches, commits, and opens a **draft** PR — the draft status prevents accidental merges before review.
- Always read the PR diff before approving; check that only the expected files were changed.

> **Next:** [Exercise 07 — Generate CI & CD Workflows](EXERCISE_07_CI_CD_WORKFLOWS.md)

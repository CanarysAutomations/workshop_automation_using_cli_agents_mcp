# Exercise 02 — Plan & Implement the Ticket Assignment Feature

> **Duration:** 30 minutes &nbsp;|&nbsp; **Copilot Feature:** `/plan`, `/delegate`, Custom Agent &nbsp;|&nbsp; **Goal:** Use the custom agent from Exercise 01 to generate a detailed implementation plan for a ticket assignment feature, monitor context usage, and delegate the full implementation to Copilot.

---

## Background

The Help Desk CRM currently has no way to assign a ticket to a specific team member or role. Product wants tickets assignable to a **Developer**, **Test Engineer**, or **DevOps Engineer**, with the assignee stored persistently and exposed via a dedicated REST endpoint.

Rather than writing the code yourself, you will use the **`/plan`** command to produce a step-by-step implementation plan, review it, then use **`/delegate`** to hand off implementation to the Copilot coding agent. Copilot will push the changes to a branch and open a draft pull request automatically.

---

## What You Will Learn

1. How to invoke a custom agent using `@agent-name` in a CLI session.
2. How to use `/model` to select the best model for complex code generation.
3. How to use `/plan` to generate a structured, phase-by-phase implementation plan.
4. How to use `/context` to monitor token usage and manage context size.
5. How to use `/delegate` to hand off implementation and auto-create a GitHub PR.

---

## Prerequisites

- Completed [Exercise 01 — Create Custom CLI Agent](EXERCISE_1_CLI_AGENT.md)
- `helpdesk-crm-agent` exists (`/agent list` shows it as Active)
- `.github/copilot-instructions.md` is present in the repository
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Start a Copilot CLI Session and Invoke the Agent

```cmd
copilot
```

Confirm the agent is available and select it:

```
/agent list
```

Activate the agent for this session:

```
@helpdesk-crm-agent Hello! I need your help implementing a new feature.
```

The agent should acknowledge and confirm it has loaded your custom instructions.

---

## Step 2 — Select an AI Model

Check available models:

```
/model
```

Select a model suitable for complex code generation:

```
/model gpt-4
```

> **Model guidelines:**
> - `gpt-4` / `claude-3-opus` — architecture decisions and multi-file features
> - `gpt-4-turbo` / `claude-3-sonnet` — balanced performance for most tasks
> - `gpt-3.5-turbo` — quick questions and simple snippets

---

## Step 3 — Generate an Implementation Plan with `/plan`

Use the `/plan` command with the custom agent to produce a structured plan before any code is written.

```
@helpdesk-crm-agent /plan

Create a comprehensive implementation plan for adding an "Assign" feature to tickets in the Helpdesk CRM.

Requirements:
1. Add "assigned_to" (string) and "assignee_role" (enum) fields to the Ticket model
2. Assignee roles: Developer, Test Engineer, DevOps Engineer
3. Create a PUT endpoint /tickets/{id}/assign to handle assignment
4. Update Pydantic schemas to include assignment fields
5. Add validation for assignee roles
6. Write unit tests for the assignment logic
7. Update any relevant documentation

Context:
- Architecture: Route → Service → Repository → Model
- Stack: FastAPI, SQLAlchemy ORM, SQLite, Pydantic v2, pytest
- All code must have type hints and follow PEP 8
- File locations: app/models/, app/schemas/, app/api/, app/services/, app/repositories/

Output:
- Break the work into numbered phases
- List every file to create or modify with the nature of each change
- Include the key code changes for each phase
- List the test cases to create
```

Review the generated plan carefully before proceeding. It should include at minimum:
- Phase 1: Model changes
- Phase 2: Schema changes
- Phase 3: Repository / Service changes
- Phase 4: Route changes
- Phase 5: Tests

---

## Step 4 — Monitor Context Usage with `/context`

Before delegating, check how many tokens the current session is using:

```
/context
```

The output shows how much of the model's context window is occupied. If you are near the limit, trim context by removing files not needed for this feature:

```
/context remove app/templates/index.html
```

To add a specific file that the plan references:

```
/context add app/models/ticket.py
```

> **Why this matters:** If context overflows, Copilot may silently drop earlier instructions or produce incomplete output. Always check before a large delegation.

---

## Step 5 — Delegate Implementation with `/delegate`

Once you are satisfied with the plan, delegate the full implementation:

```
/delegate

Implement the complete ticket assignment feature as planned:

1. Add assigned_to (string) and assignee_role (AssigneeRole enum) to the Ticket model
2. Update Ticket schemas (TicketCreate, TicketUpdate, TicketResponse) in app/schemas/ticket.py
3. Add assign_ticket(ticket_id, assigned_to, assignee_role) to TicketRepository
4. Add assign_ticket method to TicketService with role validation
5. Create PUT /tickets/{id}/assign endpoint in ticket_routes.py
6. Write unit tests covering valid assignment, invalid role, and non-existent ticket scenarios
7. Ensure PEP 8 compliance and type hints on all new and modified code
8. Follow .github/copilot-instructions.md throughout
```

Copilot will display a confirmation prompt:

```
Send this session to GitHub?

Copilot will push your changes to a new branch and create a draft PR.

  1. Yes
  2. No, cancel (Esc)
```

Select **1 — Yes** and press Enter.

---

## Step 6 — Review the Draft Pull Request

Copilot will push the changes, create a branch (e.g., `copilot/assign-feature`), and open a draft PR. Once the job completes:

```
@helpdesk-crm-agent Give me a summary of the pull request that was just created.
```

Copilot will show:
- PR title and number
- Files changed
- Summary of what was implemented
- CI check status

Navigate to the PR in your browser to review the diff before marking it ready for review.

---

## Key Takeaways

- `/plan` separates planning from implementation — reviewing the plan before delegating catches scope creep and architectural mistakes early.
- `/context` lets you see token usage and fine-tune what the model has in view before a large generation task.
- `/delegate` pushes changes to a branch and opens a draft PR — keeping human review in the loop before merging.
- Always invoke your agent with `@agent-name` so it applies custom instructions; generic prompts do not load your project context.

> **Next:** [Exercise 03 — Build CI/CD Workflows](EXERCISE_3_BUILD_WORKFLOW.md)

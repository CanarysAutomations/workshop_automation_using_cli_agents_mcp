# Exercise 01 — Create a Custom CLI Agent

> **Duration:** 30 minutes &nbsp;|&nbsp; **Copilot Feature:** Copilot CLI + `/agent` command &nbsp;|&nbsp; **Goal:** Install and authenticate the GitHub Copilot CLI, clone the Help Desk CRM repository, create domain-specific custom instructions, and generate a custom coding agent tailored to the application.

---

## Background

A **custom CLI agent** is a named AI persona you create inside GitHub Copilot CLI. Once created, you invoke it with `@agent-name` in any Copilot CLI session. The agent carries your custom instructions automatically — it knows your project's architecture, naming conventions, and coding style without you needing to repeat that context every time.

In this exercise you will create an agent called `helpdesk-crm-agent` that understands the FastAPI repository-pattern architecture of the Help Desk CRM. This agent will be used in all subsequent exercises.

---

## What You Will Learn

1. How to install and authenticate the GitHub Copilot CLI extension.
2. How to create a `.github/copilot-instructions.md` file using a Copilot prompt.
3. How to create a named custom agent with `/agent` and configure its scope.
4. How to invoke and test a custom agent using `@agent-name`.

---

## Prerequisites

- Completed [Exercise 00 — Setup & Environment](SetupInstructions.md)
- `gh` authenticated (`gh auth status` shows your username)
- `copilot` command available (`gh copilot --version` returns a version)
- Terminal open inside the `Help_Desk_Application` directory with `.venv` activated

---

## Step 1 — Verify GitHub CLI Authentication

Open a terminal and confirm you are authenticated and in the correct directory:

```cmd
gh auth status
cd Help_Desk_Application
```

Expected: `✓ Logged in to github.com as <your-username>`

> **Note:** If authentication has expired, run `gh auth login` again and follow the browser flow.

---

## Step 2 — Create the `.github` Directory

The `.github` folder holds repository-level configuration files that Copilot reads automatically.

**Windows**

```cmd
mkdir .github
```

**macOS / Linux**

```bash
mkdir -p .github
```

---

## Step 3 — Generate Custom Instructions with Copilot CLI

Custom instructions tell every Copilot session about your project's conventions. You will use Copilot itself to draft them.

**Launch a Copilot CLI chat session:**

```cmd
copilot
```

**Paste the following prompt:**

```
Create a custom instructions file named "copilot-instructions.md" for the Helpdesk CRM application with these guidelines:

1. Project Context: FastAPI-based helpdesk ticketing system
2. Code Style: Follow PEP 8 for Python, use type hints on all functions
3. Architecture: Repository pattern — Routes → Services → Repositories → Models
4. Database: SQLAlchemy ORM with SQLite; never bypass the repository layer
5. Testing: Use pytest for unit and integration tests; write tests alongside code
6. Documentation: Clear docstrings for all public functions and classes
7. Error Handling: Proper exception handling with meaningful HTTP error responses
8. API Design: RESTful endpoints with Pydantic v2 schemas for all request/response validation
```

Copy the generated content and save it to `.github/copilot-instructions.md`.

**Verify the file was created:**

```cmd
type .github\copilot-instructions.md
```

---

## Step 4 — Create a Custom Agent

Still inside the Copilot CLI chat, use the `/agent` command to create your named agent.

```
/agent
```

You will see two options — select **"Create agent with Copilot"** (recommended), then paste this prompt:

```
Create a custom coding agent named "helpdesk-crm-agent" for our FastAPI-based helpdesk ticketing system.

Agent Purpose:
- Implement new features following the repository pattern
- Fix bugs in ticket and customer management modules
- Generate unit and integration tests for services and API endpoints
- Review code for PEP 8 compliance and correct type hints

Agent Capabilities:
- Analyse FastAPI routes, Pydantic schemas, and SQLAlchemy models
- Generate CRUD operations following: Route → Service → Repository → Model
- Create pytest tests with fixtures and assertions
- Suggest performance and readability improvements

Context:
- Stack: FastAPI, SQLAlchemy, SQLite, Pydantic v2, pytest
- Architecture: Route → Service → Repository → Model
- Code style: PEP 8, type hints, 100-character line limit
- File structure: app/models/, app/schemas/, app/api/, app/services/, app/repositories/

Agent Scope:
- Allowed paths: app/**, tests/**, .github/**
- Focus: ticket management, customer management, workflow automation
- Do not modify core/config.py or core/database.py without explicit permission

Agent Behaviour:
- Always follow .github/copilot-instructions.md
- Provide a brief explanation for every suggested change
- Generate tests alongside every code change
- Prefer incremental, reviewable changes over large rewrites
```

**Expected confirmation:**

```
✓ Agent "helpdesk-crm-agent" created successfully
✓ Custom instructions linked
✓ Ready to assist with Helpdesk CRM development

Invoke with: @helpdesk-crm-agent
```

---

## Step 5 — Verify and Test the Agent

**List available agents:**

```
/agent list
```

Expected output includes `helpdesk-crm-agent` with status `Active`.

**Test the agent with a codebase question:**

```
@helpdesk-crm-agent Explain the ticket creation flow in this codebase. List every file involved and briefly describe each file's responsibility.
```

The agent should reference `ticket_routes.py`, `ticket_service.py`, `ticket_repository.py`, and `ticket.py` (model and schema) with accurate descriptions.

Type `exit` to close the session.

---

## Key Takeaways

- `.github/copilot-instructions.md` injects project context into every Copilot CLI session automatically — you never repeat your conventions.
- `/agent` creates a named agent persona; invoke it with `@helpdesk-crm-agent` in any session.
- Always provide explicit scope (allowed paths, frameworks, architecture) when creating an agent — it improves response quality significantly.
- Start prompts broadly (explain the flow) before narrowing to specific tasks — this validates that the agent loaded the right context.

> **Next:** [Exercise 02 — Plan & Implement the Ticket Assignment Feature](EXERCISE_2_PLAN_ASSIGN_FEATURE.md)

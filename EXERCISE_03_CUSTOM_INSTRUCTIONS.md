# Exercise 03 — Generate Custom Project Instructions

> **Duration:** 10 minutes | **Feature:** Copilot CLI + `.github/copilot-instructions.md` | **Goal:** Use Copilot CLI to generate an instructions file that injects your project's conventions — architecture, code style, testing rules — into every subsequent Copilot session automatically.

---

## Background

Without instructions, every Copilot session starts fresh. With a `.github/copilot-instructions.md` file, Copilot automatically loads your project's naming conventions, architecture rules, and coding standards into every conversation — no repeated context required.

---

## Prerequisites

- Completed [Exercise 02 — Clone Repository & Set Up the Python Environment](EXERCISE_02_SETUP_ENVIRONMENT.md)
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Create the `.github` Directory

```cmd
mkdir .github
```

---

## Step 2 — Launch a Copilot CLI Session

```cmd
copilot
```

---

## Step 3 — Generate the Instructions File

Paste the following prompt:

```
Create a custom instructions file named "copilot-instructions.md" for the Helpdesk CRM with these guidelines:

1. Project Context: FastAPI-based helpdesk ticketing system
2. Code Style: PEP 8, type hints on all functions, 100-char line limit
3. Architecture: Repository pattern — Routes → Services → Repositories → Models
4. Database: SQLAlchemy ORM with SQLite; never bypass the repository layer
5. Testing: pytest for unit and integration tests; write tests alongside code
6. Documentation: docstrings for all public functions and classes
7. Error Handling: proper exception handling with meaningful HTTP responses
8. API Design: RESTful endpoints with Pydantic v2 schemas for all validation
```

Copy the generated content and save it to `.github/copilot-instructions.md`.

---

## Step 4 — Verify the File

```cmd
type .github\copilot-instructions.md
```

The file should contain the eight rules in a readable format. Type `exit` to close the Copilot session.

---

## Key Takeaways

- `.github/copilot-instructions.md` is loaded automatically by every Copilot CLI session in this repository — you never repeat project conventions.
- The more specific the instructions (exact tool names, file paths, arch patterns), the more accurate the generated code.
- Treat this file like a living document: update it as the project evolves.

> **Next:** [Exercise 04 — Create a Custom CLI Coding Agent](EXERCISE_04_CREATE_AGENT.md)

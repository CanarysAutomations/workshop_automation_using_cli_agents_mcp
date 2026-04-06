# Exercise 00 — Setup & Environment

> **Duration:** 20 minutes &nbsp;|&nbsp; **Feature:** GitHub CLI, Python venv, Copilot CLI &nbsp;|&nbsp; **Goal:** Clone the Help Desk application, verify the Python environment, install the Copilot CLI, and confirm everything runs before the first exercise.

---

## Background

Every exercise in this workshop runs against a live local copy of the **Help Desk CRM** — a FastAPI application that manages customer support tickets. Before you can use Copilot CLI to plan features, build workflows, or observe self-healing, the application must be cloned, its dependencies installed, and the server confirmed to be reachable.

This exercise also installs the GitHub Copilot CLI extension so that all subsequent exercises can use the `copilot` command from the terminal.

---

## Prerequisites

Confirm the following before continuing:

- [Python 3.11+](https://www.python.org/downloads/) installed and on `PATH`
- [Git](https://git-scm.com/install/) installed
- [GitHub CLI (`gh`)](https://cli.github.com/) installed — run `gh --version` to verify
- [VS Code](https://code.visualstudio.com/download) installed (optional but recommended)
- Active GitHub account with GitHub Copilot access

---

## Step 1 — Install GitHub CLI

If `gh` is not yet installed, follow the steps below. If `gh --version` already returns a version, skip to Step 2.

**Windows (winget)**

```cmd
winget install --id GitHub.cli
gh --version
```

**macOS (Homebrew)**

```bash
brew install gh
gh --version
```

> **Already installed?** Run `winget upgrade --id GitHub.cli` (Windows) or `brew upgrade gh` (macOS) to ensure you are on the latest version.

---

## Step 2 — Authenticate with GitHub CLI

```cmd
gh auth login
```

Follow the interactive prompts:

1. Select **GitHub.com**.
2. Choose **HTTPS** as the preferred protocol.
3. Authenticate via browser — a one-time code will be displayed; paste it at `github.com/login/device`.
4. Authorise **GitHub CLI** when prompted.

Verify authentication:

```cmd
gh auth status
```

Expected output: `✓ Logged in to github.com as <your-username>`

---

## Step 3 — Install GitHub Copilot CLI Extension

```cmd
gh extension install github/gh-copilot
```

Verify the extension is active:

```cmd
gh copilot --version
```

Launch an interactive Copilot CLI session to confirm it works:

```cmd
copilot
```

Type `Hello` and press Enter. You should receive a response from the AI. Type `exit` to close the session.

> **Note:** If `copilot` is not recognised as a standalone command, use `gh copilot chat` instead throughout this workshop.

---

## Step 4 — Clone the Help Desk Application

```cmd
gh repo clone CanarysPlayground/Help_Desk_Application
cd Help_Desk_Application
```

Verify the repository contents:

```cmd
dir
```

You should see `app/`, `tests/`, `requirements.txt`, and `README.md`.

---

## Step 5 — Set Up the Python Environment

**Create and activate a virtual environment:**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Install dependencies:**

```powershell
pip install -r requirements.txt
```

**Start the application:**

```powershell
uvicorn app.main:app --reload
```

Verify the application is running by opening the following URLs in your browser:

| Endpoint | URL |
|---|---|
| Health check | `http://localhost:8000/health` |
| Web UI | `http://localhost:8000/` |
| API Docs (Swagger) | `http://localhost:8000/docs` |

All three should return a valid response. Stop the server with `Ctrl+C`.

---

## Step 6 — Explore the Project Structure

```
Help_Desk_Application/
├── requirements.txt             # Python dependencies
├── app/
│   ├── main.py                 # Application entry point
│   ├── api/                    # Route handlers
│   │   ├── customer_routes.py
│   │   └── ticket_routes.py
│   ├── services/               # Business logic
│   ├── repositories/           # Data access layer
│   ├── models/                 # SQLAlchemy ORM models
│   ├── schemas/                # Pydantic validation schemas
│   ├── core/                   # Configuration & DB connection
│   └── templates/              # HTML frontend
└── tests/
    └── test_health.py
```

Open `app/main.py` and `app/api/ticket_routes.py` in VS Code to familiarise yourself with the codebase before Exercise 01.

---

## Key Takeaways

- `gh auth login` authenticates GitHub CLI for all subsequent `gh` commands.
- `gh extension install github/gh-copilot` adds the `copilot` command to your shell.
- The Help Desk CRM runs at `http://localhost:8000` with Swagger docs at `/docs`.
- All exercises assume you are inside the `Help_Desk_Application` directory with `.venv` activated.

> **Next:** [Exercise 01 — Create Custom CLI Agent](EXERCISE_1_CLI_AGENT.md)


# Exercise 02 — Clone Repository & Set Up the Python Environment

> **Duration:** 10 minutes | **Feature:** Git, Python venv | **Goal:** Clone the Help Desk CRM application, create a Python virtual environment, install dependencies, and verify the server runs before any Copilot work begins.

---

## Background

Every exercise targets the **Help Desk CRM** — a FastAPI ticketing application with customers, tickets, severity levels, and a layered Repository-pattern architecture. You need a working local copy before Copilot CLI can plan features or generate workflows against it.

---

## Prerequisites

- Completed [Exercise 01 — Install GitHub CLI & Authenticate](EXERCISE_01_SETUP_GITHUB_CLI.md)
- `gh auth status` shows your username
- Terminal open with `.venv` not yet activated (you will create it here)

---

## Step 1 — Clone the Help Desk Application

```cmd
gh repo clone CanarysPlayground/Help_Desk_Application
cd Help_Desk_Application
dir
```

You should see `app/`, `tests/`, `requirements.txt`, and `README.md`.

---

## Step 2 — Create and Activate a Virtual Environment

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

---

## Step 3 — Install Dependencies and Start the Server

```powershell
pip install -r requirements.txt
uvicorn app.main:app --reload
```

Verify the application in your browser:

| Endpoint | URL |
|---|---|
| Health check | `http://localhost:8000/health` |
| Web UI | `http://localhost:8000/` |
| Swagger docs | `http://localhost:8000/docs` |

All three should return a valid response. Stop the server with `Ctrl+C`.

---

## Step 4 — Explore the Project Structure

```
Help_Desk_Application/
├── app/
│   ├── main.py            # Entry point
│   ├── api/               # Route handlers
│   ├── services/          # Business logic
│   ├── repositories/      # Data access layer
│   ├── models/            # SQLAlchemy ORM models
│   ├── schemas/           # Pydantic schemas
│   ├── core/              # Config & DB connection
│   └── templates/         # HTML frontend
└── tests/
```

Open `app/api/ticket_routes.py` and `app/services/ticket_service.py` in VS Code to familiarise yourself with the pattern before Exercise 03.

---

## Key Takeaways

- All exercises assume you are inside `Help_Desk_Application` with `.venv` activated.
- The architecture is: **Route → Service → Repository → Model** — every Copilot prompt in this workshop follows that chain.
- Swagger docs at `/docs` let you test API changes without writing any client code.

> **Next:** [Exercise 03 — Generate Custom Project Instructions](EXERCISE_03_CUSTOM_INSTRUCTIONS.md)

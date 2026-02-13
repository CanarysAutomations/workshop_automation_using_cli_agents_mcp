
# Exercise 0: Setup Instructions

Before we get started on the workshop, there are a few tasks we need to complete to get everything ready. We will clone the Help Desk application repository, set up a Python environment, and verify the app runs locally.

## Prerequisites

Before starting, ensure you have the following installed:

- Python 3.11+ (Windows)
- PowerShell (latest)
- Git
- GitHub CLI (optional)
- VS Code (optional)
- GitHub Copilot subscription (active)

## Setting up the Help Desk Application

To work through the exercises, you need a local copy of the application repository.

1. Open VS Code.
2. Open the Command Palette (Ctrl+Shift+P).
3. Type Git: Clone and select it.
4. Paste the repository URL: https://github.com/CanarysPlayground/Help_Desk_Application.git
5. Choose a local directory to clone the repo.
6. After cloning, open the cloned folder in VS Code.

Repo: Help_Desk_Application (owner: CanarysPlayground)
Default branch: main

## Create a Python Environment

Next, create and activate a virtual environment, install dependencies, and start the app.

```powershell
python -m venv .venv
\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn app.main:app
```

After the app starts:

- Health endpoint: http://localhost:8000/health
- UI: http://localhost:8000/

## Project Structure

```
Help_Desk_Application/
├── README.md                    # Project documentation
├── requirements.txt             # Python dependencies
├── .env.example                # Environment variables template
├── app/
│   ├── main.py                 # Application entry point
│   ├── api/                    # API route handlers
│   │   ├── customer_routes.py # Customer endpoints
│   │   └── ticket_routes.py   # Ticket endpoints
│   ├── services/               # Business logic layer
│   │   ├── customer_service.py
│   │   └── ticket_service.py
│   ├── repositories/           # Data access layer
│   │   ├── customer_repository.py
│   │   └── ticket_repository.py
│   ├── models/                 # SQLAlchemy ORM models
│   │   ├── customer.py
│   │   └── ticket.py
│   ├── schemas/                # Pydantic validation schemas
│   │   ├── customer.py
│   │   └── ticket.py
│   ├── core/                   # Core configuration
│   │   ├── config.py          # App settings
│   │   └── database.py        # Database connection
│   └── templates/              # HTML templates
│       └── index.html         # Frontend UI
├── tests/                      # Test files
│   └── test_health.py
└── workshop/                   # Workshop materials
    ├── exercises/
    └── stages/
```

## Exercise Progression

- Exercise 1: Create Custom CLI Agent (30 min)
- Exercise 2: Plan and Implement Assign Feature (45 min)
- Exercise 3: Build CI/CD Workflows (40 min)
- Exercise 4: Observe Self-Healing (30 min)

Total workshop time: about 2.0 hours

## Summary

You now have the Help Desk application cloned locally and can run it with a local Python environment. This setup will be used throughout the remaining exercises.

## Next step

Proceed to Exercise 1: Create Custom CLI Agent in [EXERCISE_1_CLI_AGENT.md](EXERCISE_1_CLI_AGENT.md).


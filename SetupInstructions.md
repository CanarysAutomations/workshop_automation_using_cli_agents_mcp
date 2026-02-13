
```markdown
## 🎯 Workshop Exercises Setup Instructions

This workshop teaches you how to integrate AI-powered agents throughout the Software Development Lifecycle (SDLC) using GitHub Copilot CLI, SDK, MCP Server, and Multi-Agent orchestration.

**Application:** Help Desk CRM - A production-structured helpdesk ticketing system built with FastAPI, featuring customer management, ticket tracking, and a layered architecture.

---

## 📦 Initial Setup: Help Desk Application

### Prerequisites

Before starting, ensure you have:

| Requirement | Version | Purpose |
|------------|---------|---------|
| **Python** | 3.11+ | Backend runtime |
| **PowerShell** | Latest | Command execution (Windows) |
| **GitHub CLI** | Latest | Repository management |
| **Git** | Latest | Version control |
| **GitHub Copilot Subscription** | Active | AI agent features |
| **VS Code** | Latest (optional) | Code editor |

## 🚀 Step 1: Clone the Repository


Repo: Help_Desk_Application (owner: CanarysPlayground)
Default Branch: main 

clone this repo in VS code
- Open VS Code
- Open Command Palette (Ctrl+Shift+P)
- Type "Git: Clone" and select it
- Paste the repository URL: `https://github.com/CanarysPlayground/Help_Desk_Application.git`
- Choose a local directory to clone the repo
- After cloning, open the cloned folder in VS Code
### Step 2: Set Up Python Environment

## Prerequisites
- Python 3.11+ on Windows
- PowerShell
- Optional: gh (GitHub CLI), rg (ripgrep), curl

## Install & Run
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn app.main:app 
```

- Health: GET http://localhost:8000/health
- UI: http://localhost:8000/


## 🗂️ Step 3: Understand Project Structure

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


## 📚 Exercise Progression

| Exercise | Topic | Skills Learned | Duration |
|----------|-------|----------------|----------|
| Exercise 1 | Create Custom CLI Agent | Install CLI, create agent with custom instructions | 30 min |
| Exercise 2 | Plan & Implement Assign Feature | Use `/plan`, `/delegate` to add ticket assignment | 45 min |
| Exercise 3 | Build CI/CD Workflows | Create GitHub Actions for testing and self-healing | 40 min |
| Exercise 4 | Observe Self-Healing | Monitor automated dependency fixes via Copilot CLI | 30 min |

**Total Workshop Time:** ~2.0 hours

---

## 🚀 Ready to Start?

Once your setup is verified, proceed to:

### Exercise 1: Create Custom CLI Agent →

Learn how to install Copilot CLI, create custom instructions, and build your first AI coding agent for the Help Desk application.

---

**Happy Learning! 🎉**
```


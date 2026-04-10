# Debugging and Automation with GHCP

> **Audience:** Developers, DevOps Engineers, Tech Leads &nbsp;|&nbsp; **Total Duration:** ~2 hours core + ~55 min optional &nbsp;|&nbsp; **Pre-requisites:** GitHub Copilot access, GitHub CLI, Python 3.11+, VS Code with GitHub Copilot Chat extension

---

## What You Will Build

A fully automated developer workflow around the **Help Desk CRM** — a realistic customer support ticketing system built with FastAPI and SQLAlchemy. You will use **GitHub Copilot CLI**, **custom agents**, **GitHub Actions**, the **Copilot SDK**, and **Copilot debugging tools** to automate every phase of the development lifecycle.

| Capability | Description |
|---|---|
| Customer Management | Full CRUD for customer records |
| Ticket Management | Create, assign, and resolve support tickets with severity levels |
| Role-Based Assignment | Assign tickets to Developer, Test Engineer, or DevOps roles |
| RESTful API | Auto-documented endpoints via FastAPI + Swagger UI |
| Layered Architecture | Routes → Services → Repositories → Models |

> The application code lives in [CanarysPlayground/Help_Desk_Application](https://github.com/CanarysPlayground/Help_Desk_Application). Copilot agents do the heavy lifting — your job is to learn how to direct them.

---

## Prerequisites

- [VS Code](https://code.visualstudio.com/download) with the GitHub Copilot Chat extension
- [Python 3.11+](https://www.python.org/downloads/)
- [Git CLI](https://git-scm.com/install/)
- [GitHub CLI (`gh`)](https://cli.github.com/)
- [GitHub Copilot CLI extension](https://docs.github.com/en/copilot/how-tos/copilot-cli/install-copilot-cli)
- GitHub Copilot subscription (Individual, Business, or Enterprise)

---

## Workshop Map

### Core Track (~2 hours) — Complete in Order

| # | Exercise | Copilot Feature | Duration |
|---|---|---|---|
| 01 | [Install GitHub CLI & Authenticate](./workshops/EXERCISE_01_SETUP_GITHUB_CLI.md) | GitHub CLI + Copilot CLI extension | 10 min |
| 02 | [Clone Repository & Set Up Environment](./workshops/EXERCISE_02_SETUP_ENVIRONMENT.md) | Git, Python venv | 10 min |
| 03 | [Generate Custom Project Instructions](./workshops/EXERCISE_03_CUSTOM_INSTRUCTIONS.md) | `copilot-instructions.md` | 10 min |
| 04 | [Create a Custom CLI Coding Agent](./workshops/EXERCISE_04_CREATE_AGENT.md) | `/agent` command | 15 min |
| 05 | [Plan the Ticket Assignment Feature](./workshops/EXERCISE_05_PLAN_FEATURE.md) | `/model`, `/plan` | 15 min |
| 06 | [Delegate Implementation & Review PR](./workshops/EXERCISE_06_DELEGATE_IMPLEMENTATION.md) | `/context`, `/delegate`, Draft PR | 15 min |
| 07 | [Generate CI & CD Workflows](./workshops/EXERCISE_07_CI_CD_WORKFLOWS.md) | GitHub Actions + Copilot CLI | 15 min |
| 08 | [Generate Self-Healing Workflow & Trigger Failure](./workshops/EXERCISE_08_SELF_HEALING_SETUP.md) | `workflow_run` trigger | 15 min |
| 09 | [Observe & Analyse Self-Healing](./workshops/EXERCISE_09_OBSERVE_SELF_HEALING.md) | Copilot CLI + Actions logs | 10 min |
| 10 | [Review Self-Healing PR & Verify Recovery](./workshops/EXERCISE_10_REVIEW_AND_MERGE.md) | Copilot CLI + PR merge | 10 min |

### Optional Track (~55 minutes) — After Exercise 10

These exercises are self-contained. Complete them if time allows or revisit them after the workshop.

| # | Exercise | Copilot Feature | Duration | Prerequisite |
|---|---|---|---|---|
| 11 | [Build PR Summarizer Agent — SDK Setup](./workshops/EXERCISE_11_SDK_BUILD_AGENT.md) | Copilot SDK + GitHub API | 15 min | Ex 10 |
| 12 | [Test & Automate the PR Summarizer](./workshops/EXERCISE_12_AUTOMATE_PR_SUMMARY.md) | Copilot SDK + GitHub Actions | 15 min | Ex 11 |
| 13 | [Debug: Introduce Bugs & Diagnose](./workshops/EXERCISE_13_DEBUGGING_DIAGNOSE.md) | `gh copilot explain`, `gh copilot suggest` | 15 min | Ex 06 |
| 14 | [Debug: Fix, Validate & Commit](./workshops/EXERCISE_14_DEBUGGING_FIX.md) | `@terminal`, VS Code Inline Chat `/fix` | 10 min | Ex 13 |

---

## Workspace Structure After Workshop

```
Help_Desk_Application/
├── .github/
│   ├── copilot-instructions.md        ← Exercise 03
│   └── workflows/
│       ├── ci.yml                     ← Exercise 07
│       ├── cd.yml                     ← Exercise 07
│       ├── issue-automation.yml       ← Exercise 07
│       ├── self-healing.yml           ← Exercise 08
│       └── copilot-pr-summarizer.yml  ← Exercise 12
├── agents/
│   └── pr_summarizer/
│       ├── config.py                  ← Exercise 11
│       ├── copilot_analyzer.py        ← Exercise 11
│       ├── github_integration.py      ← Exercise 11
│       └── agent.py                   ← Exercise 11
├── app/
│   ├── models/ticket.py               ← Modified Exercise 06
│   ├── schemas/ticket.py              ← Modified Exercise 06
│   ├── api/ticket_routes.py           ← Modified Exercise 06
│   └── services/ticket_service.py     ← Modified Exercise 06 & 14
└── tests/                             ← Updated Exercise 06
```

---

## Key Features Covered

| Feature | Description |
|---|---|
| Copilot CLI | AI-assisted terminal commands and code generation from the shell |
| Custom CLI Agent | Domain-specific agent via `/agent` with scoped instructions |
| `/plan` | Pre-execution planning before Copilot takes action |
| `/delegate` | Full implementation delegation with auto-created GitHub PR |
| `/context` | Token usage monitoring and context window management |
| GitHub Actions | CI, CD, issue automation, and self-healing workflow generation |
| Self-Healing Workflow | Auto-detects broken builds, applies fixes, opens PR |
| Copilot SDK | Programmatic AI analysis of pull requests with comment posting |
| `gh copilot explain` | Plain-English decoding of error messages and stack traces |
| `gh copilot suggest` | Shell investigation commands from natural language |
| VS Code Inline Chat `/fix` | Targeted line-level repairs with full file context |

---

## Getting Started

1. Click **"Use this template"** → **"Create a new repository"**
2. Set the owner to your GitHub account, enter a name (e.g., `cli-agents-workshop`), and click **"Create repository"**
3. Clone the repository locally and open it in VS Code
4. Start with [Exercise 01 — Install GitHub CLI & Authenticate](EXERCISE_01_SETUP_GITHUB_CLI.md)

---

## Further Learning

- [Create Applications with the Copilot CLI](https://github.com/skills/create-applications-with-the-copilot-cli)
- [Integrate MCP with Copilot](https://github.com/skills/integrate-mcp-with-copilot)
- [E2E AI SDLC with GitHub Copilot](https://github.com/CanarysAutomations/E2E-AI-SDLC-Build-with-Github-Copilot)
- [Expand Your Team with the Copilot Coding Agent](https://github.com/skills/expand-your-team-with-copilot)

> **Note:** Complete the Core Track (Ex 01–10) first — each exercise builds on the previous one. Optional exercises (Ex 11–14) are independent and can be done in any order after their listed prerequisite.

> **Instructor Note:** Each exercise has copy-paste prompts — attendees never write code from scratch. Debrief after each exercise by reviewing the generated files before proceeding.

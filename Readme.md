# Automation Using CLI Agents & MCP — Workshop

> **Audience:** Developers, DevOps Engineers, Tech Leads &nbsp;|&nbsp; **Total Duration:** ~2.5 hours &nbsp;|&nbsp; **Pre-requisites:** GitHub Copilot access, GitHub CLI, Python 3.11+, VS Code with GitHub Copilot Chat extension

---

## What You Will Build

A fully automated developer workflow around the **Help Desk CRM** — a realistic customer support ticketing system built with FastAPI and SQLAlchemy. Rather than building the application itself, you will use **GitHub Copilot CLI**, **custom agents**, **GitHub Actions**, and the **Copilot SDK** to automate every phase of the development lifecycle: feature planning, CI/CD, self-healing pipelines, and AI-powered PR summaries.

The Help Desk CRM supports:

| Capability | Description |
|---|---|
| Customer Management | Full CRUD for customer records with contact details |
| Ticket Management | Create, assign, and resolve support tickets with severity levels |
| Role-Based Assignment | Assign tickets to Developer, Test Engineer, or DevOps roles |
| RESTful API | Auto-documented endpoints via FastAPI + Swagger UI |
| Layered Architecture | Routes → Services → Repositories → Models pattern |

> The application code lives in [CanarysPlayground/Help_Desk_Application](https://github.com/CanarysPlayground/Help_Desk_Application). You do not write the application from scratch — Copilot agents and the CLI do the heavy lifting. Your goal is to learn how to direct automation effectively.

---

## Prerequisites

Participants should have the following set up before starting the workshop:

- [VS Code](https://code.visualstudio.com/download) with the GitHub Copilot Chat extension
- [Python 3.11+](https://www.python.org/downloads/)
- [Git CLI](https://git-scm.com/install/)
- [GitHub CLI (`gh`)](https://cli.github.com/)
- [GitHub Copilot CLI extension](https://docs.github.com/en/copilot/how-tos/copilot-cli/install-copilot-cli) (`gh extension install github/gh-copilot`)
- GitHub Copilot subscription (Individual, Business, or Enterprise)
- A GitHub repository to push workflow files (fork or create one)

---

## Workshop Map

> **Two-Track Design:** Complete all core exercises in order (~2.5 hours) — they cover every automation phase end-to-end. Each exercise builds directly on the previous one.

### Core Track (~2.5 hours)

These exercises form the complete automation journey. Complete them in order.

| # | Exercise | Copilot Feature | Duration |
|---|---|---|---|
| 00 | [Setup & Environment](SetupInstructions.md) | GitHub CLI, Python venv | 20 min |
| 01 | [Create Custom CLI Agent](EXERCISE_1_CLI_AGENT.md) | Copilot CLI + `/agent` command | 30 min |
| 02 | [Plan & Implement Feature](EXERCISE_2_PLAN_ASSIGN_FEATURE.md) | `/plan`, `/delegate`, Custom Agent | 30 min |
| 03 | [Build CI/CD Workflows](EXERCISE_3_BUILD_WORKFLOW.md) | GitHub Actions + Copilot CLI | 30 min |
| 04 | [Self-Healing Workflow](EXERCISE_4_SELF_HEALING.md) | Self-healing Actions + Copilot CLI | 20 min |
| 05 | [PR Summarizer with Copilot SDK](EXERCISE_5_PRSUMMARY_SDK.md) | Copilot SDK + GitHub API | 30 min |

> Why this order? Each exercise produces an artifact that the next one builds on: agent → plan → workflows → self-healing → SDK automation. Skipping steps will leave you without required context or files.

### Optional Track (~25 minutes)

This exercise is self-contained and can be done at any point after Exercise 02.

| # | Exercise | Copilot Feature | Duration | Prerequisite |
|---|---|---|---|---|
| 06 | [Debugging with Copilot](EXERCISE_6_DEBUGGING.md) | `gh copilot explain`, `gh copilot suggest`, `@terminal`, Inline Chat | 25 min | Ex 02 |

> Exercise 06 deliberately introduces a bug into the assignment feature and walks through diagnosing and fixing it using every Copilot debugging tool — terminal, inline chat, and the CLI agent.

---

## Workspace Structure After Workshop

```
Help_Desk_Application/
├── .github/
│   ├── copilot-instructions.md        ← Created in Exercise 01
│   └── workflows/
│       ├── ci.yml                     ← Created in Exercise 03
│       ├── cd.yml                     ← Created in Exercise 03
│       ├── issue-automation.yml       ← Created in Exercise 03
│       └── self-healing.yml           ← Created in Exercise 03
├── agents/
│   └── pr_summarizer/
│       ├── config.py                  ← Created in Exercise 05
│       ├── copilot_analyzer.py        ← Created in Exercise 05
│       ├── github_integration.py      ← Created in Exercise 05
│       └── agent.py                   ← Created in Exercise 05
├── app/
│   ├── models/ticket.py               ← Modified in Exercise 02
│   ├── schemas/ticket.py              ← Modified in Exercise 02
│   ├── api/ticket_routes.py           ← Modified in Exercise 02
│   ├── services/ticket_service.py     ← Modified in Exercise 02
│   └── repositories/ticket_repository.py  ← Modified in Exercise 02
└── tests/                             ← Updated in Exercise 02
```

---

## Key Features Covered

| Feature | Description |
|---|---|
| Copilot CLI | AI-assisted terminal commands and code generation from the shell |
| Custom CLI Agent | Domain-specific coding agent created with `/agent` and custom instructions |
| `/plan` Command | Pre-execution implementation planning before Copilot takes action |
| `/delegate` Command | Delegates full implementation to the agent and creates a GitHub PR |
| GitHub Actions | CI, CD, issue automation, and self-healing workflow YAML generation |
| Self-Healing Workflow | Auto-detects broken builds, applies fixes, and opens a PR |
| Copilot SDK | Programmatic AI analysis of pull requests with comment posting |
| GitHub MCP | Model Context Protocol integration for GitHub repository interaction |
| `gh copilot explain` | Plain-English decoding of error messages and stack traces from the terminal |
| `gh copilot suggest` | Generating shell investigation commands from a natural language description |
| VS Code Inline Chat | Targeted `/fix` repairs applied directly to the faulty line with full file context |

---

## Getting Started

1. Click **"Use this template"** → **"Create a new repository"**
2. Set the owner to your GitHub account, enter a repository name (e.g., `cli-agents-workshop`), and click **"Create repository"**
3. Clone the new repository to a local folder
4. Open the cloned folder in VS Code
5. Start with [Exercise 00 — Setup & Environment](SetupInstructions.md)

---

## Further Learning — Try Next

Explore these resources to go deeper on the features covered in this workshop:

- [Create Applications with the Copilot CLI](https://github.com/skills/create-applications-with-the-copilot-cli) — Use GitHub Copilot CLI to scaffold and build applications from the terminal
- [Integrate MCP with Copilot](https://github.com/skills/integrate-mcp-with-copilot) — Connect Model Context Protocol servers to extend Copilot with external tools and data
- [E2E AI SDLC with GitHub Copilot](https://github.com/CanarysAutomations/E2E-AI-SDLC-Build-with-Github-Copilot) — Full software development lifecycle automation with Copilot agents, prompt files, and Plan Mode
- [Expand Your Team with the Copilot Coding Agent](https://github.com/skills/expand-your-team-with-copilot) — Delegate tasks to the Copilot coding agent and collaborate with it like a team member

> **Instructor Note:** Each exercise has clearly demarcated steps with copy-paste prompts. Attendees never need to write code manually — they copy prompts into Copilot CLI or VS Code and let the agent generate the output. Debrief after each exercise by reviewing the generated files before proceeding.

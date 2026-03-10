# Exercise 05: Scaffold the Application with Copilot CLI

| | Exercise 05 Overview |
|---|---|
| **Time** | ~12 minutes |
| **Copilot Feature** | Copilot CLI (`gh copilot suggest` / `gh copilot explain`) |
| **Type** | 🔴 Mandatory |
| **You Will** | Use `gh copilot suggest` to scaffold the full TaskFlow project (directories, entry point, models, routes, config) entirely from the terminal |
| **Input** | Tech stack decision from Exercise 03 (Node.js 20 + Express 4 + PostgreSQL) |
| **Output** | Scaffolded project: `src/`, `tests/`, `package.json`, `.env.example` |
| **Next** | [Exercise 06: Generate & Run Tests →](exercise-06-tests-background-agent.md) |

## Workshop Progress

> [01 BRD](exercise-01-brd-custom-agent.md) → [02 FRD](exercise-02-frd-agent-skills.md) → [03 TSD](exercise-03-tsd-cloud-agent.md) → [04 Instructions](exercise-04-impl-plan-background-agent.md) → `05 Scaffold` → [06 Tests](exercise-06-tests-background-agent.md) → [07 Gate ⚪](exercise-07-quality-gate-cli.md)

---

## Goal

Use **Copilot CLI** to scaffold the full TaskFlow Node.js + Express + PostgreSQL project structure from the terminal — directories, entry point, models, routes, and config files.

---

## ⚡ Starting Here?

Use this tech stack (from TaskFlow TSD):

| Layer | Technology |
|-------|------------|
| Runtime | Node.js 20 |
| Framework | Express 4 |
| Database | PostgreSQL (via `pg` pool) |
| Auth | JWT (`jsonwebtoken` + `bcrypt`) |
| Env | `dotenv` |
| Tests | Jest + supertest |

This exercise uses only the terminal — no prior docs needed.

---

## 5.1 What is Copilot CLI?

`gh copilot suggest` translates natural language into shell commands.  
`gh copilot explain` explains what a command does before you run it.

It is ideal for multi-step scaffolding tasks where you know *what* to do but not the exact commands.

---

## 5.2 Ask CLI to Plan the Scaffold

**1.** Open a terminal in the repo root.

**2.** Ask Copilot CLI for the scaffold commands:

> **CLI Prompt — Plan Scaffold** *(run in terminal)*

```bash
gh copilot suggest "Create a Node.js + Express + PostgreSQL project scaffold for a task management API. 
Needs: src/routes/, src/models/, src/controllers/, src/middleware/, src/config/, 
tests/ folder, .env.example, package.json with express pg bcrypt jsonwebtoken dotenv, 
and a src/index.js entry point with health check route."
```

**3.** CLI will output a shell command. Review it, then run it.

---

## 5.3 Explain Before Running

If the CLI proposes a long command you want to understand:

> **CLI Prompt — Explain Command** *(run in terminal)*

```bash
gh copilot explain "mkdir -p src/{routes,models,controllers,middleware,config} tests"
```

Review the explanation, then run the original command.

---

## 5.4 Generate Boilerplate Files

**1.** Ask CLI to generate the entry point:

> **CLI Prompt — Generate Entry Point** *(run in terminal)*

```bash
gh copilot suggest "Generate src/index.js for Express app: import routes from src/routes/index.js, 
connect to PostgreSQL using DATABASE_URL env var, add /health endpoint returning 200 OK with JSON status, 
listen on PORT env var defaulting to 3000"
```

**2.** Run the suggested command, then open `src/index.js` to verify.

**3.** Generate the database config:

> **CLI Prompt — Generate DB Config** *(run in terminal)*

```bash
gh copilot suggest "Generate src/config/db.js: export a pg Pool using DATABASE_URL from process.env"
```

**4.** Generate the User model:

> **CLI Prompt — Generate User Model** *(run in terminal)*

```bash
gh copilot suggest "Generate src/models/User.js with async functions: 
createUser(email, hashedPassword), findUserByEmail(email), findUserById(id). 
Import Pool from src/config/db.js. Use async/await. Wrap queries in try/catch."
```

---

## 🐛 Debug: Scaffold Fails to Start *(mid-exercise debugging)*

After running scaffold commands, test the entry point:

```bash
node src/index.js
```

If it throws an error, **select the full error output in the terminal**, then open Copilot Chat:

```
#terminalSelection

Debug this startup error following the project's debugging instructions.
```

> Because `.github/copilot-instructions.md` is active, Copilot will:
> 1. Quote the exact file and line that failed
> 2. State the root cause in one sentence
> 3. Show the minimal fix only

**Common errors and quick fixes:**

| Error | Cause | Fix |
|-------|-------|-----|
| `Cannot find module 'express'` | Missing install | `npm install` |
| `Cannot find module './config/db'` | Wrong relative path | Check path in import |
| `ECONNREFUSED` on pg Pool | No DB in this exercise | Comment out pool connect call |
| `process.env.PORT undefined` | Missing .env | Copy `.env.example` to `.env` |

After fixing, re-run:
```bash
node src/index.js &
curl http://localhost:3000/health
# Expected: {"status":"ok"}
kill %1
```

---

## 5.5 Verify the Scaffold

Run:

```bash
find src -type f | sort
```

Confirm you see:
- [ ] `src/index.js`
- [ ] `src/config/db.js`  
- [ ] `src/models/User.js`
- [ ] `src/routes/` directory
- [ ] `src/controllers/` directory
- [ ] `src/middleware/` directory
- [ ] `tests/` directory
- [ ] `.env.example`
- [ ] `package.json`

---

## 5.6 Install Dependencies

> **CLI Prompt — Install Dependencies** *(run in terminal)*

```bash
gh copilot suggest "Install npm dependencies for express pg bcrypt jsonwebtoken dotenv"
```

Run the suggested command, then verify:

```bash
node -e "require('./src/index.js')" 2>&1 | head -5
```

---

## What You Built

| Artifact | Location |
|----------|----------|
| Full project scaffold | `src/` tree |
| Entry point with /health | `src/index.js` |
| Database config | `src/config/db.js` |
| User model | `src/models/User.js` |
| Environment template | `.env.example` |

**CLI strength:** Natural language → runnable shell commands. No scaffolding recipes to memorise.

---

---

| | Navigation |
|---|---|
| **Produces** | `src/` project tree — entry point, models, routes, config; consumed by Exercise 06 |
| **← Previous** | [Exercise 04: Generate Copilot Instructions](exercise-04-impl-plan-background-agent.md) |
| **Next →** | [Exercise 06: Tests + Debug Failures →](exercise-06-tests-background-agent.md) |

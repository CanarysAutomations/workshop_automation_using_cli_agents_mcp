# Exercise 06: Generate & Run Tests via Background Agent

| | Exercise 06 Overview |
|---|---|
| **Time** | ~11 minutes |
| **Copilot Feature** | Background Agent (Copilot Coding Agent) |
| **Type** | 🔴 Mandatory |
| **You Will** | Create a GitHub Issue, assign it to the Copilot coding agent, and let it write the full test suite autonomously — then pull the PR, run tests, and debug failures |
| **Input** | Scaffolded project from Exercise 05 pushed to GitHub |
| **Output** | Complete unit + integration test suite (merged PR), all tests passing |
| **Next** | [Exercise 07: Quality Gate →](exercise-07-quality-gate-cli.md) |

## Workshop Progress

> [01 BRD](exercise-01-brd-custom-agent.md) → [02 FRD](exercise-02-frd-agent-skills.md) → [03 TSD](exercise-03-tsd-cloud-agent.md) → [04 Instructions](exercise-04-impl-plan-background-agent.md) → [05 Scaffold](exercise-05-scaffold-cli.md) → `06 Tests` → [07 Gate ⚪](exercise-07-quality-gate-cli.md)

---

## Goal

Assign the Copilot background agent to write a complete test suite for TaskFlow — unit tests and integration tests — then pull, run, and debug failures using custom instructions.

---

## ⚡ Starting Here?

You need a minimal scaffold for the agent to write tests against. Run:

```bash
mkdir -p src/{models,routes,controllers,middleware,config} tests/{unit,integration}
touch src/index.js src/config/db.js src/models/User.js src/models/Task.js
touch src/routes/auth.js src/routes/tasks.js src/middleware/auth.js
cat > package.json << 'EOF'
{ "name": "taskflow", "version": "1.0.0", "main": "src/index.js",
  "scripts": { "test": "jest --coverage" },
  "dependencies": { "express": "^4", "pg": "^8", "bcrypt": "^5", "jsonwebtoken": "^9", "dotenv": "^16" },
  "devDependencies": { "jest": "^29", "supertest": "^6" } }
EOF
npm install
git add . && git commit -m "feat: minimal scaffold for testing" && git push origin main
```

---

## 6.1 Push Your Scaffold First

The background agent needs your scaffold in the remote repo to write tests against it.

```bash
git add .
git commit -m "feat: scaffold TaskFlow application"
git push origin main
```

---

## 6.2 Create the Testing Issue

> **CLI Command — Create Testing Issue** *(run in terminal)*

```bash
gh issue create \
  --title "Write unit and integration tests for TaskFlow MVP" \
  --body "The scaffolded TaskFlow app is in src/. 
Write tests in tests/ using Jest.

Required test coverage:
1. tests/unit/user.model.test.js — createUser, findUserByEmail (mock pg Pool)
2. tests/unit/task.model.test.js — createTask, getTasks, updateTaskStatus
3. tests/integration/auth.routes.test.js — POST /auth/register, POST /auth/login (happy path + validation errors)
4. tests/integration/tasks.routes.test.js — CRUD operations on /tasks with JWT auth header

Setup:
- Add jest and supertest to package.json devDependencies
- Add test script: 'jest --coverage' in package.json
- Add jest.config.js if needed

All tests must pass. Target: >80% coverage on model files." \
  --label "copilot"
```

Note the issue number (e.g. `#2`).

---

## 6.3 Assign to Copilot

**Option A — GitHub UI:**
1. Open issue `#2` on GitHub.com
2. Assignees → gear → select **Copilot**

**Option B — Copilot Chat:**

> **Chat Prompt — Assign to Copilot** *(paste into Copilot Chat)*

```
@github Assign issue #2 to Copilot to write the test suite.
```

---

## 6.4 Continue Working While Agent Runs

While the agent generates tests (~5-8 min), go back to VS Code and add a route stub so the integration tests have something to hit:

In Copilot Chat (default agent):

> **Chat Prompt — Add Register Route** *(paste into Copilot Chat, no specific agent)*

```
Add a POST /auth/register route in src/routes/auth.js that:
- Accepts { email, password } 
- Validates both fields are present
- Returns 400 if missing, 201 with { id, email } on success
```

---

## 6.5 Pull and Run Tests

**1.** Check if the PR is ready:

```bash
gh pr list
```

**2.** Pull the tests branch and merge:

```bash
gh pr view <pr-number>
gh pr merge <pr-number> --squash
git pull origin main
```

**3.** Install test dependencies and run:

```bash
npm install
npm test
```

**4.** Verify:

```
PASS  tests/unit/user.model.test.js
PASS  tests/unit/task.model.test.js
PASS  tests/integration/auth.routes.test.js

Coverage: Statements > 80%
```

---

## 🐛 Debug: Tests Fail After Merge

### Step 1 — Read the failure

Select the full Jest failure output in the terminal, then open Copilot Chat:

> **Chat Prompt — Debug Test Failure** *(paste into Copilot Chat after selecting terminal output)*

```
#terminalSelection

Debug this Jest failure following the project's debugging instructions in copilot-instructions.md.
```

> Custom instructions activate automatically. Copilot will quote the failing line, give the root cause in one sentence, and show a minimal fix — not a full test rewrite.

### Step 2 — Common failures table

| Failure | Root cause | Minimal fix |
|---------|-----------|-------------|
| `Cannot find module '../config/db'` | Wrong import path in test | Change `../config/db` to `../../src/config/db` |
| `pool.query is not a function` | pg Pool mock missing | Ask Copilot Chat: *Fix the pg mock in [test file]* |
| `401 Unauthorized` in integration test | JWT secret not set | Add `process.env.JWT_SECRET = 'test'` in test file |
| `ECONNREFUSED 127.0.0.1:5432` | Real DB called in unit test | Replace pg import with `jest.mock('../../src/config/db')` |
| Expected 201 received 500 | Route not implemented | Ask Copilot Chat: *Implement POST /auth/register in src/routes/auth.js* |

### Step 3 — If the test itself is wrong

> **Chat Prompt — Clarify Test vs Implementation** *(paste into Copilot Chat)*

```
The test in tests/integration/auth.routes.test.js line [N] expects [X] but the implementation
correctly returns [Y]. Is the test wrong or the implementation? Show the minimal fix for
whichever is incorrect.
```

---

## What You Built

| Artifact | Location |
|----------|----------|
| Unit tests | `tests/unit/` |
| Integration tests | `tests/integration/` |
| Test config | `jest.config.js` |
| Coverage report | `coverage/lcov-report/` |

**Background agent strength:** It wrote 4 test files with mocks, fixtures, and coverage config autonomously while you implemented routes.

---

---

| | Navigation |
|---|---|
| **Produces** | `tests/` suite — unit + integration tests, coverage report; consumed by Exercise 07 |
| **← Previous** | [Exercise 05: Scaffold + Debug](exercise-05-scaffold-cli.md) |
| **Next →** | [Exercise 07: Quality Gate →](exercise-07-quality-gate-cli.md) *(Optional)* |
| **Done?** | All mandatory exercises complete — review `docs/` for your full SDLC chain |

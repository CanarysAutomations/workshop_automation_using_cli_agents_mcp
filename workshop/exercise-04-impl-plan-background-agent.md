# Exercise 04: Generate Copilot Custom Instructions

| | Exercise 04 Overview |
|---|---|
| **Time** | ~7 minutes |
| **Copilot Feature** | Local Custom Agent (`sdlc-agent`) + Custom Instructions |
| **Type** | 🔴 Mandatory |
| **You Will** | Read BRD + FRD + TSD with `sdlc-agent` and generate `.github/copilot-instructions.md` — stack-specific coding standards, a 7-step debug protocol, and test debugging rules |
| **Input** | `docs/BRD.md`, `docs/FRD.md`, `docs/TSD.md` |
| **Output** | `.github/copilot-instructions.md` (active globally for all remaining exercises) |
| **Next** | [Exercise 05: Create GitHub Issue via MCP →](exercise-05-scaffold-cli.md) |

## Workshop Progress

> [01 BRD](exercise-01-brd-custom-agent.md) → [02 FRD](exercise-02-frd-agent-skills.md) → [03 TSD](exercise-03-tsd-cloud-agent.md) → `04 Instructions` → [05 Scaffold](exercise-05-scaffold-cli.md) → [06 Tests](exercise-06-tests-background-agent.md) → [07 Gate ⚪](exercise-07-quality-gate-cli.md)

---

## Goal

Use the `sdlc-agent` to read your three SDLC documents and **generate `.github/copilot-instructions.md`** — a project-specific context file that teaches Copilot your chosen stack, coding standards, debugging rules, and test expectations.

> **Why this matters:** Once this file exists, every Copilot prompt in this repo automatically inherits your project's rules. The GitHub issue, scaffolding, and test debugging exercises all benefit from it.

---

## ⚡ Starting Here?

If you skipped Exercises 01–03, generate a minimal context block:

```
Stack: Node.js + Express + PostgreSQL + JWT (or Python + FastAPI if you chose that)
Core entities: User, Team, Project, Task
Key NFRs: p95 < 300ms, 99.5% uptime, bcrypt passwords, JWT auth
```

Paste that block directly into step 4.2 in place of the file references.

---

## 4.1 What Is `.github/copilot-instructions.md`?

This file is read automatically by GitHub Copilot in **every chat and inline suggestion** in your repo. It is your "standing briefing" — Copilot always knows:
- What the product is
- Which stack and libraries you use
- How to format errors and fixes
- What test patterns to follow

The placeholder is already present in this repo. You will now overwrite it with your generated instructions.

---

## 4.2 Generate the Instructions File

**1.** Open **Copilot Chat** → select **sdlc-agent** from the agent dropdown.

**2.** Copy and paste this prompt:

> **Prompt — Generate Copilot Instructions** *(paste into Copilot Chat with sdlc-agent selected)*

```
Read #file:docs/BRD.md, #file:docs/FRD.md, and #file:docs/TSD.md.

Generate .github/copilot-instructions.md with these sections:

### 1. Project Context
- Product name, one-sentence description
- Tech stack with library versions (from TSD section 2)
- Key file paths and their purpose (src/, tests/, docs/)

### 2. Coding Standards
- Language and framework conventions for the chosen stack
- Error handling pattern (try/catch + next(err) for Express; HTTPException for FastAPI)
- HTTP status codes to use for each error type
- No hardcoding secrets — always read from process.env / environment variables

### 3. Debugging Protocol
When I share an error or stack trace:
1. Quote the exact file and line that triggered it
2. State the root cause in one sentence
3. Show the minimal fix — do not rewrite unrelated code
4. Explain why the bug occurred in 1–2 sentences
5. If missing module: give the exact install command
6. If DB connection error: check the config file and .env
7. If auth error: check the Authorization header format

### 4. Test Debugging
When a test fails:
1. Quote the Expected vs Received diff
2. State whether the test or the implementation is wrong
3. Fix whichever is wrong — not both unless both are incorrect
4. If Cannot find module: give the corrected relative import path

### 5. PR Review Behaviour
- Flag hardcoded secrets, missing input validation, or unguarded routes
- Suggest the inline fix, not just a comment
- Verify error responses use consistent shape: { "error": "message" }

Overwrite the placeholder in .github/copilot-instructions.md.
```

**3.** Open `.github/copilot-instructions.md`. Verify:
- [ ] Project Context section includes the stack from your TSD (not the wrong one)
- [ ] Debugging Protocol has the 7-step numbered list
- [ ] Test Debugging section describes Expected vs Received diff handling
- [ ] PR Review mentions `{ "error": "message" }` response shape

---

## 4.3 Activate and Test the Instructions

**1.** Save `.github/copilot-instructions.md`.

**2.** Reload VS Code: `Ctrl+Shift+P` → **Developer: Reload Window**.

**3.** Open Copilot Chat (no specific agent) and type:

```
What are the debugging instructions for this project?
```

> **Expected:** Copilot recites the 7-step debugging protocol from the file.  
> **If blank:** Open the file, confirm content is there, reload again.

---

## 🐛 Debug: Instructions Not Applied

If Copilot doesn't reflect your project rules:

```
Read #file:.github/copilot-instructions.md and summarise 
the debugging and error handling rules in 5 bullet points.
```

If the file still shows the placeholder → re-run step 4.2 using the inline context from ⚡ Starting Here.

If the instructions reference the wrong stack:

```
The instructions reference [wrong stack]. 
Read #file:docs/TSD.md section 2 and update the Project Context and Coding Standards 
sections of .github/copilot-instructions.md to use the correct stack.
```

---

## What You Built

| Artifact | Location |
|----------|----------|
| `.github/copilot-instructions.md` | Generated — you own this file |
| Active project briefing | Applied to all Copilot interactions in this repo from this point forward |

---

| | Navigation |
|---|---|
| **Produces** | `.github/copilot-instructions.md` — active context for all following exercises |
| **← Previous** | [Exercise 03: Technical Specification](exercise-03-tsd-cloud-agent.md) |
| **Next →** | [Exercise 05: Create GitHub Issue via MCP →](exercise-05-scaffold-cli.md) |
# AI-Driven SDLC: From Idea to Tested Code in 75 Minutes

> **Greenfield Challenge:** Build TaskFlow — a project management SaaS — end-to-end using GitHub Copilot's full AI feature suite.

## The Scenario

**Day 0. You have a funded idea.** TaskFlow is a task and project tracking tool for small engineering teams. No code exists. No specs exist. Nothing.

Your challenge: Go from a raw idea → BRD → FRD → TSD → Implementation Plan → Scaffolded Code → Tested Application in a single 75-minute session using GitHub Copilot's agent ecosystem.

> 📄 **Your starting point:** [`docs/REQUIREMENTS.md`](docs/REQUIREMENTS.md) — TaskFlow's signed-off product brief. Open it before Exercise 01. Every artifact in this workshop derives from it.

---

## What You'll Learn

| Copilot Feature | When You Use It | Exercise |
|-----------------|-----------------|----------|
| **Local Custom Agent** | `sdlc-agent` generates BRD, FRD, TSD, and Copilot Instructions from your local docs | EX-01, 02, 03, 04 |
| **Agent Skills** | `frd-writer` skill structures the FRD with Feature IDs, API contracts, and data models | EX-02 |
| **Custom Instructions** | `.github/copilot-instructions.md` teaches Copilot your stack, debug rules, and test patterns | EX-04 onwards |
| **Copilot CLI** | `gh copilot suggest` scaffolds the project from the terminal; explains and fixes every failure | EX-05, 07 |
| **Background Agent** | Copilot coding agent writes the full test suite autonomously and opens a PR | EX-06 |

---

## Prerequisites

> Complete **all steps below before the workshop starts.** Each step has a verification command — run it to confirm the tool is ready.

---

### Step 1 — VS Code + GitHub Copilot Extension

1. Install [Visual Studio Code](https://code.visualstudio.com/download)
2. Open VS Code → Extensions (`Ctrl+Shift+X`) → search **GitHub Copilot** → Install
3. Sign in with your GitHub account when prompted

**Verify:**
```
VS Code → Extensions → GitHub Copilot → Status shows "Enabled"
```

> **Subscription required:** Individual, Business, or Enterprise. [Start a free trial](https://github.com/features/copilot) if needed.

---

### Step 2 — Git

| OS | Install |
|----|---------|
| Windows | [git-scm.com/download/win](https://git-scm.com/download/win) |
| macOS | `brew install git` or Xcode Command Line Tools |
| Linux | `sudo apt install git` |

**Verify:**
```bash
git --version
# Expected: git version 2.x.x
```

---

### Step 3 — Node.js 20+

Download from [nodejs.org](https://nodejs.org/) — choose the **LTS** version.

**Verify:**
```bash
node --version   # Expected: v20.x.x or higher
npm --version    # Expected: 10.x.x or higher
```

---

### Step 4 — GitHub CLI (`gh`)

| OS | Install |
|----|---------|
| Windows | `winget install GitHub.cli` |
| macOS | `brew install gh` |
| Linux | [cli.github.com/manual/installation](https://cli.github.com/manual/installation) |

After install, authenticate:
```bash
gh auth login
# Choose: GitHub.com → HTTPS → Login with a web browser
```

**Verify:**
```bash
gh auth status
# Expected: Logged in to github.com as <your-username>
```

---

### Step 5 — GitHub Copilot CLI Extension

Install after Step 4 is complete:

```bash
gh extension install github/gh-copilot
```

**Verify:**
```bash
gh copilot --version
# Expected: gh copilot version x.x.x
```

> Used in **Exercise 05** (scaffold) and **Exercise 07** (quality gate).

---

### Step 6 — GitHub MCP Server *(for `@github` cloud agent)*

The MCP server lets `@github` read your repository from inside VS Code's Copilot Chat.

1. Follow the [setup guide](https://github.com/github/github-mcp-server?tab=readme-ov-file)
2. Restart VS Code after configuration

**Verify:**
```
Open Copilot Chat → type @github hello → it should respond with repo context
```

> Used in **Exercise 03** (TSD with full repo read).

---

### Step 7 — Model Selection

> **Recommended: `claude-sonnet-4-6`**

This workshop generates long documents (BRD, FRD, TSD), multi-file scaffolds, and runs iterative debugging. Both models handle all exercises reliably.

| Model | All Exercises | Best For | Avoid When |
|-------|:---:|---------|------------|
| `claude-sonnet-4-5` ✅ | ✅ | Document generation, code scaffold | — |
| `gpt-4o` ✅ | ✅ | CLI tasks, structured JSON output | — |
| `gpt-4o-mini` ⚠️ | ❌ | Quick answers only | Long doc exercises (EX-01–03) |
| `o1` ⚠️ | ❌ | Reasoning-only tasks | Doc writing, speed-sensitive tasks |

**To set the model:** Copilot Chat → model picker (top of chat panel) → select `claude-sonnet-4-5`.

---

### Pre-Workshop Checklist

Run this to confirm everything is ready:

```bash
git --version && echo "✅ Git OK"
node --version && echo "✅ Node OK"
gh auth status && echo "✅ gh CLI OK"
gh copilot --version && echo "✅ Copilot CLI OK"
```

All four lines should print ✅. If any fail, revisit the step above.

---

## Clone & Setup

```bash
# 1. Clone
git clone https://github.com/<your-org>/ai-sdlc-end-to-end.git
cd ai-sdlc-end-to-end

# 2. Copy environment template
cp .env.example .env

# 3. Confirm prerequisites
git --version && node --version && gh copilot --version
```

> **First thing to open:** [docs/REQUIREMENTS.md](docs/REQUIREMENTS.md) — TaskFlow's signed-off product brief. Every exercise derives from it.  
> **All exercises are independent.** Each has a ⚡ *Starting Here?* section so you can enter at any point.

---

## Workshop Exercises

| # | Exercise | Copilot Feature | Type | Time | Produces |
|---|----------|-----------------|------|------|----------|
| 1 | [EX-01: Business Requirements](workshop/exercise-01-brd-custom-agent.md) | Local Custom Agent (`sdlc-agent`) | 🔴 Mandatory | ~8 min | `docs/BRD.md` |
| 2 | [EX-02: Functional Requirements](workshop/exercise-02-frd-agent-skills.md) | Agent Skills + Local Custom Agent | 🔴 Mandatory | ~8 min | `docs/FRD.md` |
| 3 | [EX-03: Technical Spec + Stack Decision](workshop/exercise-03-tsd-cloud-agent.md) | Local Custom Agent | 🔴 Mandatory | ~9 min | `docs/TSD.md` |
| 4 | [EX-04: Generate Copilot Instructions](workshop/exercise-04-impl-plan-background-agent.md) | Local Custom Agent + Custom Instructions | 🔴 Mandatory | ~7 min | `.github/copilot-instructions.md` |
| 5 | [EX-05: Scaffold with Copilot CLI](workshop/exercise-05-scaffold-cli.md) | Copilot CLI | 🔴 Mandatory | ~12 min | `src/` project scaffold |
| 6 | [EX-06: Generate & Run Tests](workshop/exercise-06-tests-background-agent.md) | Background Agent | 🔴 Mandatory | ~11 min | `tests/` suite, passing tests |
| 7 | [EX-07: Quality Gate](workshop/exercise-07-quality-gate-cli.md) | Copilot CLI | ⏴ Optional | ~10 min | `quality-gate.sh` |

**Mandatory: ~55 min │ Optional: ~10 min │ Buffer: ~10 min │ Total: 75 min**

---

## SDLC Flow

```
REQUIREMENTS.md  ← your starting point
  ↓
EX-01  BRD     ← sdlc-agent reads REQUIREMENTS.md  →  docs/BRD.md
  ↓
EX-02  FRD     ← sdlc-agent + frd-writer skill       →  docs/FRD.md
  ↓
EX-03  TSD     ← sdlc-agent + YOUR stack choice      →  docs/TSD.md
  ↓
EX-04  Instructions  ← sdlc-agent reads BRD+FRD+TSD  →  .github/copilot-instructions.md
  ↓  (custom instructions active from here onwards)
EX-05  Scaffold      ← Copilot CLI                    →  src/ project tree
  ↓
EX-06  Tests         ← Background Agent (async PR)    →  tests/ + passing suite
  ↓
EX-07  Quality Gate  ← Copilot CLI  ◄ Optional
```

---

## Get Started → [Exercise 01](workshop/exercise-01-brd-custom-agent.md)

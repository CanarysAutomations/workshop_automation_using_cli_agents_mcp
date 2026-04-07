# Exercise 01 — Install GitHub CLI & Authenticate

> **Duration:** 10 minutes | **Feature:** GitHub CLI | **Goal:** Install the GitHub CLI, authenticate with your GitHub account, and install the GitHub Copilot CLI extension so every subsequent exercise can use the `copilot` command.

---

## Background

The GitHub CLI (`gh`) is the foundation of this workshop. Every Copilot CLI command, repository operation, and workflow query runs through it. This exercise gets it installed, authenticated, and extended with Copilot before any application code is touched.

---

## Prerequisites

- [Python 3.11+](https://www.python.org/downloads/) on `PATH`
- [Git](https://git-scm.com/install/) installed
- Active GitHub account with GitHub Copilot access

---

## Step 1 — Install GitHub CLI

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

> **Already installed?** Run `winget upgrade --id GitHub.cli` (Windows) or `brew upgrade gh` (macOS) to update.

---

## Step 2 — Authenticate with GitHub CLI

```cmd
gh auth login
```

Follow the prompts:
1. Select **GitHub.com**
2. Choose **HTTPS** as the protocol
3. Authenticate via browser — paste the one-time code shown at `github.com/login/device`
4. Authorise **GitHub CLI** when prompted

Verify:

```cmd
gh auth status
```

Expected: `✓ Logged in to github.com as <your-username>`

---

## Step 3 — Install the GitHub Copilot CLI Extension

```cmd
gh extension install github/gh-copilot
gh copilot --version
```

Test with a quick session:

```cmd
copilot
```

Type `Hello` and press Enter — you should receive an AI response. Type `exit` to close.

> **Note:** If `copilot` is not recognised as a standalone command, use `gh copilot chat` wherever this workshop writes `copilot`.

---

## Key Takeaways

- `gh auth login` authenticates all subsequent `gh` and `copilot` commands.
- `gh extension install github/gh-copilot` adds the `copilot` command to your shell.
- Run `gh auth status` any time you suspect your session has expired.

> **Next:** [Exercise 02 — Clone Repository & Set Up the Python Environment](EXERCISE_02_SETUP_ENVIRONMENT.md)

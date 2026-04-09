# Exercise 11 — Build the PR Summarizer Agent with Copilot SDK

> **Duration:** 15 minutes | **Feature:** Copilot SDK + GitHub API | **Goal:** Create the directory structure, install SDK dependencies, configure environment variables, and generate the four Python modules that make up the PR summarizer agent using Copilot Chat prompts.

---

## Background

The Copilot SDK lets you drive AI analysis from Python code. This exercise builds a four-module agent that fetches pull request diffs from GitHub, sends them to the Copilot model for analysis, and posts a structured summary comment on the PR. The modules are generated with Copilot — you write prompts, not code.

---

## Prerequisites

- Completed [Exercise 10 — Review the Self-Healing PR & Verify Recovery](EXERCISE_10_REVIEW_AND_MERGE.md)
- At least one PR exists in your repository (the self-healing PR is ideal)
- Python 3.11+ with `.venv` active
- A GitHub Personal Access Token with `repo` and `pull_requests` scopes

---

## Step 1 — Create the Agent Directory

```powershell
mkdir agents\pr_summarizer
```

---

## Step 2 — Install Dependencies

Create `agents/pr_summarizer/requirements-agent.txt`:

```
copilot-sdk>=0.1.0
PyGithub>=2.1.1
python-dotenv>=1.0.0
pydantic-settings>=2.0.0
openai>=1.0.0
rich>=13.0.0
```

```powershell
pip install -r agents\pr_summarizer\requirements-agent.txt
```

---

## Step 3 — Configure Environment Variables

Create `agents/pr_summarizer/.env` (add to `.gitignore`):

```env
GITHUB_TOKEN=ghp_your_token_here
GITHUB_REPOSITORY=CanarysPlayground/Help_Desk_Application
OPENAI_API_KEY=your_key_here
COPILOT_MODEL=gpt-4
```

---

## Step 4 — Generate the Four Modules with Copilot Chat

Open VS Code Copilot Chat (`Ctrl+Alt+I`) and generate each file using these prompts:

**`config.py`**
```
Create a Pydantic BaseSettings class loading GITHUB_TOKEN, GITHUB_REPOSITORY,
OPENAI_API_KEY, COPILOT_MODEL from environment variables via python-dotenv.
```

**`copilot_analyzer.py`**
```
Create a CopilotAnalyzer class using the OpenAI client. Accept PR metadata
and file diffs, build a structured prompt, call the API, return Markdown
covering: purpose, key changes, risk areas, review focus.
```

**`github_integration.py`**
```
Create a GitHubClient using PyGithub: fetch PR metadata and file diffs for a
PR number; post a comment, editing existing bot comment if present.
```

**`agent.py`**
```
Create agent.py: parse --repo and --pr-number CLI args, fetch PR details via
GitHubClient, analyse with CopilotAnalyzer, post the summary comment.
Include __main__ guard.
```

Save each file to `agents/pr_summarizer/`.

---

## Key Takeaways

- The four modules follow single-responsibility: config loads env, github_integration fetches data, copilot_analyzer reasons, agent orchestrates.
- Generating each module separately with a focused prompt produces cleaner, more reviewable code than one large prompt.
- Add `agents/pr_summarizer/.env` to `.gitignore` immediately — never commit API keys.

> **Next:** [Exercise 12 — Test the Agent Locally & Automate with GitHub Actions](EXERCISE_12_AUTOMATE_PR_SUMMARY.md)

# Exercise 05 — PR Summarizer with Copilot SDK

> **Duration:** 30 minutes &nbsp;|&nbsp; **Copilot Feature:** Copilot SDK + GitHub API &nbsp;|&nbsp; **Goal:** Build a Python AI agent using the GitHub Copilot SDK that automatically fetches pull request details, analyses the changes with AI, and posts a human-readable summary as a PR comment — then automate it with GitHub Actions.

---

## Background

Pull request reviews are a bottleneck in many teams. A reviewer must read every changed file to understand the intent of a PR before they can give useful feedback. An AI-powered PR summarizer can reduce this burden by generating a concise, structured summary the moment a PR is opened.

In this exercise you will use the **GitHub Copilot SDK** to build a Python agent that:
1. Fetches PR metadata and file diffs from the GitHub API.
2. Sends the context to the Copilot AI model for analysis.
3. Posts a formatted summary comment directly on the pull request.
4. Runs automatically on every new PR via a GitHub Actions workflow.

The self-healing PR from Exercise 04 is the ideal first test target.

---

## What You Will Learn

1. How to install and configure the GitHub Copilot SDK in a Python project.
2. How to structure a multi-file AI agent with clear separation of concerns.
3. How to use Copilot prompts inside Python code to drive AI analysis.
4. How to wire a Python agent to GitHub Actions for continuous automation.

---

## Prerequisites

- Completed [Exercise 04 — Self-Healing Workflow](EXERCISE_4_SELF_HEALING.md)
- At least one open or recently merged PR in your repository (the self-healing PR from Ex 04 is ideal)
- Python 3.11+ with `.venv` active
- A GitHub Personal Access Token with `repo` and `pull_requests` scopes
- `GITHUB_TOKEN` and `OPENAI_API_KEY` (or GitHub Copilot API access) available as environment variables

---

## Step 1 — Create the Agent Directory Structure

```powershell
cd Help_Desk_Application
mkdir agents\pr_summarizer
```

Your agent will follow the same single-responsibility module pattern as the application itself.

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

Install them:

```powershell
pip install -r agents\pr_summarizer\requirements-agent.txt
```

---

## Step 3 — Configure Environment Variables

Create `agents/pr_summarizer/.env` (this file must not be committed — add it to `.gitignore`):

```env
GITHUB_TOKEN=ghp_your_token_here
GITHUB_REPOSITORY=CanarysPlayground/Help_Desk_Application
OPENAI_API_KEY=your_openai_or_copilot_api_key_here
COPILOT_MODEL=gpt-4
```

---

## Step 4 — Build the Agent Modules with Copilot

Open VS Code and use Copilot Chat to generate each module. Use the prompts below — copy each prompt into Copilot Chat's agent mode and save the generated file.

### Module 1 — `config.py`

```
Create a Pydantic BaseSettings class in config.py that loads GITHUB_TOKEN,
GITHUB_REPOSITORY, OPENAI_API_KEY, and COPILOT_MODEL from environment variables.
Use python-dotenv to load a .env file automatically.
```

Save as `agents/pr_summarizer/config.py`.

### Module 2 — `copilot_analyzer.py`

```
Create a CopilotAnalyzer class in copilot_analyzer.py that uses the OpenAI client
to analyse PR changes. It should accept a dictionary of PR metadata and file diffs,
build a structured prompt, call the Copilot/OpenAI API, and return a Markdown-formatted
summary covering: purpose, key changes per file, risk areas, and suggested review focus.
```

Save as `agents/pr_summarizer/copilot_analyzer.py`.

### Module 3 — `github_integration.py`

```
Create a GitHubClient class in github_integration.py using PyGithub that can:
1. Fetch PR metadata (title, author, description, labels) for a given PR number
2. Retrieve the list of changed files and their diffs
3. Post a comment to a PR; if an existing bot comment is present, edit it instead of creating a new one
```

Save as `agents/pr_summarizer/github_integration.py`.

### Module 4 — `agent.py` (main entry point)

```
Create agent.py as the main entry point that:
1. Parses --repo and --pr-number from command-line arguments
2. Uses GitHubClient to fetch PR details and diffs
3. Passes the data to CopilotAnalyzer to generate a summary
4. Posts the summary comment to the PR via GitHubClient
5. Prints a success message with the PR URL
Include a __main__ guard.
```

Save as `agents/pr_summarizer/agent.py`.

---

## Step 5 — Test the Agent Locally

Point the agent at the self-healing PR from Exercise 04 (replace `XX` with the actual PR number):

```powershell
python agents\pr_summarizer\agent.py --repo CanarysPlayground/Help_Desk_Application --pr-number XX
```

Expected output:

```
Fetching PR #XX from CanarysPlayground/Help_Desk_Application...
Analysing 1 changed file(s) with Copilot...
Posting summary comment to PR #XX...
Done. View the comment at: https://github.com/CanarysPlayground/Help_Desk_Application/pull/XX
```

Navigate to the PR in your browser and confirm the AI summary comment appears.

---

## Step 6 — Automate with GitHub Actions

Create `.github/workflows/copilot-pr-summarizer.yml`. Use this Copilot prompt to generate it:

```
Create a GitHub Actions workflow that triggers when a pull request is opened or updated.
It should:
1. Check out the repository
2. Set up Python 3.11
3. Install dependencies from agents/pr_summarizer/requirements-agent.txt
4. Run agents/pr_summarizer/agent.py with the PR number from the event context
Use repository secrets GITHUB_TOKEN and OPENAI_API_KEY for authentication.
```

Commit and push the workflow:

```cmd
git add .github/workflows/copilot-pr-summarizer.yml agents/pr_summarizer/
git commit -m "feat: add Copilot SDK PR summarizer agent and workflow"
git push origin main
```

Open a new pull request in your repository to verify the agent posts a summary automatically.

---

## Key Takeaways

- The Copilot SDK separates concern cleanly: `github_integration.py` handles data retrieval, `copilot_analyzer.py` handles AI reasoning, and `agent.py` orchestrates both.
- Building the agent interactively with Copilot Chat (generating each module from a prompt) is faster and produces better-structured code than writing it from scratch.
- Posting AI summaries as editable comments (update if bot comment exists) avoids PR thread clutter on repeated runs.
- A GitHub Actions trigger on `pull_request` (opened, synchronize) ensures every PR gets summarised as soon as it is created or updated.

> **Well done — you have completed the core track!**
>
> **Optional:** Continue to [Exercise 06 — Debugging with GitHub Copilot](EXERCISE_6_DEBUGGING.md) to see how `gh copilot explain`, `gh copilot suggest`, `@terminal`, and VS Code Inline Chat work together to diagnose and fix a live runtime bug.
>
> Return to the [Workshop README](Readme.md) for next steps and further learning resources.

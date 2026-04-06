# Exercise 03 — Build CI/CD Workflows

> **Duration:** 30 minutes &nbsp;|&nbsp; **Copilot Feature:** GitHub Actions + Copilot CLI &nbsp;|&nbsp; **Goal:** Use the custom agent to generate a full set of GitHub Actions workflow YAML files — CI, CD, issue automation, and a self-healing workflow — then commit and trigger them.

---

## Background

Manually maintaining GitHub Actions YAML is tedious and error-prone. Copilot CLI can generate complete, production-quality workflow files from a plain-language description of your requirements. In this exercise you will generate four workflows that automate the entire lifecycle of the Help Desk CRM: testing, deployment, issue triage, and automatic recovery from broken builds.

The **self-healing workflow** you create here is the focus of Exercise 04. It watches for failed CI runs, identifies the root cause, applies a fix, and opens a PR — all without human intervention.

---

## What You Will Learn

1. How to generate GitHub Actions YAML with Copilot CLI prompts.
2. How to create CI, CD, issue automation, and self-healing workflows.
3. How to commit and push workflows so GitHub Actions picks them up.
4. How to introduce a deliberate build failure to trigger self-healing.

---

## Prerequisites

- Completed [Exercise 02 — Plan & Implement Feature](EXERCISE_2_PLAN_ASSIGN_FEATURE.md)
- Repository pushed to GitHub (the workflows folder must be in `.github/workflows/`)
- `helpdesk-crm-agent` active in Copilot CLI
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Create the `.github/workflows` Directory

```cmd
mkdir .github\workflows
```

---

## Step 2 — Generate the CI Workflow

Start a Copilot CLI session:

```cmd
copilot
```

Prompt the agent:

```
@helpdesk-crm-agent

Generate a GitHub Actions CI workflow YAML file for the Helpdesk CRM FastAPI application.

Requirements:
- Trigger: push to main and all feature branches; pull_request to main
- Python 3.11
- Install dependencies from requirements.txt
- Run pytest with coverage report
- Run flake8 for linting
- Cache pip dependencies to speed up runs
- Upload coverage report as an artifact

Output the complete YAML. Save it as .github/workflows/ci.yml
```

Save the generated content to `.github/workflows/ci.yml`.

---

## Step 3 — Generate the CD Workflow

```
@helpdesk-crm-agent

Generate a GitHub Actions CD workflow for deploying the Helpdesk CRM.

Requirements:
- Trigger: push to main only, runs after CI passes (use `needs: ci`)
- Build a Docker image
- Push the image to GitHub Container Registry (ghcr.io)
- Include an optional deploy step to Azure App Service using a repository secret
- Send a notification comment on the PR when deployment succeeds or fails

Output the complete YAML. Save it as .github/workflows/cd.yml
```

Save the generated content to `.github/workflows/cd.yml`.

---

## Step 4 — Generate the Issue Automation Workflow

```
@helpdesk-crm-agent

Generate a GitHub Actions workflow for issue automation.

Requirements:
- Trigger: when an issue is opened or a label is added
- Auto-assign based on label:
    - label "bug" → assign to developers team
    - label "docs" → assign to tech-writers team
    - label "infra" → assign to devops team
- Automatically add a "priority:high" label if the issue title contains the words "critical" or "urgent"
- Post an acknowledgment comment when the issue is opened

Output the complete YAML. Save it as .github/workflows/issue-automation.yml
```

Save the generated content to `.github/workflows/issue-automation.yml`.

---

## Step 5 — Generate the Self-Healing Workflow

This is the most important workflow in this exercise. It listens for CI failures, analyses the failing run, applies an automated fix, and opens a pull request.

```
@helpdesk-crm-agent

Generate a GitHub Actions self-healing workflow for the Helpdesk CRM.

Requirements:
- Trigger: on workflow_run completed for the "CI" workflow, only when conclusion is "failure"
- Steps:
    1. Check out the repository
    2. Set up Python 3.11
    3. Detect missing packages by scanning all Python files for import statements not present in requirements.txt
    4. Add any missing packages (with pinned version ranges) to requirements.txt
    5. Run isort and black to fix formatting
    6. Run the test suite; only proceed if tests pass after the fix
    7. Create a new branch named self-healing/auto-fix-{run_id}
    8. Commit the changes with message "fix: auto-heal — add missing dependencies and fix formatting"
    9. Open a pull request with label "self-healing" and "automated" targeting the default branch
- Use the GITHUB_TOKEN for all GitHub API operations

Output the complete YAML. Save it as .github/workflows/self-healing.yml
```

Save the generated content to `.github/workflows/self-healing.yml`.

---

## Step 6 — Commit and Push the Workflows

```cmd
git add .github/workflows/
git commit -m "ci: add CI, CD, issue automation, and self-healing workflows"
git push origin main
```

Open the **Actions** tab in your GitHub repository and confirm all four workflow files appear. The CI workflow should trigger immediately on the push.

---

## Step 7 — Introduce a Deliberate Build Failure

To demonstrate self-healing in Exercise 04, you need to break the build.

Open `app/main.py` in VS Code:

```powershell
code app/main.py
```

Add the following import at the top of the file (after the existing imports):

```python
import requests  # intentional: package not in requirements.txt
```

If `requests` is already installed, uninstall it so the CI run fails:

```powershell
pip uninstall requests -y
```

Commit and push the change:

```cmd
git add app/main.py
git commit -m "test: introduce missing dependency to trigger self-healing"
git push origin main
```

Navigate to the **Actions** tab and watch the CI workflow fail. The self-healing workflow should trigger automatically within a minute.

---

## Key Takeaways

- Copilot CLI can generate production-quality GitHub Actions YAML from a plain-language description — no need to remember every action name or syntax.
- Always review generated YAML before committing: check triggers, environment variable names, and secret references.
- The self-healing workflow pattern (`workflow_run` trigger on failure) is broadly applicable — adapt it to any language or framework.
- A deliberate failure is the most reliable way to verify your self-healing pipeline before relying on it in production.

> **Next:** [Exercise 04 — Self-Healing Workflow in Action](EXERCISE_4_SELF_HEALING.md)

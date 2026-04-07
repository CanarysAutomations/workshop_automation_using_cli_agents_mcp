# Exercise 07 — Generate CI & CD Workflows

> **Duration:** 15 minutes | **Feature:** GitHub Actions + Copilot CLI | **Goal:** Use the custom agent to generate CI, CD, and issue automation workflow YAML files from plain-language prompts, then commit and push them to GitHub.

---

## Background

Copilot CLI can produce complete, production-ready GitHub Actions YAML from a description. This exercise generates three of the four workflows needed for the workshop — CI, CD, and issue automation. The self-healing workflow is covered in Exercise 08.

---

## Prerequisites

- Completed [Exercise 06 — Delegate Implementation & Review the PR](EXERCISE_06_DELEGATE_IMPLEMENTATION.md)
- Repository pushed to GitHub
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Create the Workflows Directory

```cmd
mkdir .github\workflows
copilot
```

---

## Step 2 — Generate the CI Workflow

```
@helpdesk-crm-agent

Generate a GitHub Actions CI workflow for the Helpdesk CRM FastAPI app.
- Trigger: push to main and feature branches; pull_request to main
- Python 3.11, install from requirements.txt
- Run pytest with coverage report; run flake8 for linting
- Cache pip dependencies; upload coverage as artifact
Save as .github/workflows/ci.yml
```

Save the output to `.github/workflows/ci.yml`.

---

## Step 3 — Generate the CD Workflow

```
@helpdesk-crm-agent

Generate a GitHub Actions CD workflow for the Helpdesk CRM.
- Trigger: push to main only, after CI passes (needs: ci)
- Build Docker image and push to GitHub Container Registry (ghcr.io)
- Optional deploy step to Azure App Service via repository secret
- Post a PR comment on success or failure
Save as .github/workflows/cd.yml
```

Save the output to `.github/workflows/cd.yml`.

---

## Step 4 — Generate the Issue Automation Workflow

```
@helpdesk-crm-agent

Generate a GitHub Actions issue automation workflow.
- Trigger: issue opened or label added
- Auto-assign: bug → developers; docs → tech-writers; infra → devops
- Add priority:high label if title contains "critical" or "urgent"
- Post an acknowledgment comment on open
Save as .github/workflows/issue-automation.yml
```

Save the output to `.github/workflows/issue-automation.yml`.

---

## Step 5 — Commit and Push

```cmd
git add .github/workflows/
git commit -m "ci: add CI, CD, and issue automation workflows"
git push origin main
```

Open the **Actions** tab in your browser — the CI workflow should trigger immediately.

---

## Key Takeaways

- Copilot generates correct trigger syntax, job names, and action versions — no need to memorise the Actions schema.
- Always review YAML before committing: check trigger branches, secret names, and runner images.
- The `needs: ci` key in CD ensures deployment never runs against a failing build.

> **Next:** [Exercise 08 — Generate Self-Healing Workflow & Trigger a Failure](EXERCISE_08_SELF_HEALING_SETUP.md)

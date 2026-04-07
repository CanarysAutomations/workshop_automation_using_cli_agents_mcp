# Exercise 08 — Generate Self-Healing Workflow & Trigger a Failure

> **Duration:** 15 minutes | **Feature:** GitHub Actions `workflow_run` trigger | **Goal:** Generate the self-healing workflow with Copilot CLI, commit it, then introduce a deliberate dependency failure to trigger it.

---

## Background

The self-healing workflow listens for CI failures, automatically detects the root cause (missing imports, bad formatting), applies a fix, verifies it with tests, and opens a PR — with no human intervention. This exercise sets up the workflow and deliberately breaks the build so you can observe it activate in Exercise 09.

---

## Prerequisites

- Completed [Exercise 07 — Generate CI & CD Workflows](EXERCISE_07_CI_CD_WORKFLOWS.md)
- CI workflow is live and green in the **Actions** tab
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Generate the Self-Healing Workflow

```cmd
copilot
```

```
@helpdesk-crm-agent

Generate a GitHub Actions self-healing workflow for the Helpdesk CRM.
- Trigger: workflow_run completed for "CI" workflow, only on failure conclusion
- Steps:
  1. Checkout repository, setup Python 3.11
  2. Scan all Python files for imports missing from requirements.txt
  3. Add missing packages with pinned version ranges to requirements.txt
  4. Run isort and black to fix formatting
  5. Run the test suite; abort if tests still fail
  6. Create branch self-healing/auto-fix-{run_id}
  7. Commit with message "fix: auto-heal — missing dependencies and formatting"
  8. Open a PR labelled "self-healing" and "automated" targeting main
- Use GITHUB_TOKEN for all API operations
Save as .github/workflows/self-healing.yml
```

Save the output to `.github/workflows/self-healing.yml`. Type `exit`.

---

## Step 2 — Commit the Self-Healing Workflow

```cmd
git add .github/workflows/self-healing.yml
git commit -m "ci: add self-healing workflow"
git push origin main
```

---

## Step 3 — Introduce a Deliberate Dependency Failure

```powershell
code app/main.py
```

Add after the existing imports:

```python
import requests  # intentional: not in requirements.txt
```

Uninstall `requests` locally so the test run also fails:

```powershell
pip uninstall requests -y
```

Commit and push:

```cmd
git add app/main.py
git commit -m "test: introduce missing dependency to trigger self-healing"
git push origin main
```

Open the **Actions** tab — the CI workflow should fail within a minute.

---

## Key Takeaways

- The `workflow_run` trigger (on `conclusion: failure`) is the correct decoupled pattern — the healing workflow doesn't need to be inside the CI workflow.
- A deliberate failure is the most reliable way to verify a self-healing pipeline before trusting it in production.
- Uninstalling `requests` locally ensures the test suite also fails, making the scenario realistic.

> **Next:** [Exercise 09 — Observe & Analyse the Self-Healing Workflow](EXERCISE_09_OBSERVE_SELF_HEALING.md)

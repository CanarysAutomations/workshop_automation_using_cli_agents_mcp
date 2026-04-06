# Exercise 04 — Self-Healing Workflow in Action

> **Duration:** 20 minutes &nbsp;|&nbsp; **Copilot Feature:** Self-Healing GitHub Actions + Copilot CLI &nbsp;|&nbsp; **Goal:** Observe the self-healing workflow detect the broken build from Exercise 03, apply an automated fix, and open a pull request — then use Copilot CLI to analyse and summarise what happened.

---

## Background

In Exercise 03 you introduced a deliberate dependency error (`import requests` without adding it to `requirements.txt`). This caused the CI workflow to fail. The self-healing workflow you generated is designed to respond to that exact scenario: it analyses the failing run, resolves the missing dependency, verifies the fix with tests, and opens a PR — all automatically.

In this exercise you will use Copilot CLI as an investigative tool: asking it to retrieve workflow logs, explain what was fixed, and surface the pull request for review.

---

## What You Will Learn

1. How to use Copilot CLI to query live GitHub Actions workflow status.
2. How to interpret self-healing workflow logs with natural language prompts.
3. How to inspect the auto-generated fix PR through Copilot CLI.
4. How to merge the self-healing PR and verify the build is green again.

---

## Prerequisites

- Completed [Exercise 03 — Build CI/CD Workflows](EXERCISE_3_BUILD_WORKFLOW.md)
- The deliberate `import requests` failure has been pushed to the repository
- The CI workflow has failed at least once in the **Actions** tab
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Confirm the CI Failure

Open a Copilot CLI session:

```cmd
copilot
```

Ask Copilot to check the latest workflow runs:

```
Show me the most recent workflow runs for this repository and identify any failed runs.
```

Copilot will call `gh run list` internally and display the run status. Confirm the CI workflow has a `failure` conclusion.

---

## Step 2 — Monitor the Self-Healing Workflow

```
Monitor the self-healing workflow that triggered after the CI failure and show me its current status.
```

Copilot will watch the `self-healing.yml` run in real time. You should see jobs progress through:

1. `checkout` — cloning the repository
2. `detect-issues` — scanning Python files for missing imports
3. `apply-fixes` — adding `requests` to `requirements.txt` and running formatters
4. `verify` — running the test suite against the fixed code
5. `create-pr` — pushing a branch and opening a pull request

> **Note:** Self-healing typically completes within 2–4 minutes of the CI failure. If the workflow has not triggered yet, wait a moment and re-run the prompt.

---

## Step 3 — Analyse What Was Fixed

```
Analyse the self-healing workflow logs and explain exactly what fixes were applied to the codebase.
```

Copilot will retrieve the workflow logs and produce a structured summary, for example:

```
Self-Healing Workflow Analysis
===============================

Issue Detected:
  Missing dependency: 'requests'
  Found in: app/main.py (import statement on line 8)
  Not present in: requirements.txt

Fixes Applied:
  1. Added requests>=2.28.0,<3.0.0 to requirements.txt
  2. Ran isort — import order corrected in app/main.py
  3. Ran black — no formatting changes required

Verification:
  All tests passed after the fix
  Coverage maintained

Pull Request:
  PR #XX: "fix: auto-heal — add missing dependencies and fix formatting"
  Branch: self-healing/auto-fix-{run_id} → main
  Files changed: requirements.txt (+1 line)
```

---

## Step 4 — Review the Self-Healing Pull Request

```
Show me the pull request created by the self-healing workflow, including the file diff.
```

Copilot will list the open PR, its labels (`self-healing`, `automated`), and the diff. Confirm that:

- Only `requirements.txt` was modified
- The correct version range was added
- No unrelated files were changed

Navigate to the PR in your browser to do a final visual inspection before merging.

---

## Step 5 — Merge the Pull Request and Verify Recovery

Merge the PR via the GitHub UI or from the terminal:

```cmd
gh pr merge --merge --subject "fix: restore build after self-healing fix"
```

After merging, watch the CI workflow trigger on `main`. Ask Copilot to confirm:

```
Check the latest CI run on main and confirm it passed.
```

Expected: `✓ CI workflow — success`

---

## Key Takeaways

- Self-healing workflows follow the pattern: **detect** (scan imports vs. requirements) → **fix** (update files) → **verify** (run tests) → **propose** (open PR).
- Copilot CLI acts as a natural-language layer over `gh` commands — you can query live workflow state, logs, and PRs without remembering API syntax.
- Always review the self-healing PR before merging, even in automated pipelines — the fix should touch only the broken file.
- The `workflow_run` trigger is the correct mechanism to respond to another workflow's failure without coupling the two workflows.

> **Next:** [Exercise 05 — PR Summarizer with Copilot SDK](EXERCISE_5_PRSUMMARY_SDK.md)

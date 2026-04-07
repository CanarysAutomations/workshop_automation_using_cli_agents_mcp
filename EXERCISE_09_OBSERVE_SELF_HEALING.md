# Exercise 09 — Observe & Analyse the Self-Healing Workflow

> **Duration:** 10 minutes | **Feature:** Copilot CLI + GitHub Actions logs | **Goal:** Use Copilot CLI as a natural-language interface to query the live CI failure, watch the self-healing workflow execute in real time, and understand exactly what it fixed.

---

## Background

Copilot CLI acts as a conversational layer over `gh run` commands. Rather than remembering `gh run list --workflow=self-healing.yml`, you describe what you want and Copilot translates it to the right command. This exercise uses that capability to monitor the healing process from start to finish.

---

## Prerequisites

- Completed [Exercise 08 — Generate Self-Healing Workflow & Trigger a Failure](EXERCISE_08_SELF_HEALING_SETUP.md)
- The CI workflow has a `failure` conclusion visible in the **Actions** tab
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Confirm the CI Failure

```cmd
copilot
```

```
Show me the most recent workflow runs and identify any failed ones.
```

Confirm the CI run shows `failure`. If the self-healing workflow has not yet triggered, wait 60 seconds and re-ask.

---

## Step 2 — Monitor the Self-Healing Workflow in Real Time

```
Monitor the self-healing workflow that triggered after the CI failure and show its current status.
```

You should see jobs progress through:
1. `checkout` — clone the repository
2. `detect-issues` — scan Python files for imports missing from requirements.txt
3. `apply-fixes` — add `requests` to requirements.txt, run isort + black
4. `verify` — run the test suite against the fixed code
5. `create-pr` — push branch and open pull request

---

## Step 3 — Analyse What Was Fixed

```
Analyse the self-healing workflow logs and explain the fixes that were applied.
```

Expected summary:

```
Issue Detected:
  Missing dependency 'requests' in app/main.py (not in requirements.txt)

Fixes Applied:
  1. Added requests>=2.28.0,<3.0.0 to requirements.txt
  2. isort: import order corrected in app/main.py
  3. black: no formatting changes needed

Verification:
  All tests passed — coverage maintained

PR: "fix: auto-heal — missing dependencies and formatting"
    Branch: self-healing/auto-fix-{run_id} → main
    Files changed: requirements.txt (+1 line)
```

---

## Key Takeaways

- Copilot CLI translates natural language into `gh run`, `gh run view`, and `gh run logs` calls — no syntax needed.
- The detect → fix → verify → propose pattern is reusable: swap the scanner and fixer scripts for any language or tool chain.
- Always check which files the healing workflow touched before merging its PR.

> **Next:** [Exercise 10 — Review the Self-Healing PR & Verify Recovery](EXERCISE_10_REVIEW_AND_MERGE.md)

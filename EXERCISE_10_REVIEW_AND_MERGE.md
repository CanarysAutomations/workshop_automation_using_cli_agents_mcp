# Exercise 10 — Review the Self-Healing PR & Verify Recovery

> **Duration:** 10 minutes | **Feature:** Copilot CLI + GitHub PR review | **Goal:** Inspect the pull request opened by the self-healing workflow, confirm the diff is correct, merge it, and verify the CI build returns to green.

---

## Background

The self-healing workflow has done its job — pushed a fix branch and opened a PR. Before merging any automated change, a human must verify the diff is minimal and correct. This exercise uses Copilot CLI to surface the PR details, then merges it and confirms the build recovered.

---

## Prerequisites

- Completed [Exercise 09 — Observe & Analyse the Self-Healing Workflow](EXERCISE_09_OBSERVE_SELF_HEALING.md)
- The self-healing PR is open in your repository
- Terminal open inside `Help_Desk_Application` with `.venv` activated

---

## Step 1 — Surface the Pull Request

Continue in the same Copilot CLI session (or reopen with `copilot`):

```
Show me the pull request created by the self-healing workflow, including the file diff.
```

Copilot lists the PR number, labels (`self-healing`, `automated`), and the diff. Confirm:
- Only `requirements.txt` was modified
- The correct version range was added (`requests>=2.28.0,<3.0.0`)
- No unrelated files were changed

---

## Step 2 — Merge the Pull Request

Navigate to the PR in your browser and click **"Merge pull request"**, or merge from the terminal:

```cmd
gh pr merge --merge --subject "fix: restore build after self-healing fix"
```

---

## Step 3 — Confirm the Build Is Green

```
Check the latest CI run on main and confirm it passed.
```

Expected: `✓ CI workflow — success`

---

## Key Takeaways

- Always inspect the self-healing PR diff before merging — the fix should touch **only** the identified broken file.
- `gh pr merge` from the terminal is faster than the browser for quick merges during a workshop.
- Confirming the CI run after merge closes the feedback loop and validates the entire self-healing chain.

> **Core track complete!** Continue to the optional exercises:
> - [Exercise 11 — Build PR Summarizer Agent — SDK Setup](EXERCISE_11_SDK_BUILD_AGENT.md)
> - [Exercise 13 — Debug: Introduce Bugs & Diagnose](EXERCISE_13_DEBUGGING_DIAGNOSE.md)
>
> Or return to the [Workshop README](Readme.md).

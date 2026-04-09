# Exercise 12 — Test & Automate the PR Summarizer

> **Duration:** 15 minutes | **Feature:** Copilot SDK + GitHub Actions | **Goal:** Run the PR summarizer agent locally against the self-healing PR, confirm the AI comment appears, then wire it to GitHub Actions so every new PR gets summarised automatically.

---

## Background

The agent built in Exercise 11 can already run from the command line. This exercise validates it locally first, then automates it with a GitHub Actions workflow so it fires on every `pull_request` event — no manual steps required.

---

## Prerequisites

- Completed [Exercise 11 — Build the PR Summarizer Agent](EXERCISE_11_SDK_BUILD_AGENT.md)
- `agents/pr_summarizer/` directory with all four modules and `.env` configured
- At least one open or recently closed PR (self-healing PR from Exercise 10)

---

## Step 1 — Test the Agent Locally

Replace `XX` with the actual PR number from Exercise 10:

```powershell
python agents\pr_summarizer\agent.py --repo CanarysPlayground/Help_Desk_Application --pr-number XX
```

Expected output:

```
Fetching PR #XX...
Analysing 1 changed file(s) with Copilot...
Posting summary comment to PR #XX...
Done. https://github.com/CanarysPlayground/Help_Desk_Application/pull/XX
```

Open the PR in your browser and confirm the AI summary comment appears.

---

## Step 2 — Generate the GitHub Actions Workflow

Open Copilot Chat and generate the workflow file:

```
Create a GitHub Actions workflow that triggers when a pull request is opened or updated.
1. Checkout repository, setup Python 3.11
2. Install agents/pr_summarizer/requirements-agent.txt
3. Run agents/pr_summarizer/agent.py with the PR number from the event context
Use GITHUB_TOKEN and OPENAI_API_KEY repository secrets.
Save as .github/workflows/copilot-pr-summarizer.yml
```

Save the generated YAML to `.github/workflows/copilot-pr-summarizer.yml`.

---

## Step 3 — Commit, Push, and Verify

```cmd
git add .github/workflows/copilot-pr-summarizer.yml agents/pr_summarizer/
git commit -m "feat: Copilot SDK PR summarizer agent and workflow"
git push origin main
```

Open a new pull request in your repository — the summarizer workflow should trigger and post an AI comment within 30–60 seconds.

---

## Key Takeaways

- Test agents locally with a known PR number before deploying to CI — it is faster to debug config issues on the command line.
- Editing existing bot comments (not creating new ones) keeps PR threads clean on repeated runs.
- `pull_request` triggers with `types: [opened, synchronize]` ensures every push to a PR re-summarises the latest changes.

> **Optional track — SDK complete!** Continue to [Exercise 13 — Debug: Introduce Bugs & Diagnose](EXERCISE_13_DEBUGGING_DIAGNOSE.md) or return to the [Workshop README](Readme.md).

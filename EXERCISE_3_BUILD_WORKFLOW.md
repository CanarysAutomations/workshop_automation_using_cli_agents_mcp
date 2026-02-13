# Exercise 3: Build GitHub Actions Workflow


## 🎯 Objective
Use Copilot CLI to generate GitHub Actions workflow YAML files for CI/CD, including build, test, and deployment automation for the Helpdesk CRM application.

---

## 📋 Workflow Requirements

### Workflows to Create
1. **CI Workflow:** Build and test on every push/PR
2. **CD Workflow:** Deploy on merge to main
3. **Issue Automation:** Auto-assign based on labels
4. **Release Workflow:** Create releases with changelog

---

## 🤖 Exercise: Generate Workflow YAML

### Step 1: Open Copilot Chat
```bash
copilot 
```

### Step 2: Generate CI Workflow

#### 🔹 Prompt for CI Workflow
```
@helpdesk-crm-agent

Generate a GitHub Actions CI workflow YAML file for the Helpdesk CRM FastAPI application.

Requirements:
- Trigger on push to main and feature branches
- Trigger on pull requests
- Python 3.11
- Install dependencies from requirements.txt
- Run pytest for tests
- Run flake8 for linting
- Upload test coverage report
- Cache pip dependencies

Output the complete workflow YAML.
```

---

### Step 3: Generate CD Workflow

#### 🔹 Prompt for CD Workflow
```
@helpdesk-crm-agent

Generate a GitHub Actions CD workflow for deploying the Helpdesk CRM app.

Requirements:
- Trigger on push to main only (after CI passes)
- Build Docker image
- Push to GitHub Container Registry (ghcr.io)
- Deploy to Azure App Service (optional step with environment secret)
- Send Slack notification on success/failure

Output the complete workflow YAML.
```
---

### Step 4: Generate Issue Automation Workflow

#### 🔹 Prompt for Issue Automation
```
@helpdesk-crm-agent

Generate a GitHub Actions workflow for issue automation.

Requirements:
- Trigger when issues are opened or labeled
- Auto-assign to team member based on label:
  - label:bug → assign to developers
  - label:docs → assign to tech writers
  - label:infra → assign to devops
- Add priority label based on keywords in title
- Comment with acknowledgment

Output the complete workflow YAML.
```

Here's the updated section for executing workflows and introducing dependency issues:

```markdown
## 🚀 Step 5: Execute Build Workflow

### Step 5.1: Trigger CI Workflow

**The CI workflow will trigger automatically when you:**
- Push commits to the branch
- Open or update a pull request

### Step 5.2: Monitor Build Execution

**Watch workflow in github.com Actions**
 Build and Test should succeed
```

##  Verify Build is Running Successfully

### Step 12.1: Check All Recent Workflow Runs

**All runs should show:** ✓ (success)


## 🐛 Part 13: Introduce Dependency Issue Manually

### Step 13.1: Add Import Statement Without Installing Package

**Open main.py in VS Code:**
```powershell
code app/main.py
```

**At the top of the file, add:**
```python
import requests  # This package is not in requirements.txt
```
If already requests is installed then uninstall it
```powershell
pip uninstall requests
```




This section includes:
- ✅ Generated CI workflow yaml
- ✅ Generated CD workflow yaml
- ✅ Generated Issue Automation workflow yaml
-✅ Committed workflows to `.github/workflows/`
- ✅ Steps to execute and monitor build workflow
- ✅ Understanding and testing issue automation workflow
- ✅ Verifying build is running successfully
- ✅ Introducing dependency issue (import requests + uninstall)
- ✅ Watching self-healing workflow trigger and fix the issue
- ✅ Bridge to Exercise 4 for deeper self-healing understanding
---


---

## 🚀 Next Exercise

Proceed to [Exercise 4: Self-Healing with SDK](EXERCISE_4_SELF_HEALING.md) to implement automatic dependency issue resolution using Copilot SDK.

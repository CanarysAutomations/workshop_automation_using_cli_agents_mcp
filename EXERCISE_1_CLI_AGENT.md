```markdown
# Exercise 1: Create a Custom Coding Agent via CLI



## 🎯 Objective
Use Copilot CLI to create a custom coding agent that will help implement features in the Helpdesk CRM application.

---

## 📚 Reference Documents
- [Install Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/install-copilot-cli)
- [Use Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli)
- [Add Custom Instructions](https://docs.github.com/en/copilot/how-tos/copilot-cli/add-custom-instructions)
- [About Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli)

---

## 📦 Part 1: Prerequisites and Installation

### Step 1.1: Prerequisites

Before installing Copilot CLI, ensure you have:

- **GitHub Account**: Active GitHub account with Copilot access
- **GitHub Copilot Subscription**: Individual, Business, or Enterprise subscription
- **Supported Operating System**: Windows, macOS, or Linux
- **Internet Connection**: Required for authentication and API calls

### Step 1.2: Install GitHub CLI

**Windows (Command Prompt)**
```cmd
:: Install GitHub CLI using winget
winget install --id GitHub.cli

:: Verify installation
gh --version
```

**Alternative Windows Installation Methods:**
- Download MSI installer from [https://cli.github.com/](https://cli.github.com/)
- Use Chocolatey: `choco install gh`
- Use Scoop: `scoop install gh`

**macOS**
```bash
# Install using Homebrew
brew install gh

# Verify installation
gh --version
```

### Step 1.3: Update GitHub CLI (If Already Installed)

**Windows**
```cmd
winget upgrade --id GitHub.cli
```

**macOS**
```bash
brew upgrade gh
```

### Step 1.4: Authenticate with GitHub CLI

**Interactive Authentication**
```cmd
/login
```

I understand now. You want to document the `/login` slash command workflow that's used within the Copilot CLI chat. Here's the corrected Step 1.4 with the proper authentication flow using `/login`:

```markdown
### Step 1.4: Authenticate with GitHub CLI

**Step 1: GitHub CLI Authentication**

First, authenticate with GitHub CLI:
```cmd
gh auth login
```

**Authentication Flow:**

1. **Enter the `/login` command** in the Copilot CLI chat
2. **Copilot will display**:
   - A verification code (e.g., `ABCD-1234`)
   - A URL link (e.g., `https://github.com/login/device`)
3. **Copy the verification code** shown in the terminal
4. **Click the URL** or manually open `https://github.com/login/device` in your browser
5. **Paste the verification code** in the browser
6. **Click "Continue"** to proceed with authorization
7. **Authorize GitHub Copilot** when prompted
8. **Return to terminal** - You should see a success message


**Verify Authentication**
```cmd 
copilot
```

## 📁 Part 2: Clone Repository Using CLI

### Step 2.1: Navigate to Desired Directory

**Windows Command Prompt**
```cmd
cd C:\Users\<UserName>\
```

### Step 2.2: Clone Help Desk Application Repository

```cmd
gh repo clone https://github.com/CanarysPlayground/Help_Desk_Application.git
```

### Step 2.3: Navigate to Cloned Repository

```cmd
cd Help_Desk_Application
```

### Step 2.4: Verify Repository Contents

```cmd
dir
```


## 📝 Part 3: Add Custom Instructions to Copilot CLI

### Step 3.1: Create Custom Instructions Directory

**Windows**
```cmd
mkdir .github
```

### Step 3.2: Generate Custom Instructions File Using Copilot CLI

Launch Copilot CLI chat:
```cmd
copilot
```

In the Copilot CLI chat, use the following prompt:

#### 🔹 Prompt to Generate Custom Instructions
```
Create a custom instructions file named "copilot-instructions.md" for the Helpdesk CRM application with the following guidelines:

1. Project Context: FastAPI-based helpdesk ticketing system
2. Code Style: Follow PEP 8 for Python, use type hints
3. Architecture: Repository pattern with services layer
4. Database: SQLAlchemy ORM with SQLite
5. Testing: Use pytest for unit and integration tests
6. Documentation: Clear docstrings for all functions and classes
7. Error Handling: Proper exception handling with meaningful messages
8. API Design: RESTful endpoints with Pydantic schemas for validation
```

### Step 3.3: Verify Custom Instructions

In chat, ask:
```
? What are the custom instructions for this project?
```

Copilot should reference the custom instructions file created in `.github/copilot-instructions.md`.

---

## 🤖 Part 4: Create Custom Agent Using Copilot CLI

### Step 4.1: Request Help from Copilot

I'll provide you with the steps for creating an agent using the `/agent` command in Copilot CLI, including both manual and Copilot-assisted options:

```markdown
## 🤖 Part 4: Create Custom Agent Using Copilot CLI

### Step 4.1: Start Copilot CLI Chat if you have exited

```cmd
copilot
```

### Step 4.2: Create Custom Agent Using `/agent` Command

Once in the Copilot CLI chat, use the `/agent` command:

```
/agent
```

**You will see two options:**

1. **Create agent manually** - You define the agent structure yourself
2. **Create agent with Copilot** - Copilot assists in creating the agent

---

#### Option 1: Create Agent Manually

**Step 1: Select Manual Creation**
```
/agent
→ Select: "Create agent manually"
```

**Step 2: Provide Agent Details**

Follow the prompts:
- **Agent Name**: `helpdesk-crm-agent`
- **Description**: `Custom coding agent for Helpdesk CRM application that implements features, fixes bugs, and creates workflows`
- **Capabilities**: Select from:
  - `code_analysis` - Analyze existing code
  - `code_generation` - Generate new code
  - `code_review` - Review and suggest improvements
  - `testing` - Create and run tests
  - `documentation` - Generate documentation

**Step 3: Define Agent Scope**
- **Allowed Paths**: `app/**, tests/**, .github/**`
- **Programming Languages**: `python`
- **Frameworks**: `fastapi, sqlalchemy, pydantic, pytest`

**Step 4: Set Agent Behavior**
- **Context Awareness**: Enable (uses custom instructions)
- **Auto-suggestions**: Enable
- **Validation**: Require code review before applying changes

---

#### Option 2: Create Agent with Copilot (Recommended)

**Step 1: Select Copilot-Assisted Creation**
```
/agent
→ Select: "Create agent with Copilot"
```

**Step 2: Use This Prompt**

```
Create a custom coding agent named "helpdesk-crm-agent" for our FastAPI-based helpdesk ticketing system.

Agent Purpose:
- Implement new features following repository pattern
- Fix bugs in ticket and customer management
- Generate tests for services and API endpoints
- Create and update API documentation
- Suggest code improvements based on best practices

Agent Capabilities:
- Analyze FastAPI routes, Pydantic schemas, and SQLAlchemy models
- Generate CRUD operations following our architecture pattern
- Create pytest unit and integration tests
- Review code for PEP 8 compliance and type hints
- Suggest performance optimizations

Context:
- Project uses: FastAPI, SQLAlchemy, SQLite, Pydantic, pytest
- Architecture: Route → Service → Repository → Model
- Code style: PEP 8 with type hints, 100 char line limit
- File structure: app/models/, app/schemas/, app/api/, app/services/, app/repositories/

Agent Scope:
- Allowed paths: app/**, tests/**, .github/**
- Focus areas: ticket management, customer management, workflow automation
- Avoid modifying: core/config.py, core/database.py without explicit permission

Agent Behavior:
- Always follow custom instructions in .github/copilot-instructions.md
- Provide explanations for suggested changes
- Generate tests alongside code changes
- Use type hints and docstrings for all functions
- Suggest incremental changes rather than large rewrites
```

**Expected Output:**
```
✓ Agent "helpdesk-crm-agent" created successfully
✓ Agent capabilities configured
✓ Custom instructions linked
✓ Ready to assist with Helpdesk CRM development

To use this agent, mention @helpdesk-crm-agent in your questions.
```

---

### Step 4.3: Verify Agent Creation

**List Available Agents**
```
/agent list
```

**Expected Output:**
```
Available Agents:
1. helpdesk-crm-agent - Custom coding agent for Helpdesk CRM application
   Status: Active
   Capabilities: code_analysis, code_generation, testing, documentation
   Scope: app/**, tests/**, .github/**
```

---

### Step 4.4: Test Your Custom Agent

**Example 1: Ask Agent to Explain Codebase**
```
@helpdesk-crm-agent Explain the ticket creation flow in this codebase. List all files involved.
```

---
### Step 4.4: Agent Best Practices

**Do's:**
- ✓ Always mention `@helpdesk-crm-agent` to invoke the agent
- ✓ Be specific about file paths and feature requirements
- ✓ Ask for explanations if suggestions are unclear
- ✓ Request tests alongside code generation
- ✓ Review agent suggestions before applying changes

**Don'ts:**
- ✗ Don't apply changes without reviewing them
- ✗ Don't ask about unrelated technologies
- ✗ Don't expect agent to modify restricted files
- ✗ Don't provide incomplete context for complex tasks

---

## 💡 Tips for Effective Copilot CLI Usage

1. **Be Specific**: Provide context about your task (e.g., "in the ticket service" instead of "in the code")
2. **Iterative Approach**: Start with high-level questions, then drill down into specifics
3. **Reference Files**: Mention specific file paths for more accurate suggestions
4. **Follow-up Questions**: Ask for clarification or alternatives if first response isn't ideal
5. **Use Chat History**: Copilot maintains context within a chat session
6. **Custom Instructions**: Keep instructions updated as the project evolves

---


## 🚀 Next Exercise

Proceed to Exercise 2: Plan Assign Feature to use `/plan` command for implementing the Assign feature using Copilot CLI.

---

## 📖 Additional Resources

- [GitHub CLI Documentation](https://cli.github.com/manual/)
- [GitHub Copilot CLI Guide](https://docs.github.com/en/copilot/using-github-copilot/using-github-copilot-in-the-command-line)
- [GitHub Copilot Best Practices](https://docs.github.com/en/copilot/using-github-copilot/best-practices-for-using-github-copilot)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
```

---

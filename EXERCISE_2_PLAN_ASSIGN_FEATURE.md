# Exercise 2: Plan Assign Feature Using `/plan`



## 🎯 Objective
Use the `/plan` command to generate a detailed implementation plan for adding an "Assign" feature to tickets, allowing assignment to different roles: Developer, Test Engineer, and DevOps Engineer.

---

I'll help you create a comprehensive EXERCISE_2 that builds on the agent created in EXERCISE_1. Let me first read the existing EXERCISE_2 file to understand its current structure. 



```markdown
# Exercise 2: Plan Assign Feature Using Custom Agent

> Reference: Build on the custom agent created in [Exercise 1](EXERCISE_1_CLI_AGENT.md)

## 🎯 Objective
Use the custom agent created in Exercise 1 with the `/plan` command to generate a detailed implementation plan for adding an "Assign" feature to tickets.

---

## 📋 Feature Requirements

### Assign Feature Specification
- **UI:** Add a dropdown in the Ticket form to assign tickets to team members
- **Roles:** Developer, Test Engineer, DevOps Engineer
- **Backend:** Store assignment in the database with assignee role and name
- **API:** RESTful endpoint to handle ticket assignment
- **Validation:** Ensure valid roles and assignee names

---

## 🚀 Part 1: Select Your Custom Agent

### Step 1.1: Start Copilot CLI Chat

```cmd
copilot
```

### Step 1.2: List Available Agents

Check which agents are available:
```
/agent list
```

### Step 1.3: Select Your Custom Agent

Use the agent by mentioning it with `@`:
```
@helpdesk-crm-agent Hello! I need your help implementing a new feature.
```



## 🤖 Part 2: Select AI Model

### Step 2.1: View Available Models

Check which AI models are available:
```
/model
```

### Step 2.2: Select a Model

Choose a model based on your needs:
```
/model gpt-4
```

Or for faster responses:
```
/model gpt-4-turbo
```

Or for Claude:
```
/model claude-3-sonnet
```

**Expected Response:**
```
✓ Model switched to: gpt-4
This model offers the highest quality responses and is ideal for complex code generation tasks.
```

**Model Selection Guidelines:**
- **gpt-4 / claude-3-opus**: Complex features, architecture decisions, comprehensive refactoring
- **gpt-4-turbo / claude-3-sonnet**: Balanced performance for most development tasks
- **gpt-3.5-turbo**: Quick questions, simple code snippets, documentation

---

## 📝 Part 3: Generate Implementation Plan

### Step 3.1: Use `/plan` Command with Agent

Now use the `/plan` command with your selected agent:

```
@helpdesk-crm-agent /plan

Create a comprehensive implementation plan for adding an "Assign" feature to tickets in the Helpdesk CRM application.

Requirements:
1. Add "assigned_to" (string) and "assignee_role" (enum) fields to the Ticket model
2. Assignee roles: Developer, Test Engineer, DevOps Engineer
3. Create PUT endpoint /tickets/{id}/assign to handle assignment
4. Update Pydantic schemas to include assignment fields
5. Add validation for assignee roles
6. Create unit tests for assignment logic
7. Update UI with dropdown to select assignee role

Context:
- Follow repository pattern: Route → Service → Repository → Model
- Use FastAPI with SQLAlchemy ORM and SQLite database
- Pydantic v2 schemas for validation
- All code must have type hints and follow PEP 8
- File structure: app/models/, app/schemas/, app/api/, app/services/, app/repositories/

Output Requirements:
- Break down into phases
- List all files to modify
- Provide code changes with diffs
- Include test cases
- Follow custom instructions in .github/copilot-instructions.md
```

### Step 3.2: Review Generated Plan
The agent should respond with a detailed implementation plan.

## 🔍 Part 4: Understand Token Usage with `/context`

### Step 4.1: Check Current Context

Before executing the plan, check token usage:
```
/context
```

**What are tokens?**
- Tokens are pieces of text (words, parts of words, or characters)
- AI models have a maximum context window (e.g., 8,000-128,000 tokens)
- Both your input and the AI's response count toward the limit

**Why monitor tokens?**
- Ensures the AI has enough context to generate accurate code
- Prevents context overflow that might truncate important information
- Helps optimize which files to include in context

**Token Management Tips:**
```
# Add specific files to context
/context add app/models/ticket.py

# Remove files from context to save tokens
/context remove app/templates/index.html

# Clear context and start fresh
/context clear

# Show detailed token breakdown
/context verbose
```
---
## 📊 Part 5: Monitor and Verify

### Step 5.1: Check Context After plan

```
/context
```

Review token usage to ensure you haven't exceeded limits.


---


```markdown
## 🤝 Part 6: Delegate Implementation with `/delegate`

### Step 6.1: Initiate Delegation

**Prompt:**
```
/delegate

Implement the complete ticket assignment feature plan:

Add assigned_to and assignee_role fields to Ticket model
Update schemas with AssigneeRole enum validation
Create PUT /tickets/{id}/assign endpoint
Generate unit and integration tests
Follow custom instructions in .github/copilot-instructions.md
Ensure PEP 8 compliance and type hints on all code
```
```

### Step 6.3: GitHub Submission Prompt

**Copilot will display:**
```
Send this session to GitHub?

Prompt: the plan

Copilot will push your changes to copilot/joyous-ferret (based on workshopBranch) 
in CanarysPlayground/Help_Desk_Application and create a PR.

⬢ 1. Yes
  2. No, cancel (Esc)

↑↓ to navigate · Enter to select · Esc to cancel
```

**Action:** Press `Enter` to select "Yes" (Option 1)

**What this does:**
- Creates a new feature branch with auto-generated name (e.g., `copilot/joyous-ferret`)
- Uses current branch (`existing branch name`) as base
- Pushes changes to GitHub repository
- Creates a draft pull request automatically

### Step 6.4: Processing Phase - Sending to GitHub

**Copilot displays progress:**
```
Sending to GitHub (18s):
  Summarizing conversation context...

```
Copilot Coding Agent Job Started
================================
Agent Does the analysis and starts implementation...

```
Agent Job Complete!
===================

✓ Implementation successfully completed

### Step 6.7: Understanding the Draft PR

**Why Draft PR?**
- ✓ Allows review before marking ready for merge
- ✓ CI/CD pipeline runs automatically
- ✓ You can test implementation locally
- ✓ Make additional changes if needed
- ✓ Prevents accidental merges

**Check for What's in the PR:**
```
Title: Add <feature name> Feature

Status: 🔄 Draft
Base: <base branch>
Head: copilot/<new branch name?>
Commits: 1

Description:
------------
Implements <feature> functionality with role-based assignment.




## 🚀 Next: Access and Test the PR
#### Prompt:
    GIve me the summary of the PR created with /delegate


```


### 💡 Key Takeaways

**Using Custom Agents:**
- Prefix commands with `@agent-name` to invoke specific agent
- Agents maintain context and follow custom instructions
- Agents provide consistent code style across sessions

**Model Selection:**
- Choose model based on task complexity
- More powerful models for architecture decisions
- Faster models for simple tasks and iterations

**Context Management:**
- Monitor token usage to avoid context overflow
- Add/remove files strategically to optimize context
- Clear context when switching to unrelated tasks

**Planning Best Practices:**
- Break large features into phases
- Review plan before execution
- Execute phase by phase for better control
- Test after each phase when possible

**Delegation Benefits:**
- Automates implementation based on detailed plans
- Integrates with GitHub for seamless PR creation
- Allows for review and iteration before merging


## 📖 Additional Resources

- [GitHub Copilot CLI Documentation](https://docs.github.com/en/copilot/using-github-copilot/using-github-copilot-in-the-command-line)
- [Working with Custom Agents](https://docs.github.com/en/copilot/how-tos/use-copilot-agents)
- [Understanding Token Usage](https://platform.openai.com/docs/guides/tokens)
- [FastAPI Best Practices](https://fastapi.tiangolo.com/tutorial/)
```

This comprehensive exercise now includes:
1. ✅ Steps to select the custom agent created in Exercise 
2. ✅ Steps to select and switch between AI models using `/model`
3. ✅ Detailed `/plan` usage with the custom agent
4. ✅ `/context` command usage to understand token management
5. ✅ Phase-by-phase implementation with detailed examples
6. ✅ Verification steps and best practicesThis comprehensive exercise now includes:
7. ✅ Instructions for delegating implementation to the agent with `/delegate`
8. ✅ Explanation of the GitHub PR process and benefits of draft PRs

---

## 🚀 Next Exercise
Proceed to [Exercise 3: Build Workflow](EXERCISE_3_BUILD_WORKFLOW.md) to create GitHub Actions workflow YAML files for automation.

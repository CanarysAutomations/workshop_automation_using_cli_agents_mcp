# Agents in SDLC Workshop - Exercises

This hands-on workshop teaches you how to integrate **AI-powered agents** throughout the Software Development Lifecycle (SDLC) using **GitHub Copilot CLI**. You'll learn to automate coding tasks, plan features, build CI/CD workflows, and implement self-healing systems—all using natural language prompts with AI agents.

## Scenario

### The Application: Help Desk CRM
The Help Desk CRM is a ticketing system that manages customer support requests through a web interface. Customers can be registered with their contact information, and support tickets can be created with varying severity levels (low, medium, high, critical). The application provides a complete REST API for CRUD operations on customers and tickets, with automatic API documentation. Built with FastAPI and SQLAlchemy, it follows a layered repository pattern architecture for maintainability and scalability.



**Key Features:**
- ✅ Customer management (CRUD operations)
- ✅ Ticket management with severity levels
- ✅ RESTful API with auto-generated documentation
- ✅ Web-based frontend interface
- ✅ Layered architecture (Routes → Services → Repositories → Models)

## Lab overview

1. [Exercise 1: Create Custom CLI Agent](EXERCISE_1_CLI_AGENT.md)
2. [Exercise 2: Plan & Implement Ticket Assignment Feature](EXERCISE_2_PLAN_ASSIGN_FEATURE.md)
3. [Exercise 3: Build CI/CD Workflows](EXERCISE_3_BUILD_WORKFLOW.md)
4. [Exercise 4: Self-Healing Workflow In Action](EXERCISE_4_SELF_HEALING.md)
5. [Exercise 5: PR Summarizer with GitHub Copilot SDK](EXERCISE_5_PRSUMMARY_SDK.md)

### [Exercise 1: Create Custom CLI Agent](EXERCISE_1_CLI_AGENT.md)
**Duration:** 30 minutes  
**Difficulty:** Beginner

**What You'll Learn:**
- Install and authenticate GitHub CLI
- Install GitHub Copilot CLI extension
- Clone repository and set up project
- Create custom instructions for your domain (Helpdesk CRM)
- Generate a custom coding agent tailored to your application
- Use the `/agent` command to work with custom agents

### [Exercise 2: Plan & Implement Ticket Assignment Feature](EXERCISE_2_PLAN_ASSIGN_FEATURE.md)
**Duration:** 45 minutes  
**Difficulty:** Intermediate



### [Exercise 3: Build CI/CD Workflows](EXERCISE_3_BUILD_WORKFLOW.md)
**Duration:** 40 minutes  
**Difficulty:** Intermediate

### [Exercise 4: Self-Healing Workflow In Action](EXERCISE_4_SELF_HEALING.md)
**Duration:** 30 minutes  
**Difficulty:** Intermediate

### [Exercise 5: PR Summarizer with GitHub Copilot SDK](EXERCISE_5_PRSUMMARY_SDK.md)
**Duration:** 40 minutes  
**Difficulty:** Intermediate


## Learning Outcomes

By completing all four exercises, you will gain proficiency in:

### 1. **AI-Assisted Development**


### 2. **GitHub Copilot CLI Mastery**

### 3. **Modern Python Development**


### 4. **CI/CD Automation**


### 5. **Self-Healing Systems**




## Get started

1. **Setup Environment** - Follow [SetupInstructions.md](SetupInstructions.md)
2. **Clone Repository** - Get the Help_Desk_Application repo
3. **Install Dependencies** - Set up Python virtual environment
4. **Verify Setup** - Run tests and start the application
5. **Begin Exercise 1** - Start with CLI agent creation

**Recommended Path:**
```
SetupInstructions.md → Exercise 1 → Exercise 2 → Exercise 3 → Exercise 4 → Exercise 5
```

**Total Time Investment:** ~2.5 hours

## Workshop Structure

```
Workshop Flow
│
├── Setup (30 min)
│   ├── Clone repository
│   ├── Install dependencies
│   ├── Start application
│   └── Install Copilot CLI
│
├── Exercise 1: Custom Agent (30 min)
│   ├── Authenticate GitHub CLI
│   ├── Create custom instructions
│   └── Generate coding agent
│
├── Exercise 2: Feature Implementation (45 min)
│   ├── Plan with /plan command
│   ├── Delegate implementation
│   └── Create pull request
│
├── Exercise 3: CI/CD Workflows (40 min)
│   ├── Create CI workflow
│   ├── Build self-healing workflow
│   └── Test with dependency issue
│
└── Exercise 4: Self-Healing in Action (30 min)
    ├── Monitor workflows
    ├── Review auto-fixes
    └── Merge self-healing PR

└── Exercise 5: PR Summarizer with Copilot SDK (40 min)
    ├── Setup Copilot SDK environment
    ├── Build AI-powered PR analyzer
    ├── Create GitHub Actions integration
    └── Test automated PR summaries

```

## Additional Resources

### Documentation
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [Copilot CLI Guide](https://docs.github.com/en/copilot/using-github-copilot/using-github-copilot-in-the-command-line)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [SQLAlchemy 2.0 Tutorial](https://docs.sqlalchemy.org/en/20/)

### Workshop Materials
- [Setup Instructions](SetupInstructions.md)
- [Exercise 1: CLI Agent](EXERCISE_1_CLI_AGENT.md)
- [Exercise 2: Plan & Implement](EXERCISE_2_PLAN_ASSIGN_FEATURE.md)
- [Exercise 3: Build Workflows](EXERCISE_3_BUILD_WORKFLOW.md)
- [Exercise 4: Self-Healing](EXERCISE_4_SELF_HEALING.md)
- [Exercise 5: PR Summarizer with SDK](EXERCISE_5_PRSUMMARY_SDK.md)


## What's Next?

After completing this workshop, consider:

- **Apply to Your Projects:** Use custom agents in your own repositories
- **Explore Advanced Features:** Multi-agent orchestration, MCP servers
- **Customize Workflows:** Adapt self-healing for your specific needs
- **Share Knowledge:** Teach colleagues about Agents in SDLC
- **Contribute:** Improve this workshop or share your learnings
- **Explore Copilot SDK:** Build custom Copilot extensions

**Happy Learning with AI Agents! 🚀🤖**

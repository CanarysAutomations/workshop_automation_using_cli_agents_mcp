# Exercise 01: Business Requirements Document (BRD)

| | Exercise 01 Overview |
|---|---|
| **Time** | ~8 minutes |
| **Copilot Feature** | Local Custom Agent (`sdlc-agent`) |
| **Type** | 🔴 Mandatory |
| **You Will** | Create the `sdlc-agent` custom agent (reused in EX-02–04), then generate `docs/BRD.md` from `docs/REQUIREMENTS.md` |
| **Input** | `docs/REQUIREMENTS.md` |
| **Output** | `docs/BRD.md`, `.github/agents/sdlc-agent.agent.md` |
| **Next** | [Exercise 02: Functional Requirements →](exercise-02-frd-agent-skills.md) |

## Workshop Progress

> `01 BRD` → [02 FRD](exercise-02-frd-agent-skills.md) → [03 TSD](exercise-03-tsd-cloud-agent.md) → [04 Instructions](exercise-04-impl-plan-background-agent.md) → [05 Scaffold](exercise-05-scaffold-cli.md) → [06 Tests](exercise-06-tests-background-agent.md) → [07 Gate ⚪](exercise-07-quality-gate-cli.md)

---

## Goal

Create a single multi-purpose **`sdlc-agent`** custom agent and use it to read `docs/REQUIREMENTS.md` and generate a structured Business Requirements Document.

> **Local agent vs cloud agent:** The `sdlc-agent` you create runs entirely in VS Code and reads files on your local machine. It never calls the GitHub API. This is different from `@github` (used in Exercise 05).

---

## ⚡ Starting Here?

`docs/REQUIREMENTS.md` is already in this repo — it is the single source of truth for the entire workshop. Open it now and read sections **C1–C5** (Core Capabilities) before continuing.

---

## 1.1 Create the `sdlc-agent` Local Custom Agent

This agent will be reused in Exercises 02, 03, and 04. Create it once here.

**1.** Open **Copilot Chat** → click **Configure** (⚙️ gear icon, top-right of the chat panel).

**2.** Select **Agents** → click **+ New Agent**.

**3.** In the file dialog:
- Navigate to `.github/agents/` as the save location
- Enter agent name: `sdlc-agent`
- Click **Save**

> VS Code creates `.github/agents/sdlc-agent.agent.md`.

---

**4.** Copy the entire block below and paste it as the **full contents** of `.github/agents/sdlc-agent.agent.md`:

> | Field | Value |
> |-------|-------|
> | **Name** | `sdlc-agent` |
> | **Model** | `claude-sonnet-4-5` |
> | **Description** | SDLC document generator — creates BRD, FRD, and TSD for greenfield SaaS products |
> | **Instructions** | See body below the `---` line |

```markdown
---
name: sdlc-agent
description: >
  SDLC document generator. Creates BRD, FRD, and TSD artefacts for
  greenfield SaaS products. Reads local workspace files for context.
  Trigger phrases: generate BRD, generate FRD, generate TSD,
  business requirements, functional requirements, technical spec.
model: claude-sonnet-4-5
tools:
  - read_file
  - create_file
---

## Identity
You are a senior software delivery consultant with expertise in
business analysis, product management, and solution architecture.
You generate precise, developer-ready SDLC documents.

## General Rules
- Only use content from files the user explicitly references — never invent requirements
- Flag any ambiguous or missing detail as ⚠️ NEEDS CLARIFICATION
- Output structured Markdown suitable for saving directly to a file
- Keep each section concise: max 5–6 bullet points unless a table is more appropriate

## BRD Format
When asked to generate a BRD, produce these sections in order:
1. **Executive Summary** — 2–3 sentences: product, audience, core value
2. **Problem Statement** — reference measurable pain points from the source material
3. **Goals & Success Metrics** — SMART targets with numbers
4. **Stakeholders & Roles** — table with columns: Role | Responsibilities | Key Needs
5. **User Stories** — for each capability: As a [role] I want [feature] so that [outcome]
   - Each story must have 2–3 independently verifiable Acceptance Criteria
6. **Out of Scope** — bullet list from the source document
7. **Risks & Assumptions** — table: Risk | Likelihood | Mitigation

## FRD Format
When asked to generate an FRD, for every feature produce:
Feature ID → Feature Name → Description (one sentence) →
Inputs/Outputs table (Field | Type | Required) →
Acceptance Criteria (numbered, independently verifiable) →
Data Model (key fields + types, MVP only) →
API Contract (Method | Endpoint | Request Body | Response shape)

## TSD Format
When asked to generate a TSD, produce these sections in order:
1. Architecture Decision — monolith vs microservices, with 3-bullet justification
2. Tech Stack — as confirmed by the user, with specific library versions
3. Data Schema — ERD as text, all entities with relationships
4. API Design — endpoint table mapped to FRD feature IDs
5. Auth Strategy — JWT token shape, expiry, refresh approach
6. Non-Functional Targets — response time, uptime, scaling approach
7. Infrastructure — container strategy, CI/CD approach
```

**5.** Save the file. Reload VS Code: `Ctrl+Shift+P` → **Developer: Reload Window**.

---

## 1.2 Generate the BRD

**1.** Open Copilot Chat. In the agent dropdown (top of chat panel), select **sdlc-agent**.

**2.** Copy and paste this prompt:

> **Prompt — Generate BRD** *(paste into Copilot Chat with sdlc-agent selected)*

```
Read #file:docs/REQUIREMENTS.md.

Generate the BRD for TaskFlow following your BRD Format.
- Expand each core capability (C1–C5) into user stories with acceptance criteria
- Include SMART success metrics referencing the numbers in REQUIREMENTS.md
- List all out-of-scope items from the document

Save output as docs/BRD.md.
```

**3.** After the agent writes `docs/BRD.md`, open it. Verify:
- [ ] Problem Statement references the measurable pain stat from REQUIREMENTS.md
- [ ] User stories for all 5 capabilities (C1–C5)
- [ ] Each acceptance criterion is independently verifiable
- [ ] Success metrics include numeric targets (e.g., 500 teams, 99.5% uptime)
- [ ] Risks table is present

---

## 🐛 Debug: Agent Ignores the Source File

If the output omits a capability or invents features not in REQUIREMENTS.md:

```
The BRD is missing [C2 / section name]. 
Refer to #file:docs/REQUIREMENTS.md section C2 and add the missing user stories.
Do not add any feature not present in the source file.
```

If the agent dropdown does not show `sdlc-agent`:

> `Ctrl+Shift+P` → **Developer: Reload Window** → reopen Copilot Chat → check Configure → Agents.

---

## What You Built

| Artifact | Location |
|----------|----------|
| `sdlc-agent` local custom agent | `.github/agents/sdlc-agent.agent.md` |
| Business Requirements Document | `docs/BRD.md` |

---

| | Navigation |
|---|---|
| **Produces** | `docs/BRD.md` — consumed by Exercise 02 |
| **Next →** | [Exercise 02: Functional Requirements →](exercise-02-frd-agent-skills.md) |

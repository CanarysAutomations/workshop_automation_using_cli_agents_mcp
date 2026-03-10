# Exercise 02: Functional Requirements Document (FRD)

| | Exercise 02 Overview |
|---|---|
| **Time** | ~8 minutes |
| **Copilot Feature** | Agent Skills + Local Custom Agent (`sdlc-agent`) |
| **Type** | 🔴 Mandatory |
| **You Will** | Create a `frd-writer` skill and use it with `sdlc-agent` to produce `docs/FRD.md` — Feature IDs, data models, and API contracts |
| **Input** | `docs/BRD.md` (or inline fallback from `docs/REQUIREMENTS.md`) |
| **Output** | `docs/FRD.md` (FRD-001–005), `.github/skills/frd-writer/SKILL.md` |
| **Next** | [Exercise 03: Technical Specification →](exercise-03-tsd-cloud-agent.md) |

## Workshop Progress

> [01 BRD](exercise-01-brd-custom-agent.md) → `02 FRD` → [03 TSD](exercise-03-tsd-cloud-agent.md) → [04 Instructions](exercise-04-impl-plan-background-agent.md) → [05 Scaffold](exercise-05-scaffold-cli.md) → [06 Tests](exercise-06-tests-background-agent.md) → [07 Gate ⚪](exercise-07-quality-gate-cli.md)

---

## Goal

Create a `frd-writer` **Agent Skill** and use it together with the `sdlc-agent` from Exercise 01 to generate a structured Functional Requirements Document — with Feature IDs, data models, and API contracts — from `docs/BRD.md`.

> **Agent Skill vs Custom Agent:** A custom agent carries *identity + behaviour*. A skill is a *structured prompt template* you attach with `#file:`. Skills augment any agent. Here you combine both.

---

## ⚡ Starting Here?

If you skipped Exercise 01, generate a minimal BRD inline now:

```
Using #file:docs/REQUIREMENTS.md, summarise the 5 core capabilities (C1–C5)
as a bullet-point BRD: feature name, one-line description, primary user role.
Print inline only — do not save to file.
```

Use that inline output as your FRD input in step 2.2.

---

## 2.1 Create the `frd-writer` Agent Skill

**1.** Open **Copilot Chat** → **Configure** (⚙️) → **Skills** → **+ New Skill**.

**2.** In the file dialog:
- Location: `.github/skills/frd-writer/`
- File name: `SKILL.md`
- Click **Save**

> VS Code creates `.github/skills/frd-writer/SKILL.md`.

---

**3.** Copy the entire block below and paste it as the **full contents** of `.github/skills/frd-writer/SKILL.md`:

> | Field | Value |
> |-------|-------|
> | **Name** | `frd-writer` |
> | **Model** | `claude-sonnet-4-5` |
> | **Description** | Converts a BRD into a structured FRD with Feature IDs, API contracts, and data models |
> | **Instructions** | See body below the `---` line |

```markdown
---
name: frd-writer
description: >
  Converts a BRD into a structured Functional Requirements Document.
  Produces Feature IDs, data models, API contracts, and acceptance criteria.
  Trigger phrases: generate FRD, functional requirements, feature spec,
  API contract, data model.
model: claude-sonnet-4-5
---

## Your Output Format
For every feature identified in the BRD, produce all 7 sections in this exact order:

1. **Feature ID** — sequential identifier, e.g. FRD-001, FRD-002
2. **Feature Name** — concise title (3–6 words)
3. **Description** — one sentence stating what this feature does
4. **Inputs / Outputs** — table with columns: Field | Type | Required | Notes
5. **Acceptance Criteria** — numbered list; every item must be independently verifiable
   - Bad: "The feature works correctly"
   - Good: "POST /auth/register returns HTTP 201 and a JSON body containing { id, email, createdAt }"
6. **Data Model** — key entities, fields, and types needed for MVP only
   - Mark fields Required or Optional
   - Note Post-MVP fields rather than omitting them
7. **API Contract**
   | Method | Endpoint | Request Body | Success Response | Error Responses |
   |--------|----------|--------------|------------------|-----------------|

## Rules
- Never skip a section — if data is unavailable, write "TBD — needs decision"
- Flag any feature with unclear scope as ⚠️ NEEDS DECISION
- Keep data models minimal — only fields required for the stated acceptance criteria
- All endpoint paths must be lowercase, kebab-case, versioned at /api/v1/
```

**4.** Save and reload VS Code (`Ctrl+Shift+P` → **Developer: Reload Window**).

---

## 2.2 Generate the FRD

**1.** Open Copilot Chat → select **sdlc-agent** in the agent dropdown.

**2.** Copy and paste this prompt:

> **Prompt — Generate FRD** *(paste into Copilot Chat with sdlc-agent selected)*

```
Using #file:.github/skills/frd-writer/SKILL.md as your output format,
read #file:docs/BRD.md (or #file:docs/REQUIREMENTS.md if BRD not available).

Generate FRD entries for these 5 features:
- FRD-001: User registration & JWT authentication (C1)
- FRD-002: Project creation and team membership management (C2)
- FRD-003: Task creation with assignee, due date, priority, and labels (C3)
- FRD-004: Task status transitions — Todo → In Progress → Under Review → Done (C3)
- FRD-005: Dashboard views — My Tasks, Per-Project summary, Team workload (C5)

Follow the 7-section format in the skill file exactly. Do not skip any section.
Save output as docs/FRD.md.
```

**3.** Open `docs/FRD.md`. Verify:
- [ ] Feature IDs FRD-001 through FRD-005 are all present
- [ ] Each feature has numbered acceptance criteria
- [ ] At least one API endpoint per feature with request/response shape
- [ ] Data model fields include types (string, integer, timestamp, boolean…)
- [ ] No acceptance criterion says "works correctly" or "functions as expected"

---

## 🐛 Debug: Skill Structure Not Applied

If the output is unstructured (missing Feature IDs or API contracts):

```
FRD-001 is missing the API Contract section.
Reread #file:.github/skills/frd-writer/SKILL.md and regenerate FRD-001 
following the exact 7-section format. Do not change FRD-002 through FRD-005.
```

If `sdlc-agent` is not visible in the dropdown:

> `Ctrl+Shift+P` → **Developer: Reload Window** — the agent was created in Exercise 01.  
> If you skipped Ex 01, complete step 1.1 of Exercise 01 first (create the agent — it takes ~3 minutes).

---

## What You Built

| Artifact | Location |
|----------|----------|
| `frd-writer` Agent Skill | `.github/skills/frd-writer/SKILL.md` |
| Functional Requirements Document | `docs/FRD.md` |

> **Skills are reusable** — attach `#file:.github/skills/frd-writer/SKILL.md` to any prompt in any exercise to re-apply the same structured format.

---

| | Navigation |
|---|---|
| **Produces** | `docs/FRD.md` — FRD-001 to FRD-005 with API contracts, consumed by Exercise 03 |
| **← Previous** | [Exercise 01: Business Requirements](exercise-01-brd-custom-agent.md) |
| **Next →** | [Exercise 03: Technical Specification →](exercise-03-tsd-cloud-agent.md) |

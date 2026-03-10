# Exercise 03: Technical Specification Document (TSD)

| | Exercise 03 Overview |
|---|---|
| **Time** | ~9 minutes |
| **Copilot Feature** | Local Custom Agent (`sdlc-agent`) |
| **Type** | 🔴 Mandatory |
| **You Will** | Pick your tech stack (Node.js/Express or Python/FastAPI), confirm it in chat, then generate `docs/TSD.md` covering architecture, ERD, API design, auth, and NFRs |
| **Input** | `docs/FRD.md` + `docs/REQUIREMENTS.md`, your team's stack choice |
| **Output** | `docs/TSD.md` with your chosen stack locked in |
| **Next** | [Exercise 04: Generate Copilot Instructions →](exercise-04-impl-plan-background-agent.md) |

## Workshop Progress

> [01 BRD](exercise-01-brd-custom-agent.md) → [02 FRD](exercise-02-frd-agent-skills.md) → `03 TSD` → [04 Instructions](exercise-04-impl-plan-background-agent.md) → [05 Scaffold](exercise-05-scaffold-cli.md) → [06 Tests](exercise-06-tests-background-agent.md) → [07 Gate ⚪](exercise-07-quality-gate-cli.md)

---

## Goal

Make your own **tech stack decision**, then use the `sdlc-agent` local custom agent to generate a complete Technical Specification Document that reflects your choice.

> **Why local agent?** The TSD must stay consistent with `docs/FRD.md` and `docs/BRD.md` on your disk. The `sdlc-agent` reads all three files locally without needing a GitHub connection.

---

## ⚡ Starting Here?

If you skipped previous exercises, generate minimal context inline:

```
Read #file:docs/REQUIREMENTS.md. List the 5 capabilities (C1–C5) and 
the Non-Functional Requirements (NFRs) as bullet points. Print inline only.
```

Use that inline context in step 3.2 below if `docs/FRD.md` does not exist.

---

## 3.1 Open the `sdlc-agent`

**1.** Open **Copilot Chat** → click the agent dropdown → select **sdlc-agent**.

> If `sdlc-agent` is not listed: complete Exercise 01 step 1.1 first (takes ~3 min).

---

## 3.2 You Decide the Tech Stack

This is a design decision made by your team — not something to delegate to the model. Gather information first, then commit.

**1.** With `sdlc-agent` selected, copy and paste:

> **Prompt 1 — Request Stack Options** *(paste into Copilot Chat with sdlc-agent selected)*

```
Read #file:docs/REQUIREMENTS.md.

Present 2 backend stack options for TaskFlow:
- Option A: Node.js + Express + PostgreSQL
- Option B: Python + FastAPI + PostgreSQL

For each option give:
  - 3 pros relevant to this product's NFRs (p95 < 300ms, 99.5% uptime, JWT auth)
  - 2 cons for a 2-engineer, 90-day MVP
  - One sentence on when this option is the better choice

Do not recommend — present both objectively.
```

**2.** Read both options. Discuss with your team if working in pairs.

**3.** Lock in your choice:

> **Prompt 2 — Confirm Your Stack Choice** *(replace `[Option A / Option B]` with your choice)*

```
I choose [Option A / Option B].
Use this stack for the entire TSD. Do not suggest alternatives.
```

> ⚠️ Write your stack choice on a sticky note or in a local note. You will reference it in Exercise 04 and the GitHub issue in Exercise 05.

---

## 3.3 Generate the TSD

**1.** In the same chat thread (so the agent retains your stack choice), copy and paste:

> **Prompt 3 — Generate TSD** *(paste in the same chat thread so the agent remembers your stack)*

```
Using the stack I just confirmed, read #file:docs/FRD.md 
and #file:docs/REQUIREMENTS.md.

Generate docs/TSD.md using your TSD Format. Cover:
1. Architecture Decision — monolith for MVP, 3-bullet justification
2. Tech Stack — confirm my chosen stack, list specific library versions (Express 4.x / FastAPI 0.11x, pg / asyncpg, Jest / pytest, Docker)
3. Data Schema — ERD as text, entities: User, Team, Project, Task, Notification
4. API Design — endpoint table mapped to FRD-001 through FRD-005
5. Auth Strategy — JWT: access token shape, 15-min expiry, refresh token approach
6. Non-Functional Targets — p95 < 300ms, 99.5% uptime, horizontal scale via containers
7. Infrastructure — Dockerfile + single VM for MVP, GitHub Actions CI pipeline

Keep each section under 10 lines. Save as docs/TSD.md.
```

**2.** Open `docs/TSD.md`. Verify:
- [ ] Stack matches what you chose (not a different one)
- [ ] Architecture decision has 3-bullet justification
- [ ] ERD includes User, Team, Project, Task entities with relationships
- [ ] API table references FRD-001 through FRD-005
- [ ] Non-functional targets include the specific numbers (300ms, 99.5%)
- [ ] Auth strategy specifies JWT token shape and expiry

---

## 3.4 Resolve FRD / TSD Conflicts

If the TSD proposes a different auth approach than FRD-001 specifies:

```
FRD-001 specifies [paste the conflicting line from FRD.md].
The TSD section 5 proposes [conflicting decision].
Which is correct for a 90-day MVP with 2 engineers?
Update docs/TSD.md section 5 to resolve this conflict.
```

---

## 🐛 Debug: Wrong Stack in TSD

If `docs/TSD.md` uses a different stack than you selected:

```
The TSD uses [wrong stack] but I chose [your choice].
Update sections 2, 3, and 4 of docs/TSD.md to use [your choice].
Do not change sections 1, 5, 6, or 7.
```

If the ERD is missing entities:

```
The ERD is missing the Notification entity.
Add it to the data schema with: id, user_id (FK), message, read (bool), created_at.
Relationships: Notification belongs to User.
```

---

## What You Built

| Artifact | Location |
|----------|----------|
| Tech stack decision | recorded in docs/TSD.md section 2 |
| Technical Specification Document | `docs/TSD.md` |

---

| | Navigation |
|---|---|
| **Produces** | `docs/TSD.md` — chosen stack, ERD, API table; consumed by Exercises 04 and 05 |
| **← Previous** | [Exercise 02: Functional Requirements](exercise-02-frd-agent-skills.md) |
| **Next →** | [Exercise 04: Generate Copilot Instructions →](exercise-04-impl-plan-background-agent.md) |

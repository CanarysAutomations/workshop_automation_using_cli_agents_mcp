# TaskFlow — Product Requirements

> **This is the starting point for the entire workshop.**  
> BRD → FRD → TSD → Implementation Plan → Code → Tests all derive from this file.  
> Do not modify it — treat it as a signed-off product brief.

---

## 1. Product Overview

**Product Name:** TaskFlow  
**Type:** Greenfield SaaS — Task & Project Management  
**Target Users:** Small engineering teams (5–20 people)  
**MVP Timeline:** 90 days from kickoff  
**Team Size:** 1–2 backend engineers

### The Problem

Engineering teams lose **2–4 hours per week** synchronising task status across Slack threads, personal spreadsheets, and ad-hoc email chains. There is no single source of truth for:
- What is being worked on
- Who owns each piece of work
- When it is due and what its current status is

### The Solution

A lightweight, web-based task management API that gives teams one place to create projects, assign tasks, track status, and see a team dashboard — with no setup friction.

---

## 2. Core Capabilities

### C1 — User & Team Management
- Users self-register with email + password
- Users are invited into teams (orgs) by an Admin
- Two roles: **Admin** (manages team, creates projects) and **Member** (creates and updates tasks)
- Password reset via email link
- A user can belong to multiple teams

### C2 — Project Management
- Admins create projects with name and description
- Projects are scoped to exactly one team
- Project status: `Active` | `On Hold` | `Archived`
- All members of a team can view active projects
- Admins can archive or reactivate projects

### C3 — Task Management
- Members create tasks inside a project
- **Task fields:**
  - Title *(required)*
  - Description *(optional)*
  - Assignee — one team member *(required)*
  - Due Date *(required)*
  - Priority — `Low` | `Medium` | `High` *(required)*
  - Status *(see lifecycle below)*
- **Status lifecycle:** `Todo → In Progress → Under Review → Done`
  - Any member can move a task forward one step
  - Admins can move tasks backward (reopen)
- Tasks can be reassigned and have their due dates changed
- Tasks can be filtered by: assignee, status, priority, due date range

### C4 — Notifications *(in-app only for MVP)*
- Assignee notified when a task is assigned to them
- Assignee notified when a task due date is < 24 hours away
- Notification marked as read when viewed
- **Out of MVP scope:** email, push, Slack notifications

### C5 — Dashboard
- **My Tasks view** — all tasks assigned to the logged-in user, sorted by due date ascending
- **Per-Project view** — task counts grouped by status for one project
- **Team view** — all open tasks (Todo + In Progress) across all team projects, sorted by priority descending

---

## 3. Non-Functional Requirements

| Category | Requirement |
|----------|-------------|
| **Performance** | API p95 response time < 300ms under 100 concurrent users |
| **Availability** | 99.5% uptime during business hours (08:00–20:00 UTC) |
| **Security** | Passwords: bcrypt (cost ≥ 12). All endpoints require JWT auth except `/register` and `/login` |
| **Scalability** | Stateless API — scale horizontally via container replicas |
| **Database** | PostgreSQL only. No analytics store or caching layer for MVP |

---

## 4. Data Entities (summary for TSD)

| Entity | Key Fields |
|--------|-----------|
| **User** | id, email, password_hash, created_at |
| **Team** | id, name, created_by (User), created_at |
| **TeamMember** | team_id, user_id, role (admin\|member) |
| **Project** | id, team_id, name, description, status, created_by, created_at |
| **Task** | id, project_id, title, description, assignee_id, due_date, priority, status, created_by, updated_at |
| **Notification** | id, user_id, task_id, type, is_read, created_at |

---

## 5. API Surface (summary for FRD → TSD mapping)

| Feature | Methods | Base Path |
|---------|---------|-----------|
| Auth | POST | `/auth/register`, `/auth/login`, `/auth/refresh` |
| Teams | GET, POST | `/teams` |
| Team membership | GET, POST, DELETE | `/teams/:id/members` |
| Projects | GET, POST, PATCH, DELETE | `/projects` |
| Tasks | GET, POST, PATCH, DELETE | `/projects/:id/tasks` |
| Task status | PATCH | `/tasks/:id/status` |
| Notifications | GET, PATCH | `/notifications` |
| Dashboard | GET | `/dashboard/my-tasks`, `/dashboard/project/:id`, `/dashboard/team/:id` |

---

## 6. Out of Scope (MVP)

- File or image attachments on tasks
- Time tracking or time logging
- Gantt charts, roadmaps, or calendar views
- Third-party integrations (GitHub Issues, Jira, Slack, email)
- Mobile native apps — web API only
- Audit log / activity history
- Custom task fields or workflows

---

## 7. Constraints

| Constraint | Detail |
|-----------|--------|
| Open-source only | No proprietary paid libraries or services |
| Deployment | Single Dockerfile; deploy to one cloud VM or container for MVP |
| Database | PostgreSQL — no NoSQL, no SQLite in production |
| Auth | JWT (stateless) — no session cookies |

---

## 8. Success Metrics

| Metric | 30-day target | 90-day target | 6-month target |
|--------|--------------|---------------|----------------|
| Active teams | 50 | 200 | 500 |
| Weekly active users / team | ≥ 3 | ≥ 5 | ≥ 8 |
| Tasks created / team / week | ≥ 10 | ≥ 20 | ≥ 30 |
| API error rate | < 1% | < 0.5% | < 0.2% |

---

## How This File Drives the Workshop

```
REQUIREMENTS.md  ←  you are here
      │
      ├── Exercise 01 → BRD.md        (custom agent reads C1–C5, Section 8)
      ├── Exercise 02 → FRD.md        (skill reads BRD + Section 5 API surface)
      ├── Exercise 03 → TSD.md        (cloud agent reads FRD + Sections 3–5)
      ├── Exercise 04 → IMPL_PLAN.md  (background agent reads TSD + FRD)
      ├── Exercise 05 → src/          (CLI reads TSD tech stack decision)
      ├── Exercise 06 → tests/        (background agent reads src/ structure)
      └── Exercise 07 → quality-gate  (CLI enforces NFRs from Section 3)
```

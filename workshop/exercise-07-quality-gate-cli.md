# Exercise 07: Quality Gate with Copilot CLI

| | Exercise 07 Overview |
|---|---|
| **Time** | ~10 minutes |
| **Copilot Feature** | Copilot CLI (`gh copilot suggest` / `gh copilot explain`) |
| **Type** | ⏴ Optional |
| **You Will** | Use CLI to generate and run a quality gate script — coverage threshold, ESLint, and npm security audit — then ask CLI to explain and fix every failure |
| **Input** | TaskFlow project with Jest tests from Exercise 06 |
| **Output** | `quality-gate.sh` script with all gates passing |
| **Next** | Workshop complete ✅ |

## Workshop Progress

> [01 BRD](exercise-01-brd-custom-agent.md) → [02 FRD](exercise-02-frd-agent-skills.md) → [03 TSD](exercise-03-tsd-cloud-agent.md) → [04 Instructions](exercise-04-impl-plan-background-agent.md) → [05 Scaffold](exercise-05-scaffold-cli.md) → [06 Tests](exercise-06-tests-background-agent.md) → `07 Gate ⚪`

---

## Goal

Use **Copilot CLI** to enforce coverage thresholds, lint rules, and a security audit — then ask CLI to explain and fix every failure before shipping.

---

## ⚡ Starting Here?

This exercise requires a Node.js project with Jest. If you don’t have one from earlier exercises, run:

```bash
mkdir -p src tests && npm init -y
npm install --save-dev jest
npx jest --init   # answer prompts to create jest.config.js
```

Then continue from step 7.1.

---

## 7.1 Run Coverage Gate

**1.** Ask CLI how to enforce an 80% coverage threshold:

> **CLI Prompt — Coverage Gate** *(run in terminal)*

```bash
gh copilot suggest "Run Jest with coverage and fail the command if statement coverage drops below 80%"
```

**2.** Run the suggested command. If coverage fails, continue to step 7.2.

---

## 7.2 🐛 Debug a Failing Test with CLI

If the coverage run fails, copy the error and ask CLI to explain it:

> **CLI Prompt — Explain Test Error** *(run in terminal)*

```bash
gh copilot explain "Jest error: Cannot find module '../config/db' 
from 'tests/unit/user.model.test.js'"
```

CLI explains the import resolution. Apply the fix, re-run.

> **Why CLI not Chat?** CLI `explain` gives you a runnable fix as a shell command — Chat gives prose. Use CLI when the fix is a file path, config change, or npm install.

---

## 7.3 Lint Check

**1.** Ask CLI to add ESLint:

> **CLI Prompt — Set Up ESLint** *(run in terminal)*

```bash
gh copilot suggest "Set up ESLint for a Node.js Express project with no framework preset, 
enable no-unused-vars and no-console rules, add a lint script to package.json"
```

**2.** Run the suggested setup commands.

**3.** Run the linter:

```bash
npm run lint
```

**4.** If lint errors appear, ask CLI to auto-fix:

> **CLI Prompt — Auto-Fix Lint Errors** *(run in terminal)*

```bash
gh copilot suggest "Fix all auto-fixable ESLint errors in the src/ directory"
```

---

## 7.4 Security Audit

> **CLI Prompt — Security Audit** *(run in terminal)*

```bash
gh copilot suggest "Run npm audit and fail if any high or critical vulnerabilities exist"
```

Run the command and review the output. If high vulnerabilities are found:

> **CLI Prompt — Fix Vulnerabilities** *(run in terminal)*

```bash
gh copilot suggest "Fix high severity npm audit vulnerabilities automatically"
```

---

## 7.5 Generate a Gate Summary

Ask CLI to combine all checks into a single gate script:

> **CLI Prompt — Generate Quality Gate Script** *(run in terminal)*

```bash
gh copilot suggest "Create a shell script quality-gate.sh that runs in sequence: 
npm test with 80% coverage threshold, npm run lint, npm audit --audit-level=high. 
Exit with code 1 on any failure and print which gate failed."
```

Run the suggested output script:

```bash
chmod +x quality-gate.sh
./quality-gate.sh
```

---

## Expected Final Output

```
✅ Tests passed — coverage 83%
✅ Lint passed — 0 errors
✅ Audit passed — 0 high/critical vulnerabilities

Quality gate: PASSED
```

---

## What You Built

| Artifact | Location |
|----------|----------|
| Coverage-enforced test run | `npm test` |
| ESLint config | `.eslintrc.js` |
| Quality gate script | `quality-gate.sh` |

---

## 🎉 Workshop Complete

You just ran the full AI-driven SDLC — idea to tested, quality-gated application:

| Exercise | Artifact | Copilot Feature Used |
|----------|----------|----------------------|
| [01 BRD](exercise-01-brd-custom-agent.md) | `docs/BRD.md` | Local Custom Agent (`sdlc-agent`) |
| [02 FRD](exercise-02-frd-agent-skills.md) | `docs/FRD.md` | Agent Skills + Local Custom Agent |
| [03 TSD](exercise-03-tsd-cloud-agent.md) | `docs/TSD.md` + your stack decision | Local Custom Agent (`sdlc-agent`) |
| [04 Instructions](exercise-04-impl-plan-background-agent.md) | `.github/copilot-instructions.md` | Local Custom Agent (`sdlc-agent`) |
| [05 Scaffold](exercise-05-scaffold-cli.md) | `src/` project tree | Copilot CLI |
| [06 Tests](exercise-06-tests-background-agent.md) | `tests/` suite, coverage report | Background Agent |
| [07 Quality Gate](exercise-07-quality-gate-cli.md) | `quality-gate.sh` | Copilot CLI |

---

| | Navigation |
|---|---|
| **← Previous** | [Exercise 06: Tests + Debug Failures](exercise-06-tests-background-agent.md) |
| **Start over** | [Back to README](../README.md) |
| **Workshop complete** | All mandatory exercises done — review `docs/` for your full SDLC artefact chain |

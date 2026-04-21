# SKILLS.md — Riferimento delle Skill

> La conoscenza delle skill è incorporata **inline in ogni file TOOLS.md dei singoli agenti**.
> Questo file è un riferimento rapido per tutte le skill e le informazioni di download.
> Fonti delle skill con URL: vedi `SHARED_CONFIG.md`.

---

## Scoperta delle Skill (Skill Discovery)

```bash
skills search "<argomento>"
skills install <nome-skill>
# Oppure: curl -sL https://raw.githubusercontent.com/obra/superpowers/main/skills/<nome>/SKILL.md
```

---

## Le 23 Skill Principali — Riferimento Rapido

### Superpowers (obra) — Metodologia Core

| Skill | Regola Cardine | Agenti |
|-------|-----------|--------|
| `systematic-debugging` | 4 Fasi: Root Cause (Causa Radice) → Pattern → Ipotesi → Fix. **Nessun fix senza causa radice.** | Tutti |
| `test-driven-development` | RED (Fallimento) → Verifica RED → GREEN (Successo) → Verifica GREEN → REFACTOR. Un solo comportamento per test. | Unit Test Writer, Builder |
| `verification-before-completion` | Gate a 5 step: Identifica → Esegui → Leggi → Verifica → Conferma. **Nessun "fatto" senza prove.** | Tutti |
| `writing-plans` | Contesto zero, Task piccoli (2-5 min), Struttura file prima, Sintassi checkbox. | Gatekeeper, Orchestrator |
| `executing-plans` | Carica → Esegui (in_progress → completed) → Finisci. STOP in caso di blocchi. | Builder |
| `brainstorming` | Raffinamento Socratico: 1 domanda/messaggio → 2-3 approcci → Design → Spec → Review. | Gatekeeper, UX |
| `subagent-driven-development` | Per ogni task: Implementatore → Spec-Review → Code-Quality-Review (3 round). | Orchestrator |
| `dispatching-parallel-agents` | Identifica Task Indipendenti → Crea Task → Invia in Parallelo → Revisiona e Integra. | Orchestrator, QA |
| `finishing-a-development-branch` | Verifica Test → Base Branch → Opzioni di Merge → Esegui → Pulizia Worktree. | Builder |
| `requesting-code-review` | Dopo ogni task: SHA → Invia ai Reviewer → Correggi subito le criticità. | Builder, QA |
| `receiving-code-review` | LEGGI → CAPISCI → VERIFICA → VALUTA → RISPONDI → IMPLEMENTA. Mai rispondere "Ottimo punto!". | Builder |
| `using-git-worktrees` | Isolamento delle feature: `git worktree add ../wt-<nome> -b feat/<name>` | Git WF Mgr, Builder |
| `using-superpowers` | Priorità: Istruzioni Utente > Skill > System Prompt. | Tutti |

### Vercel Labs / skills.sh — Frontend & Design

| Skill | Regola Cardine | Agenti |
|-------|-----------|--------|
| `vercel-react-best-practices` | `Promise.all()`, niente Barrel File, `next/dynamic`, Server Components come default. | Frontend Builder |
| `web-design-guidelines` | Scarica linee guida da Vercel → Verifica rispetto a tutte le regole → Output `file:linea`. | Design Auditor |
| `frontend-design` | Tipografia: mai usare font di sistema. Colore: Dominante + Accenti. Motion: Sfalsato (Staggered). | Design Architect |
| `agent-browser` | `open` → `snapshot -i` → `screenshot` → `set viewport` → `close`. | E2E, Design Auditor |
| `next-best-practices` | App Router, Server Components, `loading.tsx` + `error.tsx`, Metadata API. | Frontend Builder |
| `ui-ux-pro-max` | Contrasto ≥4.5:1, Touch ≥44px, Focus Ring, Gerarchia degli Heading, `prefers-reduced-motion`. | Design Architect |
| `webapp-testing` | Test Server → `curl`. Test Visuali → `agent-browser`. Ricognizione prima dell'azione. | E2E, QA |

### Specializzate

| Skill | Regola Cardine | Agenti |
|-------|-----------|--------|
| `supabase-postgres` | RLS sempre attivo, Index sulle FK, Enum, Prepared Statement, PgBouncer. | Backend Builder |
| `typescript-advanced-types` | Discriminated Unions, Generics, `satisfies`, Type Guards, Utility Types. | Frontend Builder |

---

## Flusso di Lavoro Superpowers → Mappatura Agenti

```
1. brainstorming        → Gatekeeper + UX Researcher
2. using-git-worktrees  → Git Workflow Manager
3. writing-plans        → Gatekeeper → Orchestrator
4. subagent-driven-dev  → Orchestrator → Builder + QA
5. test-driven-dev      → Unit Test Writer + Builder
6. requesting-review    → Orchestrator → Reviewer
7. finishing-branch     → Builder → Gatekeeper
```

Sempre attivo: `systematic-debugging` (per i bug) · `verification-before-completion` (prima della consegna)

---

## Ordine di Caricamento del Contesto

```
1. GOAL.md          → Qual è l'obiettivo?
2. SYSTEM_STATE.md  → Cosa esiste già?
3. MEMORY.md        → Cosa abbiamo imparato?
4. SHARED_CONFIG.md → Stack, Regole
5. Propri TOOLS.md   → Skill specifiche per l'agente
```

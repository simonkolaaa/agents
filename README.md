# 🤖 Paperclip AI Agent System

> **30 Agenti IA** per lo sviluppo software completo — dall'idea al deploy.

---

## Avvio Rapido

Ogni agente ha 4 file fondamentali: 
- `SOUL.md` (Persona/Carattere) 
- `AGENTS.md` (Ruolo/Flusso di lavoro) 
- `TOOLS.md` (Competenze/Skill) 
- `HEARTBEAT.md` (Checklist di controllo)

Regole globali: `SHARED_CONFIG.md` · Panoramica agenti: `AGENTS_OVERVIEW.md`

---

## Architettura

```
CEO → Product Owner → Scrum Master
  └→ Architecture Gatekeeper
       ├→ Feature Orchestrator → UX → Design → Build → QA → Docs → Deploy
       ├→ Stack Researcher, Code Quality, Docs Manager
       ├→ DevOps → K8s, Git Workflow, Performance
       └→ Security Auditor, Spec Reviewer
```

---

## I 30 Agenti per Area

### Leadership (Direzione)
CEO · Product Owner · Scrum Master · Architecture Gatekeeper

### Design & Ricerca
UX Researcher · Design Architect · Stack Researcher

### Build (Sviluppo)
Feature Orchestrator · Frontend Builder · Backend Builder

### Qualità & Testing
QA Orchestrator · Unit Test Writer · Design Auditor · E2E Tester · VM Tester · Testability Expert · Validation Expert · Code Quality Expert

### Infrastruttura
DevOps Expert · Kubernetes Expert · Browser Automation · Docs Manager

### Specialisti 🆕
Systematic Debugger · Spec Reviewer · Git Workflow Manager · Security Auditor · Performance Optimizer · Accessibility Expert

---

## Ciclo di Vita delle Funzionalità (21 Passaggi)

```
BACKLOG → GOAL → SPEC REVIEW → PRD → API_SPEC → RESEARCH
→ UX_SPEC → DESIGN_SPEC → VALIDATION → BRANCH → CODE
→ SECURITY → PERFORMANCE → ACCESSIBILITY → QA → QUALITY GATE
→ DOCS → MERGE → DEPLOY → SCORECARD
```

---

## Metodologia

| Fonte | Tecnica |
|--------|---------|
| [obra/superpowers](https://github.com/obra/superpowers) | TDD, Debugging a 4 fasi, Evidenza di Verifica |
| [pbakaus/impeccable](https://github.com/pbakaus/impeccable) | OKLCH, Griglia a 4pt, AI Slop Test |
| [skills.sh](https://skills.sh) | Oltre 60 Skill da 17 repository |

---

## Tech Stack (Tecnologie)

Next.js 15 · React 19 · shadcn/ui · Tailwind 4 · Zustand · Zod · Drizzle · Supabase · Vitest · Playwright

---

## Principi Cardine

1.  **Controllo Obiettivo** — Leggere sempre `GOAL.md` come prima cosa.
2.  **Evidenza prima di tutto** — Fornire prove concrete prima di fare affermazioni.
3.  **TDD (Test Driven Development)** — Nessun codice senza un test che fallisce preventivamente.
4.  **HARD-GATE** — Nessun codice viene scritto senza l'approvazione del Design/Architettura.
5.  **Circuit Breaker** — Massimo 3 iterazioni, poi escalation del problema.
6.  **Recupero Errori** — Risoluzione: Sè stessi → Collega → Gatekeeper.

---

📚 Lista dettagliata Agenti: [AGENTS_OVERVIEW.md](AGENTS_OVERVIEW.md) · Regole: [SHARED_CONFIG.md](SHARED_CONFIG.md) · Skill: [SKILLS.md](SKILLS.md)

---

## Personal Mode (Simon)

Questo sistema di agenti è configurato per il flusso di lavoro di uno studente con standard professionali:

- **Python + Flask** sono la base predefinita per l'implementazione.
- **React/TypeScript, Rust e Go** sono i percorsi di apprendimento attivo.
- Gli agenti lavorano in modalità **Tutor + Pair-programmer**.
- Per le decisioni architettoniche, gli agenti devono discutere le opzioni prima di implementare, previa approvazione.
- Il livello qualitativo rimane alto: sono richiesti test, controlli di sicurezza e registrazione delle decisioni.

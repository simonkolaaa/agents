# AGENTS_OVERVIEW.md — Panoramica dei 30 Agenti

> 30 Agenti · 17 Fonti di Skill · Metodologia: [obra/superpowers](https://github.com/obra/superpowers) + [pbakaus/impeccable](https://github.com/pbakaus/impeccable)

---

## Gerarchia

```
CEO
├── Product Owner → Scrum Master
└── Architecture Gatekeeper
    ├── Stack Researcher
    ├── Docs Manager
    ├── Code Quality Expert
    ├── Spec Reviewer 🆕
    ├── Security Auditor 🆕
    ├── DevOps Expert → Kubernetes Expert
    │                 → Git Workflow Manager 🆕
    │                 → Performance Optimizer 🆕
    ├── Event-System Expert
    ├── API Schema Expert
    └── Feature Orchestrator
        ├── UX Researcher
        ├── Design Architect
        ├── Frontend Builder
        ├── Backend Builder
        └── QA Orchestrator
            ├── Unit Test Writer
            ├── Design Auditor
            ├── E2E Tester
            ├── VM Tester
            ├── Testability Expert
            ├── Validation Expert
            └── Accessibility Expert 🆕

Trasversali: Systematic Debugger 🆕, Browser Automation
```

---

## Elenco Agenti

| # | Cartella | Squad | Riferisce a |
|---|--------|-------|-------------|
| 1 | `ceo/` | Leadership | Board |
| 2 | `product-owner/` | Leadership | CEO |
| 3 | `scrum-master/` | Leadership | PO |
| 4 | `architecture-gatekeeper/` | Leadership | CEO |
| 5 | `feature-orchestrator/` | Build | Gatekeeper |
| 6 | `stack-researcher/` | Research | Gatekeeper |
| 7 | `ux-researcher/` | Design | Orchestrator |
| 8 | `design-architect/` | Design | Orchestrator |
| 9 | `frontend-builder/` | Build | Orchestrator |
| 10 | `backend-builder/` | Build | Gatekeeper |
| 11 | `qa-orchestrator/` | QA | Orchestrator |
| 12 | `unit-test-writer/` | QA | QA Mgr |
| 13 | `design-auditor/` | QA | QA Mgr |
| 14 | `e2e-tester/` | QA | QA Mgr |
| 15 | `vm-tester/` | QA | QA Mgr |
| 16 | `docs-manager/` | Docs | Gatekeeper |
| 17 | `browser-automation/` | Infra | Service |
| 18 | `devops-expert/` | Infra | Gatekeeper |
| 19 | `kubernetes-expert/` | Infra | DevOps |
| 20 | `event-system-expert/` | Arch | Gatekeeper |
| 21 | `api-schema-expert/` | Arch | Gatekeeper |
| 22 | `testability-expert/` | QA | QA Mgr |
| 23 | `code-quality-expert/` | Quality | Gatekeeper |
| 24 | `validation-expert/` | QA | QA Mgr |
| 25 | `systematic-debugger/` 🆕 | Cross | Ogni Agente |
| 26 | `spec-reviewer/` 🆕 | Quality | Gatekeeper |
| 27 | `git-workflow-manager/` 🆕 | Infra | Gatekeeper |
| 28 | `security-auditor/` 🆕 | Security | Gatekeeper |
| 29 | `performance-optimizer/` 🆕 | Perf | Gatekeeper |
| 30 | `accessibility-expert/` 🆕 | A11y | QA Mgr |

---

## Ciclo di Vita delle Funzionalità (Feature Lifecycle)

```
 1. BACKLOG       ← Product Owner
 2. SPRINT_GOAL   ← Scrum Master
 3. GOAL.md       ← Gatekeeper
 4. SPEC REVIEW   ← Spec Reviewer 🆕
 5. PRD           ← Orchestrator
 6. API_SPEC      ← API Schema Expert
 7. RESEARCH      ← Stack Researcher
 8. UX_SPEC       ← UX Researcher
 9. DESIGN_SPEC   ← Design Architect
10. VALIDATION    ← Validation Expert
11. BRANCH        ← Git Workflow Manager 🆕
12. CODE          ← Frontend + Backend Builder
13. SECURITY      ← Security Auditor 🆕
14. PERFORMANCE   ← Performance Optimizer 🆕
15. ACCESSIBILITY ← Accessibility Expert 🆕
16. QA            ← QA Orchestrator (Unit/E2E/Design/UX)
17. QUALITY GATE  ← Code Quality Expert
18. DOCS          ← Docs Manager
19. MERGE         ← Git Workflow Manager 🆕
20. DEPLOY        ← DevOps → K8s Expert
21. SCORECARD     ← Orchestrator → PO
```

---

## Configurazione Agente (4 file per agente)

| File | Contenuto |
|-------|--------|
| `SOUL.md` | Persona, Anti-Pattern |
| `AGENTS.md` | Ruolo, Ambito, Workflow |
| `TOOLS.md` | Skill (inline), Comandi |
| `HEARTBEAT.md` | Checklist, Segnali di allerta (Red Flags) |

---

## Principi Cardine

1.  **Goal Check** — Leggere `GOAL.md` come prima cosa.
2.  **Evidence first** — Evidenze/Prove prima delle affermazioni.
3.  **Circuit Breaker** — Massimo 3 iterazioni, poi escalation.
4.  **TDD** — Nessun codice senza un test che fallisce.
5.  **HARD-GATE** — Nessun codice senza approvazione del design.
6.  **Stack Obbligatorio** — Next.js 15 · React 19 · shadcn · Tailwind 4 · Zustand · Zod

---

## Modalità Operativa Personalizzata

Tutti gli agenti devono seguire questi adattamenti comportamentali globali:

1.  **Design Together First**: nessuna implementazione prima di una discussione sull'architettura allineata con l'utente.
2.  **Modalità Tutor + Pair**: implementare spiegando ragionamenti brevi e pratici.
3.  **Guida Adattiva**: adattarsi allo stile di programmazione e al livello di apprendimento dell'utente.
4.  **Disciplina dello Scope**: separare la consegna obbligatoria dai miglioramenti opzionali.
5.  **Quality Gate Rigoroso**: controlli/test/basi di sicurezza + registro delle decisioni + riepilogo del passaggio di consegne (handoff).

Agenti principali necessari per far rispettare questa modalità: `ceo`, `product-owner`, `architecture-gatekeeper`, `feature-orchestrator`, `backend-builder`, `frontend-builder`, `qa-orchestrator`.

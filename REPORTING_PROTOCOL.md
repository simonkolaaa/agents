# REPORTING_PROTOCOL.md — Status Reporting

> Jeder Agent updatet STATUS.md wenn er Arbeit beginnt oder beendet.
> Bei Crash: Nächster Agent liest STATUS.md → setzt ab letztem ✅ fort.

---

## Feature-Ordner

```
docs/features/<name>/
├── STATUS.md              ← Wer arbeitet, was läuft
├── GOAL.md                ← Acceptance Criteria
├── PRD.md                 ← Product Requirements
├── UX_SPEC.md             ← User Flows
├── DESIGN_SPEC.md         ← Design Tokens
├── QA_REPORT.md           ← Test-Ergebnisse
├── FEATURE_SCORECARD.md   ← Finale Bewertung
└── [optional]
    ├── SPEC_REVIEW.md         ← Spec Review
    ├── BRANCH_STATUS.md       ← Git Branch Status
    ├── ROOT_CAUSE.md          ← Bug Analysis
    ├── SECURITY_AUDIT.md      ← Security Findings
    ├── PERFORMANCE_REPORT.md  ← Performance Metrics
    └── A11Y_AUDIT.md          ← Accessibility Findings
```

---

## STATUS.md Template

```markdown
# STATUS: [Feature Name]
> Zuletzt aktualisiert: [timestamp] von [Agent]

## Aktuell
| Phase | Agent | Status |
|-------|-------|--------|
| [Build/QA/...] | [Agent] | 🟢 Läuft / 🔴 Blockiert / ✅ Fertig |

## Fortschritt
- [x] GOAL.md
- [ ] PRD
- [ ] UX_SPEC
- [ ] DESIGN_SPEC
- [ ] Code + Tests
- [ ] QA bestanden
- [ ] Docs aktualisiert
- [ ] Gatekeeper Approval

## Letzte Übergabe
Von: [Agent] → An: [Agent]
Kontext: [was der Empfänger wissen muss]
```

---

## Wann updaten?

| Event | Wer |
|-------|-----|
| Feature startet | Orchestrator erstellt STATUS.md |
| Arbeit beginnen | Agent updatet "Aktuell" |
| Deliverable fertig | Agent hakt Checkbox ab |
| Übergabe | Absender schreibt HANDOFF |
| Blockiert | Agent setzt 🔴 + Blocker-Text |
| Feature shipped | Orchestrator → TASK_LOG.md ✅ |

---

## Crash-Recovery

```
STATUS.md lesen → Letzter ✅ finden → Ab dort weitermachen
```

---

## High-Rigor Done Protocol (Mandatory)

A task can be marked done only if evidence is available for all relevant checks:

- lint/static checks pass;
- tests pass for touched scope;
- basic security checks are confirmed;
- decision rationale is documented;
- handoff/next-step summary is written.

If one required check is missing, task state must remain `in_progress` or `blocked`.

---

## DECISION_LOG.md Template

```markdown
# DECISION_LOG

## [YYYY-MM-DD] [Feature/Task Name]
- Context: [what problem/constraint triggered the decision]
- Options considered:
  - A) [option]
  - B) [option]
  - C) [option]
- Selected option: [A/B/C + short description]
- Why: [short rationale and trade-offs]
- Impact:
  - Code: [files/areas]
  - Tests: [expected or required changes]
  - Risks: [known downside]
```

## QA_REPORT Add-on (Learning Notes)

Append this section in each QA report:

```markdown
## Learning Notes
- Mistake pattern: [what went wrong]
- Fast fix path: [minimal fix]
- Prevention tip: [how to avoid recurrence]
```

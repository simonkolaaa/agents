# REPORTING_PROTOCOL.md — Reporting dello Stato

> Ogni agente aggiorna `STATUS.md` quando inizia o finisce un lavoro.
> In caso di crash: l'agente successivo legge `STATUS.md` → riprende dall'ultimo ✅.

---

## Cartella della Feature

```
docs/features/<nome>/
├── STATUS.md              ← Chi lavora, cosa è in corso
├── GOAL.md                ← Criteri di Accettazione (AC)
├── PRD.md                 ← Requisiti di Prodotto
├── UX_SPEC.md             ← Flussi Utente (User Flows)
├── DESIGN_SPEC.md         ← Design Token
├── QA_REPORT.md           ← Risultati dei Test
├── FEATURE_SCORECARD.md   ← Valutazione finale
└── [opzionale]
    ├── SPEC_REVIEW.md         ← Spec Review
    ├── BRANCH_STATUS.md       ← Stato dei Branch Git
    ├── ROOT_CAUSE.md          ← Analisi del Bug
    ├── SECURITY_AUDIT.md      ← Risultati di Sicurezza
    ├── PERFORMANCE_REPORT.md  ← Metriche di Performance
    └── A11Y_AUDIT.md          ← Risultati Accessibilità
```

---

## Template di STATUS.md

```markdown
# STATUS: [Nome Feature]
> Ultimo aggiornamento: [timestamp] da [Agente]

## Attuale
| Fase | Agente | Stato |
|-------|-------|--------|
| [Build/QA/...] | [Agente] | 🟢 In corso / 🔴 Bloccato / ✅ Completato |

## Progressi
- [x] GOAL.md
- [ ] PRD
- [ ] UX_SPEC
- [ ] DESIGN_SPEC
- [ ] Codice + Test
- [ ] QA superato
- [ ] Docs aggiornati
- [ ] Approvazione Gatekeeper

## Ultimo Handoff (Passaggio Consegne)
Da: [Agente] → A: [Agente]
Contesto: [cosa deve sapere il ricevente]
```

---

## Quando aggiornare?

| Evento | Chi |
|-------|-----|
| Inizio Feature | L'Orchestrator crea `STATUS.md` |
| Inizio lavoro | L'agente aggiorna "Attuale" |
| Deliverable pronto | L'agente spunta la casella (checkbox) |
| Handoff | Il mittente scrive l'HANDOFF |
| Bloccato | L'agente imposta 🔴 + motivo del blocco |
| Feature rilasciata | L'Orchestrator segna ✅ in `TASK_LOG.md` |

---

## Recupero dopo Crash (Crash-Recovery)

```
Leggi STATUS.md → Trova l'ultimo ✅ → Riprendi da lì
```

---

## Protocollo "Fatto" ad Alto Rigore (Obbligatorio)

Un compito può essere segnato come completato solo se è disponibile l'evidenza per tutti i controlli rilevanti:

- controlli lint/statici superati;
- test superati per lo scope interessato;
- controlli di sicurezza base confermati;
- logica delle decisioni documentata;
- scritto il riepilogo handoff/prossimo passo.

Se manca un solo controllo richiesto, lo stato del task deve rimanere `in_progress` o `blocked`.

---

## Template di DECISION_LOG.md

```markdown
# DECISION_LOG

## [AAAA-MM-GG] [Nome Feature/Task]
- Contesto: [quale problema/vincolo ha generato la decisione]
- Opzioni considerate:
  - A) [opzione]
  - B) [opzione]
  - C) [opzione]
- Opzione scelta: [A/B/C + breve descrizione]
- Perché: [breve razionale e compromessi - trade-offs]
- Impatto:
  - Codice: [file/aree coinvolte]
  - Test: [modifiche attese o richieste]
  - Rischi: [svantaggi noti]
```

---

## Add-on QA_REPORT (Note di Apprendimento)

Aggiungi questa sezione in ogni report QA:

```markdown
## Note di Apprendimento
- Pattern d'errore: [cosa è andato storto]
- Percorso di correzione rapida: [fix minimale]
- Suggerimento preventivo: [come evitare che si ripeta]
```

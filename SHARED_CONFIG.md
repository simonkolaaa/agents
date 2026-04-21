# SHARED_CONFIG.md — Configurazione Centrale per tutti gli Agenti

> Questo file viene letto da OGNI agente. Le modifiche qui influenzano tutti.
> Ultimo aggiornamento: 2026-03-13 (Skill Registry, Ragionamento Avanzato, Recupero Errori, 30 Agenti)

---

## Runtime
- **OpenCode** è il runtime degli agenti.
- Tutti gli agenti hanno accesso alla Shell, a Internet e ai server MCP.

## API Paperclip

| Endpoint | Metodo | Scopo |
|----------|--------|-------|
| `/api/agents/me` | GET | Identità dell'Agente |
| `/api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked` | GET | Posta in arrivo dei compiti |
| `/api/issues/{issueId}` | PATCH | Aggiornamenti di stato (incl. header `X-Paperclip-Run-Id`) |
| `/api/companies/{companyId}/issues` | POST | Creazione subtask (con `parentId` + `goalId`) |

---

## Stack Obbligatorio (Mandated Stack)

| Livello | Tecnologia | Riferimento |
|-------|-------------|----------|
| Framework | Next.js 15 (App Router) | `/vercel/next.js` |
| Libreria UI | React 19 | `/facebook/react` |
| Componenti UI | shadcn/ui | `/shadcn-ui/ui` |
| Stile (CSS) | Tailwind CSS 4 | `/tailwindlabs/tailwindcss` |
| Stato (Client) | Zustand (con persist + devtools) | `/pmndrs/zustand` |
| Stato (Server) | TanStack React Query | `/TanStack/query` |
| Validazione | Zod | `/colinhacks/zod` |
| Form | React Hook Form + Zod Resolver | `/react-hook-form/react-hook-form` |
| Icone | lucide-react | — |
| Animazioni | Framer Motion | — |
| Client HTTP | ky | — |
| Toast | Sonner | — |

> La colonna Riferimento contiene gli ID Context7 per la documentazione aggiornata.
> Questo stack **NON è negoziabile**. Ottimizza ALL'INTERNO di esso.

### Stack Backend

| Livello | Tecnologia | Riferimento |
|-------|-------------|----------|
| ORM | Drizzle ORM | `/drizzle-team/drizzle-orm` |
| Migrazioni | drizzle-kit | — |
| Database | Supabase (PostgreSQL) | `/supabase/supabase` |
| Autenticazione | Supabase Auth / better-auth | `/supabase/supabase` |
| SSR Auth | @supabase/ssr | — |
| Logging | pino | — |
| IDs | nanoid | — |

> Lo stack backend si applica a tutti i lavori su API/DB. Viene imposto dal Backend Builder.

### Obiettivi di Copertura Test (Quality Gate)

| Metrica | Minimo | Raccomandato |
|--------|---------|----------|
| Statement | 80% | 90% |
| Branch | 75% | 85% |
| Funzioni | 80% | 90% |
| Linee | 80% | 90% |

> La copertura viene misurata con `npx vitest run --coverage`.
> Le funzionalità NON possono essere rilasciate se la copertura scende sotto il minimo.
> Il QA Orchestrator verifica la copertura come parte del file `QA_REPORT.md`.

---

## Server MCP

### Context7 — Documentazione Librerie Aggiornata
```json
{
  "context7": {
    "command": "npx",
    "args": ["-y", "@upstash/context7-mcp"]
  }
}
```
**Strumenti:** `resolve-library-id`, `get-library-docs`
**Quando:** Scaricare i docs aggiornati prima di ogni implementazione → salvarli in `docs/lib/`

### Firecrawl — Web Scraping & Crawling
```json
{
  "firecrawl": {
    "command": "npx",
    "args": ["-y", "firecrawl-mcp"],
    "env": { "FIRECRAWL_API_KEY": "<key>" }
  }
}
```
**Auto-Install:** `which firecrawl || npm install -g firecrawl`

---

## Regole Condivise (per TUTTI gli Agenti)

### 0. 🔍 Scoperta del Contesto (Context Discovery - PRIMO passo obbligatorio)

> **Prima di fare qualsiasi cosa: Leggi cosa è già presente.**
> **Se manca un file: Crealo partendo dal template.**

```
PASSO 0 — CONTEXT DISCOVERY (OBBLIGATORIO per ogni agente ad ogni avvio)

1. Verifica: Esiste `../../SYSTEM_STATE.md`?
   ├── SÌ → LEGGERE. Ora sai cosa esiste nel sistema.
   └── NO → Crealo dal template (vedi struttura cartelle progetto SHARED_CONFIG).

2. Verifica: Esiste `../../MEMORY.md`?
   ├── SÌ → LEGGERE. Ora conosci i problemi noti (gotchas) e i pattern.
   └── NO → Crealo dal template.

3. Verifica: Esiste `../../TASK_LOG.md`?
   ├── SÌ → LEGGERE. Sai cosa è attivo, bloccato o completato.
   └── NO → Crealo dal template.

4. Verifica: Esiste `docs/features/<feature-attuale>/STATUS.md`?
   ├── SÌ → LEGGERE. Sai a che punto è la feature e chi ha fatto cosa per ultimo.
   └── NO → La feature è nuova, l'Orchestrator crea la cartella.

5. Verifica: Esiste `docs/lib/`?
   ├── SÌ → Verifica se ci sono i docs per le tue librerie. LEGGERE.
   └── NO → Crea la cartella, chiedi allo Stack Researcher i docs Context7.

6. Leggi `../SHARED_CONFIG.md` — Stack, Regole, Server MCP.
7. Leggi `../SKILLS.md` — skill disponibili e conoscenza estratta.
8. Leggi `../REPORTING_PROTOCOL.md` — come riportare lo stato.
```

**Perché è importante:**
- L'agente inizia → recupera lo stato precedente → CONTINUA invece di ricominciare da zero.
- Se un agente crasha → l'agente successivo legge `STATUS.md` → subentra.
- Nessun agente lavora mai "al buio" senza contesto.

### 1. Controllo Obiettivo (Goal Check - Passo 0 mandatorio)
Ogni agente legge come PRIMA cosa il `GOAL.md` della feature. Tutte le azioni devono servire all'obiettivo.

### 2. Evidenze prima delle Affermazioni
Nessun agente può dire "fatto" senza prove:
- Builder: I test devono mostrare PASS.
- Tester: Screenshot + Log.
- Auditor: `REVIEW.md` con i risultati.
- Docs: Tutti i link verificati.

### 3. Circuit Breaker
Massimo 3 iterazioni per ogni fase (Gate). Dopo → Escalation all'Architecture Gatekeeper.

### 4. Protocollo di Passaggio Consegne (HANDOFF)
Formato standard per i passaggi tra agenti:
```markdown
# HANDOFF: [Da Agente] → [A Agente]
Feature: [nome]
Goal: [link a GOAL.md]
Deliverables: [cosa viene consegnato]
Contesto: [cosa deve sapere il ricevente]
Documentazione: [riferimenti docs/lib/]
```

### 5. Caricamento Skill (Skill Loading)

```bash
# Cerca + Installa
skills search "<argomento>"
skills install <nome-skill>

# Oppure direttamente da GitHub
curl -sL https://raw.githubusercontent.com/obra/superpowers/main/skills/<nome>/SKILL.md
```

### Fonti di Skill

| Fonte | GitHub | Top Skills |
|--------|--------|-----------|
| obra/superpowers | [GitHub](https://github.com/obra/superpowers) | TDD, Debugging, Piani, Verifica, Git, Subagent, Code Review |
| Vercel Labs | [skills.sh](https://skills.sh) | Best Practice React, Linee guida Design, Browser, Next.js |
| Anthropic | [GitHub](https://github.com/anthropics/skills) | Design Frontend, Canvas, Testing Webapp |
| pbakaus/impeccable | [GitHub](https://github.com/pbakaus/impeccable) | OKLCH, Griglia 4pt, Motion, AI Slop Test |
| supercent-io | [GitHub](https://github.com/supercent-io/agent-skills) | Sicurezza, Code Review, Design System |
| coreyhaines31 | [GitHub](https://github.com/coreyhaines31/marketingskills) | SEO, Strategia Contenuti, Analisi Competitor |
| google-labs-code | [GitHub](https://github.com/google-labs-code/stitch-skills) | Componenti React, Design |
| supabase | [GitHub](https://github.com/supabase/agent-skills) | Best Practice Postgres |
| nextlevelbuilder | [GitHub](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) | UI/UX Pro Max |
| browser-use | [GitHub](https://github.com/browser-use/browser-use) | Automazione Browser |
| better-auth | [GitHub](https://github.com/better-auth/skills) | Best Practice Autenticazione |
| currents-dev | [GitHub](https://github.com/currents-dev/playwright-best-practices-skill) | Playwright |
| wshobson | [GitHub](https://github.com/wshobson/agents) | TypeScript, Tailwind |
| sleekdotdesign | [GitHub](https://github.com/sleekdotdesign/agent-skills) | Design App Mobile |
| am-will | [GitHub](https://github.com/am-will/codex-skills) | Context7, Find-Skills |
| Intopia | [Website](https://intopia.digital) | Accessibilità Web (WCAG) |
| Trail of Bits | [Website](https://www.trailofbits.com) | Audit di Sicurezza |

> Le skill sono incorporate **inline in TOOLS.md**. Gli URL servono per approfondire o aggiornare.

### Priorità delle Skill
1. **Istruzioni Utente** → MASSIMA
2. **Skill** → Sovrascrivono i default
3. **System Prompt** → MINIMA

### 6. Tracciamento dello Stato (State Tracking)
- Dopo OGNI build: aggiornare `SYSTEM_STATE.md`.
- Prima di OGNI feature: leggere `SYSTEM_STATE.md`.

### 7. Ragionamento Avanzato (Advanced Reasoning)

Per compiti complessi:
- **Chain-of-Thought**: mostrare i passaggi del pensiero (Problema → Opzioni → Decisione).
- **ReAct**: alternare pensiero + azione (Ragiona → Agisci → Ragiona → Agisci).
- **Self-Refinement**: prima della consegna: È completo? Corretto? Minimale?

### 8. Recupero Errori (Error Recovery)

```
Livello 1: Risoluzione autonoma (max 3 tentativi)
Livello 2: Chiedere al Systematic Debugger
Livello 3: Impostare stato BLOCKED → Gatekeeper
```

### 9. Report dei Progressi
- Aggiornare `STATUS.md` all'inizio e alla fine del lavoro.
- `TASK_LOG.md` per la panoramica delle feature.
- In caso di crash: leggere `STATUS.md` → riprendere dall'ultimo ✅.

### 10. 🛡️ Protocollo Anti-Allucinazione (OBBLIGATORIO per OGNI agente)

> **Regola Ferrea: Nessun agente consegna senza essersi auto-controllato E senza essere controllato dal ricevente.**

#### A. STOP-CHECK-DELIVER (prima di ogni consegna)

Ogni agente DEVE rispondere a queste 3 domande prima di consegnare:

```
STOP: Il mio output è ESATTAMENTE quanto richiesto?
  1. Ho riletto GOAL.md / l'incarico? (Obbligatorio!)
  2. Il mio output contiene SOLO quanto richiesto? (Nessun extra!)
  3. Manca qualcosa che era stato richiesto? (Completezza!)

Se UNA sola risposta è NO → CORREGGI prima di consegnare.
```

#### B. Validazione Gerarchica (Il ricevente controlla SEMPRE)

```
L'agente consegna
    ↓
Il ricevente (gerarchia superiore) controlla:
  ├── Corrisponde all'incarico? → ✅ Accettato
  ├── Manca qualcosa? → 🔴 RIFIUTATO: "Manca AC #X"
  ├── C'è troppo materiale? → 🔴 RIFIUTATO: "Rimuovi [X], non richiesto"
  └── Diverso da quanto richiesto? → 🔴 RIFIUTATO: "Doveva essere [A], è [B]"
```

#### C. Regole Anti-Allucinazione specifiche per Agente

| Agente | Si controlla rispetto a | Viene controllato da |
|-------|------------------|-----------------|
| Stack Researcher | GOAL.md — cercare solo quanto richiesto | Gatekeeper / Orchestrator |
| UX Researcher | PRD — solo flussi per feature richieste | Orchestrator |
| Design Architect | UX_SPEC + PRD — disegnare solo schermate richieste | Orchestrator |
| Frontend Builder | DESIGN_SPEC + GOAL.md — costruire solo quanto disegnato | Orchestrator (Scope Gate) |
| Backend Builder | API_SPEC + GOAL.md — solo endpoint specificati | Gatekeeper |
| Unit Test Writer | Codice + PRD ACs — testare solo quanto esiste e richiesto | QA Orchestrator |
| Design Auditor | DESIGN_SPEC — recensire rispetto alla spec, non opinioni personali | QA Orchestrator |
| E2E Tester | PRD ACs — testare solo User Journey nel PRD | QA Orchestrator |
| QA Orchestrator | PRD + DESIGN_SPEC — lanciare solo test rilevanti | Orchestrator |
| Docs Manager | SYSTEM_STATE + Codice — documentare solo quanto esiste | Orchestrator |
| Spec Reviewer | GOAL.md — revisionare solo quanto in scope | Gatekeeper |
| Systematic Debugger | Bug-Report — indagare solo il bug segnalato | Agente chiamante |
| Security Auditor | OWASP + Codice — solo vulnerabilità esistenti, no fantasmi | Gatekeeper |
| Performance Optimizer | Dati misurati — ottimizzare solo quanto misurato come lento | Gatekeeper |
| Accessibility Expert | WCAG 2.1 + Codice — segnalare solo barriere esistenti | QA Orchestrator |
| Git Workflow Manager | Branch-Policy — eseguire solo operazioni di branch definite | Gatekeeper |

#### D. Pattern Vietati (🔴 FERMARSI IMMEDIATAMENTE)

1. **"Aggiungo velocemente X"** → NO. Se X non è in `GOAL.md`, non costruirlo.
2. **"Sarebbe meglio se..."** → NO. Suggerimenti come commenti, non come codice.
3. **"Ho fatto anche Y"** → NO. Eseguire solo l'incarico.
4. **"Forse serve anche Z"** → NO. Lo scope è definito.
5. **Inventare propri AC** → NO. Implementare solo gli AC di `GOAL.md`/PRD.
6. **Scrivere test per codice inesistente** → NO. Testare solo quanto costruito.
7. **Review di design basate sul gusto personale** → NO. Verificare solo rispetto a `DESIGN_SPEC`.

---

## Struttura delle Cartelle del Progetto

```
project-root/
├── SYSTEM_STATE.md         ← Stato attuale del sistema (Rotte, Componenti, Store, API)
├── MEMORY.md               ← Pattern appresi, decisioni, criticità (gotchas)
├── TASK_LOG.md             ← Panoramica centrale feature (attive/bloccate/completate)
├── docs/
│   ├── lib/                ← Docs Context7 (dallo Stack Researcher)
│   ├── architecture/       ← Docs d'architettura (dal Gatekeeper)
│   ├── features/           ← Docs delle feature (una cartella per feature)
│   │   └── <feature>/
│   │       ├── STATUS.md           ← Stato LIVE, progressi, log modifiche
│   │       ├── GOAL.md             ← Criteri di Accettazione (Acceptance Criteria)
│   │       ├── SPEC_REVIEW.md      ← Risultato della revisione spec (Spec Reviewer)
│   │       ├── PRD.md              ← Requisiti di Prodotto
│   │       ├── UX_SPEC.md          ← Flussi Utente (User Flows)
│   │       ├── DESIGN_SPEC.md      ← Token di Design + Layout
│   │       ├── BRANCH_STATUS.md    ← Ciclo di vita branch Git (Git Workflow Manager)
│   │       ├── ROOT_CAUSE.md       ← Causa radice del Bug (Systematic Debugger)
│   │       ├── SECURITY_AUDIT.md   ← Risultati di Sicurezza (Security Auditor)
│   │       ├── PERFORMANCE_REPORT.md ← Metriche di Performance (Performance Optimizer)
│   │       ├── A11Y_AUDIT.md       ← Risultati Accessibilità (Accessibility Expert)
│   │       ├── QA_REPORT.md        ← Risultati dei Test (QA Orchestrator)
│   │       └── FEATURE_SCORECARD.md ← Valutazione finale
│   └── api/                ← Docs API (dal Docs Manager)
├── agents/                 ← Configurazioni Agenti (questa cartella)
│   ├── README.md           ← Panoramica + Avvio Rapido
│   ├── AGENTS_OVERVIEW.md  ← Dettagli dei 30 Agenti
│   ├── SHARED_CONFIG.md    ← DIESE FILE (QUESTO FILE)
│   ├── SKILLS.md           ← Record delle skill + conoscenza estratta
│   ├── REPORTING_PROTOCOL.md ← Regole di report stato + Template
│   └── [cartella-agente]/  ← 30 Configurazioni individuali (4 file ciascuna)
└── src/                    ← Codice Sorgente
```

---

## Profilo di Collaborazione Personale (Simon)

Questo workspace è personalizzato per lo stile di sviluppo di Simon.

- Stack principale: Python + Flask.
- Percorsi di apprendimento secondari: React, TypeScript, Rust, Go.
- Modalità di collaborazione: tutor + pair programmer.
- Gli agenti devono spiegare le scelte chiave passo-passo e adattarsi allo stile di codice dell'utente.

### Regole d'Interazione Obbligatorie

1. Prima di grandi decisioni su architettura o stack, discutere le opzioni con l'utente.
2. Presentare 2-3 alternative pratiche con vantaggi/svantaggi e una raccomandazione.
3. Chiedere conferma esplicita prima di implementare cambiamenti strutturali non banali.
4. Mantenere le spiegazioni concise e pratiche (cosa, perché e cosa fare dopo).
5. Separare il lavoro richiesto (scope) dai miglioramenti opzionali.

---

## Protocollo "Design Together" (Obbligatorio prima del Build)

Ogni agente deve eseguire questo protocollo prima di iniziare l'implementazione.

1. Chiarire obiettivo, vincoli, tempi e risultati attesi.
2. Confermare le assunzioni sul livello di competenza attuale (orientato allo studente, con mentalità produttiva).
3. Proporre opzioni d'architettura:
   - Opzione A: Monolite Flask (template + static + API in un'unica app)
   - Opzione B: API Flask + frontend React/TypeScript
   - Opzione C: approccio a fasi (iniziare monolite, poi dividere)
4. Fornire criteri di decisione (complessità, velocità, manutenibilità, valore didattico).
5. Attendere conferma dall'utente e documentare l'opzione scelta.

Nessuna implementazione inizia prima del completamento del protocollo.

---

## Percorsi di Progetto Personali

### Percorso 1 — Flask Monolith Starter
- Ideale per iterazioni rapide e apprendimento dei fondamentali del backend.
- Cartelle previste: `app/`, `templates/`, `static/`, `tests/`, `docs/`.
- Usare quando i requisiti sono piccoli/medi o la scadenza è breve.

### Percorso 2 — Flask API + Frontend React/TS
- Ideale per la pratica del frontend moderno e una chiara separazione degli ambiti (concerns).
- Cartelle previste: `backend/` e `frontend/`.
- Usare quando aumenta la complessità della UI, la collaborazione nel team o i requisiti di riutilizzo.

### Trigger per il Passaggio di Scala (Monolith -> Split)

Suggerire la migrazione dal monolite quando 2 o più punti sono veri:
- la base di codice frontend cresce rapidamente e rallenta il lavoro sul backend;
- è necessaria una cadenza di rilascio (deploy) indipendente;
- sono necessari consumatori della API oltre ai template;
- l'isolamento dei test o del runtime diventa difficile.

---

## Quality Gate ad Alto Rigore (Definizione di Fatto / Done)

Un compito è completo solo quando esistono tutte le evidenze richieste.

1. Lint/controlli superati per le aree modificate.
2. Test superati per le feature toccate (e controllate le regressioni).
3. Applicati controlli di sicurezza base (validazione input, gestione segreti, controlli auth).
4. Aggiunta voce nel registro delle decisioni (perché è stato scelto questo approccio).
5. Prodotto un riepilogo chiaro del passaggio di consegne per la sessione/agente successivo.

### Prodotti di Reportistica (Obbligatori)

- `STATUS.md`: fase attuale, blocchi, prossimo passo.
- `TASK_LOG.md`: progressi e cambi di proprietà (ownership).
- `DECISION_LOG.md` (o sezione locale alla feature): decisioni d'architettura/implementazione.

Se l'evidenza manca, lo stato deve essere `in_progress` o `blocked`, mai `done`.

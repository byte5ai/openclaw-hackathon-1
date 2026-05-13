---
marp: true
theme: byte5
paginate: false
header: 'byte5 GmbH  |  OpenClaw Hackathon'
footer: '13. Mai 2026 · byte5 Office'
---

<!-- _class: title -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: '' -->

<span class="eyebrow">OpenClaw Hackathon · 13. Mai 2026 · byte5 Office</span>

# OpenClaw Hackathon

## AgentSkills bauen <span class="b5-colon">:</span> wir, heute Abend, gemeinsam

Marcel Wege · CTO @ byte5 · [mwege@byte5.de](mailto:mwege@byte5.de)

---

<!-- _header: 'Roter Faden für den Abend' -->

## Heute Abend <span class="b5-colon">:</span> vom fertigen Skill zum eigenen Skill

- **Demo** — Non-Annoying News live · ~20 min
- **Phase 0 <span class="b5-colon">:</span> Brain-Check** — Skill-Anatomy + Smoke-Tests · ~30 min
- **Phase 1 <span class="b5-colon">:</span> Level-Wahl** — Entry / Intermediate / Expert · ~10 min
- **Phase 2 <span class="b5-colon">:</span> Build** — Pomodoro-Rhythmus 55 + 10 + 55 · ~120 min
- **Phase 3 <span class="b5-colon">:</span> Show & Tell** — 3 min pro Team · ~30 min

> **Erfolgs-Versprechen** <span class="b5-colon">:</span> alle gehen mit etwas, das *läuft*. Egal welches Level.

---

<!-- _class: divider -->
<!-- _header: '' -->
<!-- _footer: '' -->

# Demo <span class="b5-colon">:</span> Non-Annoying News

---

<!-- _class: phase phase-1 -->
<!-- _header: 'Demo — Eine eigene Zeitung, geschrieben vom Agent' -->

<div class="phase-bar"></div>

## Non-Annoying News <span class="b5-colon">:</span> kein Clickbait, keine Filler-Boxen

Ein **public AgentSkill** von [@iret77](https://github.com/iret77) auf ClawHub — macht aus deinen Bookmarks, Reading-Lists und Feeds eine kompakte Zeitung im Magazin-Stil.

- **Quellen** <span class="b5-colon">:</span> X-Bookmarks · Browser Reading List · Read-Later · RSS · Newsletter · gepastete URLs
- **Anti-Pattern** <span class="b5-colon">:</span> kein Clickbait, keine Dashboard-Cards, keine vagen Link-Summaries
- **Versprechen** <span class="b5-colon">:</span> jeder Artikel ist verständlich, *ohne* die Quelle zu öffnen

> v0.2.1 · ClawHub · `non-annoying-news` → Installation auf der nächsten Folie

<small>*Quelle: [github.com/iret77/non-annoying-news](https://github.com/iret77/non-annoying-news) — README v0.2.1*</small>

---

<!-- _class: phase phase-1 -->
<!-- _header: 'Demo — Installation via OpenClaw-Agent' -->

<div class="phase-bar"></div>

## Installation 1/2 <span class="b5-colon">:</span> Agent-geführt

Paste in deinen OpenClaw-Agent — er installiert *und* führt durchs Onboarding:

```text
Install the public ClawHub skill `non-annoying-news` by @iret77,
then guide me through setup. Start with onboarding questions
(title, topics, sources, cadence, delivery, design) — do not
invent anything, create config only after I confirm.
```

> **Wichtig** <span class="b5-colon">:</span> Keine Tokens oder Cookies in den Chat. Die *Personalization Gate* verhindert Auto-Setup ohne Bestätigung.

<small>*Quelle: [github.com/iret77/non-annoying-news](https://github.com/iret77/non-annoying-news) — README v0.2.1*</small>

---

<!-- _class: phase phase-1 -->
<!-- _header: 'Demo — Installation via CLI' -->

<div class="phase-bar"></div>

## Installation 2/2 <span class="b5-colon">:</span> Manuell via CLI

`openclaw skills install` ist der native Befehl. `clawhub install` läuft alternativ — die Skills-README nutzt ihn.

```bash
openclaw skills install non-annoying-news    # native
clawhub install non-annoying-news            # alternative
```

Beide installieren in den aktiven Workspace. Details zur Location-Präzedenz kommen auf der nächsten Phase-0-Folie.

<small>*Quelle: [docs.openclaw.ai/tools/skills](https://docs.openclaw.ai/tools/skills)*</small>

---

<!-- _class: phase phase-1 -->
<!-- _header: 'Demo — Wie es funktioniert' -->

<div class="phase-bar"></div>

## Drei Stufen <span class="b5-colon">:</span> Signal → Standard → Issue

1. **Signals sammeln** — Bookmarks und Reading-Lists sind *Intent*, keine Fakten. Der Skill liest die Original-Quelle nach und markiert Zugriffs-Grenzen.
2. **Editorial Standard** — jeder Artikel beantwortet: *was* ist passiert · welcher *Mechanismus* · *warum* relevant · *Grenzen* der Evidenz.
3. **Render** — HTML zuerst, PDF danach. PNG-Previews jeder Seite vor Auslieferung.

> **Personalization Gate** <span class="b5-colon">:</span> kein Issue, kein Cron, keine Auslieferung — bis du Titel, Topics, Sources, Cadence und Design bestätigt hast.

<small>*Quelle: [github.com/iret77/non-annoying-news](https://github.com/iret77/non-annoying-news) — README v0.2.1, SKILL.md*</small>

---

<!-- _class: divider -->
<!-- _header: '' -->
<!-- _footer: '' -->

# Phase 0 <span class="b5-colon">:</span> OpenClaw-Brain

---

<!-- _class: phase phase-1 -->
<!-- _header: 'Phase 0 — Anatomy of a Skill' -->

<div class="phase-bar"></div>

## Anatomy <span class="b5-colon">:</span> ein Folder, ein Manifest, optional mehr

```
my-skill/
├── SKILL.md          # Required: metadata + instructions
├── scripts/          # Optional: executable code
├── references/       # Optional: documentation
└── assets/           # Optional: templates, resources
```

> **Mental Model** <span class="b5-colon">:</span> Skill = Manifest + Lazy-Loaded Knowledge + optionale Scripts. Der Agent lädt nur, was er für die Aufgabe braucht.

<small>*Quellen: [agentskills.io](https://agentskills.io) · [docs.openclaw.ai/tools/skills](https://docs.openclaw.ai/tools/skills)*</small>

---

<!-- _class: phase phase-1 -->
<!-- _header: 'Phase 0 — Drei Smoke-Tests' -->

<div class="phase-bar"></div>

## Bevor wir bauen <span class="b5-colon">:</span> zwei schnelle Checks

1. **Agent-Hello** — ein bekannter Prompt, du erkennst die Antwort.
2. **Demo-Skill installierbar** — `openclaw skills install non-annoying-news` läuft sauber durch und landet im aktiven Workspace.

```bash
# Sync-Punkt für alle: kurzer Trockenlauf
openclaw skills install non-annoying-news
```

Skills landen je nach Scope in `<workspace>/skills`, `~/.agents/skills` oder `~/.openclaw/skills` — bei Konflikten gewinnt die höhere Präzedenz.

> **Wenn was klemmt** <span class="b5-colon">:</span> *jetzt* melden — wir lösen das hier zusammen, nicht später unter Zeitdruck.

<small>*Quelle: [docs.openclaw.ai/tools/skills](https://docs.openclaw.ai/tools/skills) — Location-Präzedenz + CLI-Kommandos*</small>

---

<!-- _class: divider -->
<!-- _header: '' -->
<!-- _footer: '' -->

# Phase 1 <span class="b5-colon">:</span> Level wählen

---

<!-- _class: phase phase-2 -->
<!-- _header: 'Phase 1 — Drei Levels, eine Wahl' -->

<div class="phase-bar"></div>

## Pick dein Level <span class="b5-colon">:</span> Entry · Intermediate · Expert

| Level | Was du baust | Zeit-Realismus in 2 h |
|---|---|---|
| **Entry** | Du remixt einen bestehenden Skill — Config, Design, eigene Quelle | sicheres Ergebnis |
| **Intermediate** | Eigener kleiner Skill — *1 Input → 1 Artefakt* | ambitioniert |
| **Expert** | Meta-Skill, Composer oder Round-Trip auf ClawHub | sportlich, dafür spannend |

> **Team-Bildung** <span class="b5-colon">:</span> 1–3 Personen pro Team · gleiches Level. Solo bauen ist auch okay.

---

<!-- _class: divider -->
<!-- _header: '' -->
<!-- _footer: '' -->

# Phase 2 <span class="b5-colon">:</span> Build

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Entry-Level' -->

<div class="phase-bar"></div>

## Entry <span class="b5-colon">:</span> Remix einen bestehenden Skill

**Empfohlen** — `non-annoying-news` personalisieren:

- Eigene Quellen (Bookmarks · RSS · Reading-List) durchs Onboarding fahren
- Ein **Design-Preset** ändern — Theme-Farben, Density-Token
- **Eine neue Signal-Quelle** ergänzen — z. B. dein Lieblings-Newsletter als RSS

**Open Slot** — du hast einen anderen public Skill im Auge, den du remixen willst? Genauso valide.

> **Erfolg** <span class="b5-colon">:</span> ein gerendertes, personalisiertes Issue, das deine Sprache spricht.

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Entry: Demo-Vorlage im Repo' -->

<div class="phase-bar"></div>

## `demos/entry/byte5-news-remix/`

```
byte5-news-remix/
├── README.md           # Anwendungs-Anleitung
├── config.json         # Topics, Quellen, Cadence — onboarding.complete=true
└── design-tokens.css   # byte5-Magenta, Cyan, Days One, Density
```

> Config-Overlay für `non-annoying-news`. **Klonen · `config.json` auf deine Topics umbiegen · Tokens auf deine Farben.**

<small>*[demos/entry/byte5-news-remix](https://github.com/byte5ai/openclaw-hackathon-1/tree/main/demos/entry/byte5-news-remix)*</small>

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Entry: Umsetzung' -->

<div class="phase-bar"></div>

## Von Zero zum personalisierten Issue

**Via OpenClaw-Chat — Personalization Gate:**

> „Starte das non-annoying-news-Onboarding. Topics: AI-Agents, OpenClaw, Web-Standards. Quelle: hnrss.org/frontpage. Cadence: wöchentlich. Design: byte5-Magenta, Days One."

Der Skill führt durch sein Onboarding, persistiert die Antworten lokal, rendert das erste Issue.

**Via Code-Eingaben:**

`references/onboarding.md` + `config-schema.md` von non-annoying-news lesen → `config.json` am vom Skill genannten Pfad hand-bauen → `onboarding.complete=true` → `/new`.

→ Referenz im Repo: [`demos/entry/byte5-news-remix`](https://github.com/byte5ai/openclaw-hackathon-1/tree/main/demos/entry/byte5-news-remix)

<small>*Quelle: [non-annoying-news SKILL.md](https://github.com/iret77/non-annoying-news/blob/main/SKILL.md) — Personalization Gate + references*</small>

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Intermediate' -->

<div class="phase-bar"></div>

## Intermediate <span class="b5-colon">:</span> 1 Input → 1 Artefakt

**Empfohlen** — ein kleiner Skill, der genau eine Quelle in genau ein Artefakt verwandelt:

- `RSS-Feed → 5-Bullet-Wochenbrief`
- `Meeting-Transcript → Action-Items-Liste`
- `GitHub-Notifications → Wochenrückblick`

Mindest-Pattern <span class="b5-colon">:</span> `SKILL.md` + 1 Reference-Doc + 1 Script + 1 Asset-Template.

**Open Slot** — eigene Input-Output-Kombo? Pick dir was, woran du genuin interessiert bist.

> **Erfolg** <span class="b5-colon">:</span> lokal installierbar, mit *einem* gezeigten Live-Beispiel.

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Intermediate: Demo-Vorlage im Repo' -->

<div class="phase-bar"></div>

## `demos/intermediate/rss-zu-wochenbrief/`

```
rss-zu-wochenbrief/
├── SKILL.md                            # Manifest + Workflow
├── README.md
├── references/editorial-style.md       # Stil-Regeln pro Bullet
├── scripts/fetch_rss.py                # RSS/Atom-Parser (stdlib-only)
└── assets/template.md                  # Markdown-Output-Template
```

> RSS-URL → 5-Bullet-Markdown. **Kopier-Vorlage für deine eigene 1-Input/1-Artefakt-Idee** — Script + Template tauschen, Pattern bleibt.

<small>*[demos/intermediate/rss-zu-wochenbrief](https://github.com/byte5ai/openclaw-hackathon-1/tree/main/demos/intermediate/rss-zu-wochenbrief)*</small>

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Intermediate: Umsetzung' -->

<div class="phase-bar"></div>

## Von Zero zum eigenen Skill

**Via OpenClaw-Chat:**

> „Bau einen Skill `rss-zu-wochenbrief` in `~/.openclaw/workspace/skills/`. Pattern: `SKILL.md` mit Frontmatter + Workflow, 1 Reference (Editorial-Stil), 1 Python-Script (stdlib, parsed RSS/Atom), 1 Markdown-Template."

Agent schreibt die vier Dateien direkt. `/new`, dann mit RSS-URL triggern.

**Via Code-Eingaben:**

`mkdir -p ~/.openclaw/workspace/skills/rss-zu-wochenbrief/{references,scripts,assets}` → vier Dateien nach AgentSkills-Spec hand-schreiben → `/new`.

→ Referenz im Repo: [`demos/intermediate/rss-zu-wochenbrief`](https://github.com/byte5ai/openclaw-hackathon-1/tree/main/demos/intermediate/rss-zu-wochenbrief)

<small>*Quellen: [docs.openclaw.ai/tools/creating-skills](https://docs.openclaw.ai/tools/creating-skills) · [agentskills.io](https://agentskills.io)*</small>

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Expert' -->

<div class="phase-bar"></div>

## Expert <span class="b5-colon">:</span> Skill ist nur der Anfang

**Empfohlen — wähle einen Pfad:**

- **Meta-Skill** — analysiert andere Skills auf OpenClaw-Konventionen (`SKILL.md`-Schema, Personalization-Gate, Editorial-Standard)
- **Composer-Skill** — orchestriert 2+ Skills mit eigenem QA-Gate dazwischen
- **Round-Trip** — Skill bauen, validieren, auf ClawHub publishen

**Open Slot** — eigenes Expert-Vorhaben? Geh es an, wir reviewen mit.

> **Erfolg** <span class="b5-colon">:</span> ein Pattern, das jemand anderes übernehmen kann.

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Expert: Demo-Vorlage im Repo' -->

<div class="phase-bar"></div>

## `demos/expert/daily-briefing/`

```
daily-briefing/
├── SKILL.md                                # Composer-Workflow (3 Steps)
├── README.md
├── references/qa-gate.md                   # QA-Regeln + Output-Schema
├── scripts/qa_check.py                     # Validator (pass→weiter, fail→Stopp)
└── assets/composition-diagram.md           # Mermaid: Pipeline
```

> `rss-zu-wochenbrief` + QA-Gate + `non-annoying-news`. **Pipeline-Pattern — andere Skills, anderes Gate, anderes Ergebnis.**

<small>*[demos/expert/daily-briefing](https://github.com/byte5ai/openclaw-hackathon-1/tree/main/demos/expert/daily-briefing)*</small>

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Expert: Umsetzung' -->

<div class="phase-bar"></div>

## Von Zero zum Composer

**Voraussetzung:** `rss-zu-wochenbrief` schon im Workspace.

**Via OpenClaw-Chat:**

> „Bau einen Composer `daily-briefing`. Pipeline: RSS-URL → rss-zu-wochenbrief → QA-Gate (Python) → non-annoying-news. Validator prüft 5 Bullets, Quellen vorhanden, 8–25 Wörter, keine Hype-Wörter."

**Via Code-Eingaben:**

Folder mit den 4 AgentSkill-Schichten anlegen → `SKILL.md` mit 3-Step-Workflow → `scripts/qa_check.py` mit Bullet-/Quellen-/Hype-Checks → `/new`.

→ Referenz im Repo: [`demos/expert/daily-briefing`](https://github.com/byte5ai/openclaw-hackathon-1/tree/main/demos/expert/daily-briefing)

<small>*Quellen: [docs.openclaw.ai/tools/creating-skills](https://docs.openclaw.ai/tools/creating-skills) · [docs.openclaw.ai/tools/skills](https://docs.openclaw.ai/tools/skills)*</small>

---

<!-- _class: phase phase-3 -->
<!-- _header: 'Phase 2 — Spielregeln' -->

<div class="phase-bar"></div>

## Pomodoro <span class="b5-colon">:</span> 55 + 10 + 55

1. **Block 1** — 55 min bauen, ausprobieren, scheitern dürfen
2. **Cross-Check** — 10 min gemeinsame Sync-Runde, was funktioniert nicht
3. **Block 2** — 55 min stabilisieren, demoreif machen

**Deine Hilfe-Quellen:**

- **Dein eigener Agent** — pair-programmt mit dir
- **ClawHub** — andere public Skills als Vorlage / Pattern-Quelle
- **Wir als Mentoren** — Marcel (+ ggf. weitere) bei echten Blöckern

> **Leitsatz** <span class="b5-colon">:</span> funktioniert > schön · *kein Production-Skill in 2 h*.

---

<!-- _class: divider -->
<!-- _header: '' -->
<!-- _footer: '' -->

# Phase 3 <span class="b5-colon">:</span> Show & Tell

---

<!-- _class: phase phase-4 -->
<!-- _header: 'Phase 3 — Show & Tell' -->

<div class="phase-bar"></div>

## Format <span class="b5-colon">:</span> 3 min · Demo > Slides · kein Kritik-Format

**Was zeigen:**

- Was hast du gebaut? In *einem* Satz.
- Live-Demo — der Skill in Aktion. Wenn er kaputt geht: auch okay, ist Hackathon.
- Was war der Aha-Moment?

**Was *nicht* zeigen:**

- Code-Walkthrough Zeile für Zeile
- Folien-Deck — du hast gerade einen *Skill* gebaut, kein Tech-Talk

> **Feedback-Regel** <span class="b5-colon">:</span> nur „cool, weil…" — Kritik bekommst du danach, einzeln, wenn du sie willst.

---

<!-- _class: divider -->
<!-- _header: '' -->
<!-- _footer: '' -->

# Vielen Dank.

---

<!-- _class: closing -->
<!-- _header: '' -->

# Vielen Dank.

<span class="eyebrow">Material zum Mitnehmen</span>

- **Slides** <span class="b5-colon">:</span> [byte5ai.github.io/openclaw-hackathon-1](https://byte5ai.github.io/openclaw-hackathon-1/) · [PDF](https://byte5ai.github.io/openclaw-hackathon-1/deck.pdf)
- **Repo** <span class="b5-colon">:</span> [github.com/byte5ai/openclaw-hackathon-1](https://github.com/byte5ai/openclaw-hackathon-1)
- **Demo-Skills** <span class="b5-colon">:</span> [drei Levels im Repo](https://github.com/byte5ai/openclaw-hackathon-1/tree/main/demos) · Entry · Intermediate · Expert
- **Original-Demo** <span class="b5-colon">:</span> [github.com/iret77/non-annoying-news](https://github.com/iret77/non-annoying-news)
- **byte5** <span class="b5-colon">:</span> [byte5.de](https://www.byte5.de)

<span class="eyebrow">Du suchst Unterstützung bei deinem digitalen Projekt?</span>

**Dein digitales Projekt** <span class="b5-colon">:</span> unsere Expert:innen beraten dich transparent.

---
name: brain-wiki
description: Kuratiertes Wissens-Wiki (OKF-Bundle) führen und abfragen — Seiten anlegen/aktualisieren, Ingest, Query mit Zitaten, Lint. Nutzen, wenn Wissen dauerhaft versioniert werden soll oder die Frage das Wiki als Quelle verdient.
disable-model-invocation: true
---

# Brain-Wiki

Kuratiertes, Git-versioniertes Wissens-Gehirn: **Open Knowledge Format (OKF) Bundle**
× **LLM-Wiki-Workflow** (Karpathy). Der Agent pflegt es selbstständig — Seiten
schreiben, index.md führen, log.md anhängen.

## Wiki-Ort finden

1. Umgebungsvariable `PI_BRAIN_WIKI_DIR`, falls gesetzt
2. Sonst `~/wiki`
3. Sonst: User fragen (oder mit `wiki-vorlage/` aus diesem Paket ein neues Wiki anlegen:
   Vorlage nach `~/wiki` kopieren, `git init`, erste Einträge)

## Die drei Schichten

1. **Raw Sources** (`sources/`) — unveränderlich, **nie editieren**
2. **Wiki-Seiten** (`entities/`, `concepts/`, `projects/`, `insights/`) — nur hier schreiben
3. **SCHEMA.md** im Wiki-Root — die Konventionen; bei Zweifeln nachlesen

## Ordner

| Ordner | Inhalt |
|---|---|
| `sources/` | Rohquellen (Notizen, Exporte, Artikel-URLs) |
| `entities/` | Eine Seite pro „Ding": Tool, Extension, Komponente |
| `concepts/` | Abstrakte Ideen, Muster, Techniken |
| `projects/` | Aktive Projekte mit Entscheidungen + Status |
| `insights/` | Synthesen, Vergleiche, erforschte Antworten |

## Frontmatter (jede Seite)

```yaml
---
type: Entity | Concept | Project | Insight | Reference
title: Lesbarer Titel
tags: [pi, ...]
sources:
  - url: https://...
    note: kurze Einordnung (optional)
generated: "YYYY-MM-DD"
status: current | stable | deprecated
---
```

Cross-Links als relative Markdown-Links, jede Seite mindestens ein Link (keine Orphans).

## Workflows

- **Ingest**: Quelle nach `sources/` (danach nie anfassen) → Kerninhalt extrahieren,
  mit User abstimmen → betroffene Entity-/Concept-Seiten anlegen/aktualisieren →
  ggf. Insight → `index.md` aktualisieren → `log.md`-Eintrag anhängen.
- **Query**: `index.md` lesen → relevante Seiten lesen, Links folgen → Antwort
  **mit Seitenzitaten** synthetisieren → gute Antworten ggf. als Insight zurück ins
  Wiki (mit User absprechen).
- **Lint** (gelegentlich, `/wiki-update`): Orphans finden, Widersprüche auflösen,
  `status: deprecated` setzen, `index.md` mit realen Seiten abgleichen, `log.md` führen.

## Abgrenzung zu mnemon

- **mnemon**: episodisch, automatisch, altert — Entscheidungen, Präferenzen, Session-Kontinuität
- **Wiki**: kuratiert, dauerhaft, versionierbar — destilliertes Wissen
- Regel: Fakt taucht in mehreren Sessions auf → Wiki-Seite. Einmal-Erkenntnis → nur `log.md`.

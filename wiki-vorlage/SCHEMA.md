---
type: Schema
title: Brain-Wiki Konventionen
description: Regeln für Ingest, Query und Lint dieses OKF-Bundles
generated: "2026-09-15"
status: current
---

# Brain-Wiki — Konventionen

Dieses Wiki ist ein **Open Knowledge Format (OKF) Bundle** (Spec: v0.2, GoogleCloudPlatform/knowledge-catalog) kombiniert mit dem **LLM-Wiki-Workflow** (Karpathy).

## Die drei Schichten

1. **Raw Sources** (`sources/`) — unveränderlich, niemals editieren. Original-Notizen, Exporte, CLIs, Artikel.
2. **Wiki-Seiten** (`entities/`, `concepts/`, `projects/`, `insights/`) — LLM-gepflegt, nur hier schreiben.
3. **Dieses Schema** — Konventionen, die der Agent befolgt.

## Ordnerstruktur

| Ordner      | Inhalt                                                      |
|-------------|-------------------------------------------------------------|
| `sources/`  | Unveränderliche Rohquellen                                   |
| `entities/` | Eine Seite pro „Ding": Tool, Person, Projekt-Komponente      |
| `concepts/` | Abstrakte Ideen, Muster, Techniken                           |
| `projects/` | Aktive Projekte mit Entscheidungen und Status                |
| `insights/` | Synthesen, Vergleiche, erforschte Antworten („gefilete")     |

## Frontmatter (OKF-Kern)

```yaml
---
type: Entity | Concept | Project | Insight | Reference
title: Lesbarer Titel
tags: [pi, memory]
sources:
  - url: https://...
    note: kurze Einordnung (optional)
generated: "YYYY-MM-DD"   # wann die Seite erstellt/aktualisiert wurde
status: current | stable | deprecated
---
```

**Bewusst nicht genutzt** (optional laut Spec, für Firmen): `verified`, Trust-Tiers, `stale_after`, Attested Computations. Kann später nachgerüstet werden, ohne Kompatibilität zu brechen.

## Cross-Links

Normale Markdown-Links mit relativen Pfaden: `[mnemon](entities/mnemon.md)`.
Jede Seite sollte mindestens einen Link haben, kein Orphan-Seiten-Dickicht.

## Workflows

### Ingest (neue Quelle)
1. Quelle nach `sources/` legen (oder URL notieren) — danach nie wieder anfassen.
2. Kerninhalt extrahieren, mit mir (User) kurz abstimmen.
3. Betroffene Entity-/Concept-Seiten erstellen **oder** aktualisieren (eine Quelle kann mehrere Seiten berühren).
4. `insights/`-Seite anlegen, falls die Quelle eigene Erkenntnis verdient.
5. `index.md` aktualisieren (eine Zeile pro Seite, mit Tags).
6. Eintrag in `log.md` anhängen.

### Query (Frage stellen)
1. `index.md` lesen → relevante Seiten identifizieren.
2. Seiten lesen, links folgen falls nötig.
3. Antwort synthetisieren **mit Quellen-/Seitenzitaten**.
4. Gute Antworten als Insight zurück ins Wiki filelen (mit User absprechen).

### Lint (Pflege, gelegentlich)
- Orphan-Seiten finden und verlinken oder löschen.
- Widersprüche zwischen Seiten auflösen.
- `status: deprecated` bei Veraltetem; `log.md` Eintrag dazu.
- `index.md` mit tatsächlichen Seiten abgleichen.

## Arbeitsteilung mit mnemon

- **mnemon** (`~/.mnemon`): episodisch, automatisch, altert — Entscheidungen, „das ging schief, weil…", Präferenzen, Session-Kontinuität.
- **Wiki**: kuratiert, dauerhaft, versionierbar (Git) — destilliertes Wissen.
- Regel: Taucht ein mnemon-Fakt in mehreren Sessions wieder auf → verdient eine Wiki-Seite.

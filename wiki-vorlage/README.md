# Brain-Wiki Vorlage (OKF + Karpathy)

Der **Bauplan** für das persönliche Brain-Wiki — die Wissensbasis, in der pi
destilliertes Wissen ablegt: Tools, Projekte, Muster, gefilete Antworten.
Besteht aus dem **Open Knowledge Format** (Google, Markdown + YAML-Frontmatter)
und dem **LLM-Wiki-Workflow** (Karpathy) — die beiden Concept-Seiten erklären
beides, `SCHEMA.md` sind die Konventionen, die pi befolgt.

**Bewusst nur der Bauplan, keine Inhalte:** Deine Entities, Projekte und
Erinnerungen gehören dir allein — das Gerüst ist austauschbar.

## Inhalt

```
wiki-vorlage/
├── README.md        ← diese Datei (Aufbau-Anleitung)
├── SCHEMA.md        ← die Konventionen (Ordner, Frontmatter, Workflows)
├── index.md         ← Start-Index (pi liest ihn bei jeder Query zuerst)
├── concepts/
│   ├── okf.md       ← was ist das Open Knowledge Format?
│   └── llm-wiki.md  ← was ist der Karpathy-Workflow?
├── entities/        ← eine Seite pro „Ding" (Tool, Komponente …)
├── insights/        ← gefilete Antworten & Synthesen
├── projects/        ← aktive Projekte mit Entscheidungen
└── sources/         ← unveränderliche Rohquellen (niemals editieren!)
```

## Aufbau (5 Minuten)

```bash
# 1. Gerüst nach ~/wiki legen (oder beliebiges Verzeichnis)
cp -R wiki-vorlage ~/wiki
cd ~/wiki

# 2. Git initialisieren
git init && git add -A && git commit -m "Brain-Wiki Gerüst (OKF + Karpathy)"

# 3. Privates GitHub-Repo anlegen und pushen (die Inhalte sind privat!)
gh repo create brain-wiki --private --source=. --push

# 4. pi bescheid sagen
```

## pi einrichten

Der Wiki-Pfad muss pi bekannt sein — z. B. in der ersten Sitzung nach der
Installation sagen:

> „Mein Brain-Wiki liegt in `~/wiki` (OKF-Bundle nach SCHEMA.md). Wenn du
> Wichtiges aus unseren Sessions destillierst, lege/update Wiki-Seiten nach
> den Workflows in SCHEMA.md (Ingest, Query, Lint) und halte `index.md`
> und `log.md` aktuell."

Tipp: Der Satz gehört auch in die eigene `/erste-einrichtung`-Vorlage oder
ein `AGENTS.md`/`SYSTEM.md`, damit er jede Session automatisch da ist.

## Zusammenleben mit mnemon

- **mnemon** = episodisches Gedächtnis (automatisch, altert, Entsprechung:
  „was war gestern?")
- **Wiki** = kuratiertes Wissensbuch (dauerhaft, in Git, Entsprechung:
  „was weiß ich sicher über Tool X?")
- Faustregel aus SCHEMA.md: Taucht ein mnemon-Fakt in mehreren Sessions auf,
  verdient er eine Wiki-Seite.

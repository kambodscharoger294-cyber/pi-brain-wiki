---
type: Concept
title: Open Knowledge Format (OKF)
tags: [format, standard, markdown]
sources:
  - url: https://github.com/GoogleCloudPlatform/knowledge-catalog/blob/main/okf/SPEC.md
    note: Spec v0.2
  - url: https://github.com/GoogleCloudPlatform/open-knowledge-format
    note: Referenz-Repo mit visualize-Tool
generated: "2026-09-15"
status: current
---

# Open Knowledge Format (OKF)

Vendor-neutrales Format von Google (v0.2): Wissen als **Verzeichnis aus Markdown-Dateien mit YAML-Frontmatter**. Human- und agent-lesbar mit simplen File-Operationen — „wenn man eine Datei catten oder ein Repo klonen kann, kann man OKF lesen und versenden".

## Kernkonzepte

- **Knowledge Bundle**: in sich geschlossenes Verzeichnis, portabel (tarball/Repo)
- **Concept**: eine UTF-8-Markdown-Datei = Frontmatter + Body
- **type** (Pflicht): beschreibender Concept-Typ (z. B. `Entity`, `Concept`, `BigQuery Table`, `API Endpoint`); Consumer müssen unbekannte Typen tolerieren
- **Cross-Links + Paths**: normales Verlinken → navigierbarer Knowledge-Graph
- **Progressive Disclosure**: `index.md` als Einstieg, dann links folgen

## Provenance & Trust (der „Firmen-Teil")

Alles **optional** laut Spec:

- `sources` — Glaubwürdigkeits-Signale pro Quelle (keine numerischen Scores)
- `generated` / `verified` — Trust-Lifecycle des Concepts
- `status` — Lifecycle-State (current / deprecated …)
- `stale_after` — Frische-Signal
- Trust-Tiers, **Attested Computations** (Executor, Attester, Receipt, Evidence — verifizierbare Rechenergebnisse)

**Für private Brain-Nutzung:** Kern-Subset nutzen (`type`, `title`, `tags`, `sources`, `generated`, `status`), Enterprise-Felder weglassen. Bleibt 100 % spec-konform und später ohne Bruch nachrüstbar.

## Tooling-Kompatibilität

Obsidian, MkDocs, Hugo, Jekyll, Notion fressen das Format direkt. Das Referenz-Repo hat ein `visualize`-Subcommand: Bundle → **self-contained HTML-Viewer** (kein Backend) → klickbares Wiki zum Teilen.

## Verbindungen

- Format dieses [Brain-Wikis](../SCHEMA.md)
- [LLM Wiki](llm-wiki.md) liefert den Workflow dazu

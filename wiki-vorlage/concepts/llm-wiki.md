---
type: Concept
title: LLM Wiki
tags: [wissen, muster, karpathy]
sources:
  - url: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
    note: Original-Gist von Andrej Karpathy
generated: "2026-09-15"
status: current
---

# LLM Wiki

Muster für eine persistente, LLM-gepflegte Wissensbasis — „ein interlinktes Wiki, das zwischen dich und deine Rohquellen gestellt wird".

## Kernidee

Kein RAG über chaotische Notizen, sondern ein **kompiliertes Artefakt**: Beim Ingest liest der LLM die Quelle, extrahiert Kerninfos und *integriert* sie in bestehende Wiki-Seiten (Entity-Seiten, Concept-Seiten, Cross-References) — statt sie nur zu indexieren. Metapher: „Obsidian ist die IDE, der LLM der Programmierer, das Wiki die Codebase."

## Drei Schichten

1. **Raw Sources** — unveränderlich, nur referenzieren
2. **Wiki** — LLM-gepflegte Markdown-Seiten mit Cross-Links
3. **Schema** — Konfiguration/Konventionen, die dem Agent Struktur und Workflows vorgeben

## Reservierte Dateien

- `index.md` — Katalog: alle Seiten mit Einzeiler-Zusammenfassung + Metadaten; der Agent liest ihn zuerst bei jeder Query
- `log.md` — chronologisches Änderungsprotokoll

## Workflows

- **Ingest**: Quelle lesen → Takeaways klären → Summary + betroffene Seiten schreiben → Index + Log updaten. Eine Quelle kann mehrere Seiten berühren.
- **Query**: Index → relevante Seiten → synthetisierte Antwort mit Zitaten. Gute Antworten werden als neue Seiten zurück ins Wiki gefiled (kumulatives Wachstum).
- **Lint**: Konsistenz, Orphans, Veraltetes.

## Skalierung

Gedacht für ~100 Quellen / hunderte Seiten **ohne** Embedding-Retrieval — Struktur und Index tragen die Auffindbarkeit.

## Verbindungen

- Umgesetzt in diesem [Brain-Wiki](../SCHEMA.md)
- Seitenformat: [OKF](okf.md)

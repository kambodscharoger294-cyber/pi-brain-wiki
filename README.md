# pi-brain-wiki

**Brain-Wiki für [pi](https://pi.dev)** — Skill + Prompt + Vorlage, damit der Agent
ein kuratiertes Wissens-Wiki (OKF-Bundle × LLM-Workflow) selbst pflegt.

## Was drin ist

```
pi-brain-wiki/
├── skills/brain-wiki/SKILL.md   ← Agent kennt Struktur, Frontmatter, Ingest/Query/Lint
├── prompts/wiki-update.md       ← /wiki-update: Lint-Runde (Index-Abgleich, Orphans, log.md)
└── wiki-vorlage/                ← fertige Starter-Struktur für ein neues Wiki
```

## Installieren

```bash
pi install git:github.com/USER/pi-brain-wiki
# oder lokal:
pi install /pfad/zu/pi-brain-wiki
```

Danach kennt pi die Konventionen (Skill „brain-wiki"). Das Wiki selbst bleibt ein
eigenes Git-Repo pro Nutzer — gepackt werden nur die Regeln.

## Wiki anlegen (erstmals)

```bash
mkdir -p ~/wiki && cp -R wiki-vorlage/* ~/wiki/ && cd ~/wiki && git init
```

Oder pi fragen: „Leg mir mit der brain-wiki-Vorlage ein Wiki an."

Wiki-Ort anpassen: Umgebungsvariable `PI_BRAIN_WIKI_DIR` setzen (Default: `~/wiki`).

## Zusammen mit mnemon

mnemon = episodisch („was ist passiert"), Wiki = kuratiert + versioniert („was weiß ich").
Fakt taucht in mehreren Sessions auf → Wiki-Seite.

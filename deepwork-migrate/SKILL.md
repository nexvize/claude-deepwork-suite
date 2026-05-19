---
name: deepwork-migrate
description: "**VERALTET — Diese Funktion ist jetzt in deepwork-entry-analyze integriert.** Redirect: nutze /deepwork-entry-analyze stattdessen — erkennt automatisch ob keine oder eine veraltete deepwork-Struktur vorliegt und handelt entsprechend. Dieser Skill ist ein Redirect zu /deepwork-entry-analyze, welcher alle Migrationsfälle behandelt — inklusive automatischer Erkennung des Projekttyps (coding, research, content, design, media, marketing, analysis, concept, education, automation, legal, finance) und Anlage der typ-spezifischen Ordnerstruktur."
allowed-tools:
  - Read
---

# deepwork-migrate — Jetzt Teil von deepwork-entry-analyze

Diese Skill ist in `deepwork-entry-analyze` aufgegangen.

`deepwork-entry-analyze` erkennt automatisch:
- **Kein deepwork** → vollständige Analyse + Struktur aufbauen
- **Alte/unvollständige deepwork-Struktur** → Struktur additiv ergänzen (Migrate-Modus) + leichte Gap-Analyse

```
Statt /deepwork-migrate → nutze /deepwork-entry-analyze
```

Der Skill startet automatisch im richtigen Modus basierend auf dem was er vorfindet — inklusive automatischer Erkennung des Projekttyps (coding, research, content, design, media, marketing, analysis, concept, education, automation, legal, finance) und Anlage der typ-spezifischen Ordnerstruktur.

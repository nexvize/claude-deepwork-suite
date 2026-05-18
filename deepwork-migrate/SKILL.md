---
name: deepwork-migrate
description: "**VERALTET — Diese Funktion ist jetzt in deepwork-entry-analyze integriert.** Redirect: nutze /deepwork-entry-analyze stattdessen — erkennt automatisch ob keine oder eine veraltete deepwork-Struktur vorliegt und handelt entsprechend."
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

Der Skill startet automatisch im richtigen Modus basierend auf dem was er vorfindet.

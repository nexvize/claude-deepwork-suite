# Deepwork-Suite — Zentrale Konfiguration

Diese Datei ist die einzige Stelle, die angepasst werden muss wenn sich Pfade oder Grundeinstellungen ändern.
Alle deepwork-Skills lesen ihre Konfiguration von hier — niemals hardcoded in den Skills selbst.

---

## Pflicht: Beim Start jeder Skill lesen

Jede deepwork-Skill liest am Anfang diese Datei und nutzt die Werte unten.
Format: `DEEPWORK_<KEY> = <value>`

---

## Konfiguration

```
DEEPWORK_VAULT_PATH = D:\Claude\ObsidianVault
DEEPWORK_PROJECTS_PATH = D:\Claude\Projekte
DEEPWORK_SKILLS_PATH = C:\Users\Paul\.claude\skills
DEEPWORK_SWARM_MAX_WORKERS = 100
DEEPWORK_DEFAULT_COST_CAP_USD = 5.00
DEEPWORK_ENVIRONMENT_FILE = C:\Users\Paul\.claude\ENVIRONMENT.md
```

---

## Wie du Werte änderst

1. Diese Datei öffnen (`DEEPWORK-CONFIG.md`)
2. Den entsprechenden Wert rechts vom `=` ändern
3. Speichern — alle Skills verwenden ab sofort den neuen Wert

Beispiel: Du hast den Vault auf `E:\Notizen\Obsidian` verschoben:
```
DEEPWORK_VAULT_PATH = E:\Notizen\Obsidian
```
Fertig. Keine anderen Dateien müssen geändert werden.

---

## Für Claude: Wie die Werte gelesen werden

```
Lese DEEPWORK-CONFIG.md am Anfang der Skill.
Verwende DEEPWORK_VAULT_PATH für alle Vault-Pfade.
Verwende DEEPWORK_SWARM_MAX_WORKERS als hartes Maximum für Swarm-Sizing.
Verwende DEEPWORK_DEFAULT_COST_CAP_USD wenn kein Cost-Cap im Projekt-Contract.
```

---

## Versions-Info

Erstellt: 2026-05-17
Letzte Änderung: 2026-05-17
Suite-Version: 2.0 (9 Skills)

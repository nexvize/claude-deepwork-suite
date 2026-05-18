# Vault-Bootstrap — Obsidian-Ordner aufbauen

Obsidian ist ein kostenloses Notizprogramm das Dateien lokal auf deinem Computer speichert — als normale Textdateien (Markdown). Das macht es ideal als dauerhaften Wissensspeicher für deepwork-Projekte.

Ein "Vault" ist einfach ein Ordner auf deinem Computer, den Obsidian als seine Heimat betrachtet.

---

## Konfigurierter Vault-Pfad

**Primärer Vault:** Lese `DEEPWORK-CONFIG.md` → `DEEPWORK_VAULT_PATH` (Standard: `D:\Claude\ObsidianVault\`)

Dieser Pfad liegt neben `DEEPWORK_PROJECTS_PATH` (`D:\Claude\Projekte\`) — so sind Vault und Projekte auf derselben Festplatte, was Backup und Zugriff vereinfacht.

**Pfad ändern:** Nur `DEEPWORK-CONFIG.md` bearbeiten — alle Skills lesen automatisch den neuen Wert.

---

## Ordnerstruktur die Claude anlegt

```
D:\Claude\ObsidianVault\
├── Projects\                    ← Ein Unterordner pro Projekt
│   └── <projekt-name>\          ← Wird beim ersten Projekt angelegt
│       └── Deepwork\            ← deepwork-Dateien gespiegelt
│           ├── Plan.md
│           ├── Verdict.md
│           ├── Handoff.md
│           ├── Decisions.md
│           ├── Research-Summary.md
│           └── (weitere deepwork-Dokumente)
├── Inbox\                       ← Schnelle Notizen ohne Zuordnung
└── .obsidian\                   ← Obsidian-Konfiguration (auto-erstellt von der App)
```

---

## Was Claude anlegen kann (ohne Obsidian-App)

Claude Code kann den Ordner und die Unterstruktur anlegen — das geht ohne die App. Die Dateien sind dann schon als Markdown vorhanden und lesbar.

**Was Claude tut** (Pfad aus DEEPWORK-CONFIG.md `DEEPWORK_VAULT_PATH`):
```powershell
$vault = "<DEEPWORK_VAULT_PATH>"  # aus DEEPWORK-CONFIG.md lesen
New-Item -ItemType Directory -Force "$vault\Projects"
New-Item -ItemType Directory -Force "$vault\Inbox"
```

**Was die Obsidian-App beim ersten Öffnen tut:**
- Erstellt `.obsidian\` Konfigurationsordner
- Indexiert alle Markdown-Dateien automatisch
- Erstellt verknüpfte Ansicht der Notizen

---

## Was manuell gemacht werden muss

### Obsidian-App öffnen und Vault verknüpfen

Die Obsidian-App muss einmalig auf den Vault-Ordner zeigen. Das geht so:

1. Obsidian-App öffnen
2. Auf "Open folder as vault" klicken (beim ersten Start) oder "Manage vaults" → "Open folder as vault"
3. Den Ordner aus `DEEPWORK-CONFIG.md` (`DEEPWORK_VAULT_PATH`) auswählen
4. Fertig — Obsidian indexiert alle Dateien automatisch

**Bei Safety-Pause:** Falls Claude diese Aktion anleitet, öffnet er den Obsidian-Download-Link im Browser falls die App noch nicht installiert ist, oder erklärt Schritt für Schritt wie man einen Vault öffnet.

---

## Obsidian-App installieren (falls noch nicht vorhanden)

**Download:** https://obsidian.md/download

Direkt-Links:
- Windows (64-bit): Installer auf der Download-Seite
- Kostenlos für persönliche Nutzung

**Installationsschritte:**
1. Browser öffnen und zur Download-Seite gehen
2. "Download for Windows" klicken
3. Installer herunterladen und ausführen
4. Installation abschließen (Standard-Pfad ist OK)
5. Obsidian starten
6. Bei "Open another vault" → Vault-Pfad aus `DEEPWORK-CONFIG.md` auswählen

---

## Synchronisation mit Projekten

Am Ende jeder deepwork-Phase werden Key-Dokumente in den Vault gespiegelt:

| deepwork-Datei | Vault-Ziel |
|---|---|
| `handoff.md` | `Projects/<slug>/Deepwork/Handoff.md` |
| `.deepwork/PLAN.md` | `Projects/<slug>/Deepwork/Plan.md` |
| `.deepwork/VERDICT.md` | `Projects/<slug>/Deepwork/Verdict.md` |
| `.deepwork/decisions.md` | `Projects/<slug>/Deepwork/Decisions.md` |
| `.deepwork/research/SUMMARY.md` | `Projects/<slug>/Deepwork/Research-Summary.md` |
| `NEXT-STEPS.md` | `Projects/<slug>/Deepwork/Next-Steps.md` |
| `PROJECT-COMPLETE.md` | `Projects/<slug>/Deepwork/Project-Complete.md` |

Das passiert automatisch am Ende jeder Phase — kein manuelles Kopieren nötig.

---

## Obsidian vs. Vector Memory — kurze Erklärung

**Obsidian (primär):**
- Alle wichtigen Projektergebnisse landen hier als lesbare Textdateien
- Funktioniert immer — kein Plugin, kein Programm muss aktiv sein
- Du kannst selbst darin lesen, suchen, bearbeiten

**Ruflo Vector Memory (ergänzend, wenn Ruflo aktiv):**
- Semantic search — findet Infos auch wenn du die Formulierung nicht kennst
- Nur innerhalb einer Session schnell verfügbar
- Ergänzt Obsidian, ersetzt es nicht

**Faustregel:** Alles Wichtige geht in Obsidian. Vector ist der "schnelle Assistent" der sich gut an die aktuelle Session erinnert.

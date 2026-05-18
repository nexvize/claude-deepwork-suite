---
name: deepwork-env-setup
description: "**When: MUST — Run once per machine before starting any deepwork project. Sets up Claude Code in the best possible environment.** Prüft alle Tools, MCPs, Plugins und Einstellungen gegen eine Quality-Baseline, findet Lücken, und führt den User Schritt für Schritt durch die Behebung — ohne jemals etwas ohne Bestätigung zu installieren. Legt auch den Obsidian-Vault an (D:\\Claude\\ObsidianVault\\) falls noch nicht vorhanden. Trigger: 'umgebung einrichten', 'setup', 'claude code optimal einrichten', 'bevor wir starten', 'check environment', '/deepwork-env-setup', oder zu Beginn einer neuen Maschine/Installation."
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
  - Bash
  - AskUserQuestion
  - Skill
---

# deepwork-env-setup: Umgebungs-Setup

**Einmalig pro Maschine ausführen.** Ziel: Claude Code in die beste mögliche Arbeitsumgebung bringen, bevor das erste Projekt startet. Ohne diese Basis fehlen Tools, die alle anderen deepwork-Skills voraussetzen.

**Lies zuerst:**
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/quality-baseline.md` — was muss installiert sein
- `references/hooks-defaults.md` — empfohlene Hook-Konfiguration
- `references/vault-bootstrap.md` — Obsidian-Vault Aufbau

---

## Schritt 1 — Vollständige Inventur (nur lesen, nichts ändern)

Zuerst den IST-Zustand feststellen. In einfacher Sprache erklären, was geprüft wird:

> "Ich schaue mir jetzt an, welche Hilfsprogramme und Erweiterungen bei dir installiert sind, damit ich herausfinden kann, was noch fehlt."

**A. Skills prüfen** (aus system-reminder verfügbar):
- Sind die deepwork-Skills (deepwork-00-bootstrap bis deepwork-entry-analyze, deepwork-env-setup, deepwork-migrate) alle da?

**B. MCPs prüfen** (nicht nur Konfiguration — jedes MCP wirklich aufrufen, nicht nur Listeneintrag prüfen):

Für jedes Pflicht-MCP: einen einfachen Test-Aufruf machen und schauen ob eine Antwort kommt.

| MCP | Test-Aufruf | Was ein Erfolg bedeutet |
|---|---|---|
| `context7` | `mcp__context7__resolve-library-id` mit query "react" | Gibt eine Library-ID zurück |
| `filesystem` | `mcp__filesystem__list_allowed_directories` | Gibt erlaubte Pfade zurück |
| `exa` | `WebSearch` mit einfachem Begriff (als Proxy) | Gibt Ergebnisse zurück |
| `firecrawl` | Kleinen bekannten URL scrapen (z.B. example.com) | Gibt Seiteninhalt zurück |
| `obsidian` | Vault-Ordner lesen falls vorhanden | Gibt Ordnerstruktur zurück |
| `playwright` | `mcp__plugin_playwright_playwright__browser_snapshot` | Gibt DOM zurück |

**Ergebnis:** Für jedes MCP festhalten: `installiert + funktioniert` / `installiert, aber Fehler: <was>` / `nicht installiert`

Ein MCP das nur in der Konfiguration steht aber keine Antwort gibt, zählt als NICHT verfügbar.

**C. Ruflo-Plugins prüfen** (aus system-reminder):
- ruflo-swarm (parallele Arbeit mit mehreren Helfern gleichzeitig)
- ruflo-autopilot (vollautomatischer Modus)
- ruflo-loop-workers (Hintergrund-Aufgaben)
- ruflo-cost-tracker (Kosten im Blick behalten)
- ruflo-knowledge-graph (Wissens-Netzwerk)

**D. Obsidian-Vault prüfen:**
- Existiert `D:\Claude\ObsidianVault\`?
- Existiert `D:\Claude\ObsidianVault\Projects\`?

**E. Hooks prüfen** (`~/.claude/settings.json`):
- Welche Hooks sind konfiguriert?

**F. ENVIRONMENT.md prüfen:**
- Existiert `~/.claude/ENVIRONMENT.md`? Falls ja: wann war der letzte Check?

Alles sammeln — noch nichts ausgeben.

---

## Schritt 2 — Gap-Analyse und Ergebnis zeigen

Ausgabe in klarer, einfacher Sprache. Kein Tech-Jargon ohne Erklärung:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DEINE CLAUDE CODE UMGEBUNG — AKTUELLER STAND
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✓ Vorhanden:
  <liste was gut ist>

⚠️ Fehlt oder nicht optimal:
  <liste was fehlt>

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Schritt 3 — Lücken Schritt für Schritt schließen

Für jede Lücke: erst erklären was es ist und warum es wichtig ist, dann fragen ob installiert werden soll. Niemals mehrere Dinge auf einmal — immer eine nach der anderen.

**Format pro Lücke:**

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ FEHLT: <Name in normaler Sprache>

Was ist das?
<1–2 Sätze ohne Fachbegriffe>

Warum brauchst du das?
<Konkret: was geht ohne das nicht, oder schlechter>

Was ich dafür tue:
<Beschreibung der Aktion in normaler Sprache>

Technischer Befehl (falls du neugierig bist):
<der eigentliche Befehl>

Soll ich das jetzt einrichten? (ja / überspringen / erklär mir mehr)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Reihenfolge der Lücken (von wichtig nach optional):**
1. Obsidian-Vault (Langzeit-Gedächtnis für Projekte)
2. context7 MCP (aktuelle Dokumentation nachschlagen)
3. filesystem MCP (Dateizugriff über Projektgrenzen hinaus)
4. exa MCP (tiefe Web-Recherche)
5. firecrawl MCP (vollständige Webseiten einlesen)
6. Ruflo-Plugins (parallele Arbeit, Autopilot, Kosten-Tracking)
7. Hooks (automatische Verhaltensregeln)
8. obsidian MCP (direkter Vault-Zugriff)
9. playwright MCP (Browser-Automatisierung)

**Bei Webbrowser-Aktionen (Login, Konfiguration im Browser):**
Lese `references/vault-bootstrap.md` für den genauen Ablauf. Immer:
1. Browser öffnen: `start <url>` (Windows) oder `open <url>` (Mac)
2. Genau beschreiben was zu tun ist: welche Buttons, welche Felder
3. Warten auf Bestätigung des Users

---

## Schritt 4 — Hooks konfigurieren

Lese `references/hooks-defaults.md`. Für jeden empfohlenen Hook:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
EMPFOHLENE EINSTELLUNG: <Hook-Name in normaler Sprache>

Was macht das?
<1 Satz: was passiert automatisch, wenn dieser Hook aktiv ist>

Beispiel:
<konkretes Beispiel wann das nützlich ist>

Soll ich das aktivieren? (ja / nein / was ist das genau?)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Schritt 5 — Vault-Struktur anlegen

Lese `references/vault-bootstrap.md`.

Vault-Pfad aus `DEEPWORK-CONFIG.md` lesen (`DEEPWORK_VAULT_PATH`).

Falls der Vault noch nicht existiert oder unvollständig ist: anlegen.
Falls bereits vorhanden: prüfen ob Unterstruktur stimmt, fehlende Ordner ergänzen.

In Klartext erklären was angelegt wird und warum:
> "Ich lege jetzt die Ordnerstruktur für deinen Wissens-Speicher an. Das ist der Ort, wo alle wichtigen Erkenntnisse aus unseren Projekten dauerhaft gespeichert werden — auch wenn du die Unterhaltung neu startest."

---

## Schritt 6 — ENVIRONMENT.md schreiben

Snapshot des aktuellen Stands als `~/.claude/ENVIRONMENT.md`:

```markdown
# Claude Code Environment — Baseline Snapshot
Datum: <ISO-8601>
Nächster empfohlener Check: in 30 Tagen

## Installierte MCPs
| MCP | Status | Zweck |
|---|---|---|
| context7 | <installiert/fehlt> | Dokumentation nachschlagen |
| filesystem | <installiert/fehlt> | Dateizugriff |
| exa | <installiert/fehlt> | Tiefe Web-Recherche |
| firecrawl | <installiert/fehlt> | Webseiten einlesen |
| obsidian | <installiert/fehlt> | Vault-Zugriff |
| playwright | <installiert/fehlt> | Browser-Automatisierung |

## Ruflo-Plugins
| Plugin | Status | Zweck |
|---|---|---|
| ruflo-swarm | <ja/nein> | Parallele Helfer |
| ruflo-autopilot | <ja/nein> | Vollautomatischer Modus |
| ruflo-loop-workers | <ja/nein> | Hintergrund-Aufgaben |
| ruflo-cost-tracker | <ja/nein> | Kosten im Blick |
| ruflo-knowledge-graph | <ja/nein> | Wissens-Netzwerk |

## Obsidian-Vault
Pfad: <aus DEEPWORK-CONFIG.md: DEEPWORK_VAULT_PATH>
Status: <vorhanden/angelegt/fehlt>

## Aktive Hooks
<liste der konfigurierten Hooks>

## Offene Lücken (bewusst übersprungen)
<was der User übersprungen hat und warum>

## Deepwork-Skills
<status: alle vorhanden / fehlende auflisten>
```

---

## Schritt 7 — Abschluss

```
═══════════════════════════════════════════════════
SETUP ABGESCHLOSSEN
═══════════════════════════════════════════════════
Deine Umgebung ist jetzt bereit für deepwork-Projekte.

Was eingerichtet wurde:
<kurze Liste in normaler Sprache>

Was noch fehlt (falls übersprungen):
<kurze Liste + Hinweis dass du es später nachholen kannst>

Nächster Schritt:
Für ein neues Projekt: /deepwork-00-bootstrap
Für ein bestehendes Projekt: /deepwork-entry-analyze

Tipp: Dieser Setup-Check empfiehlt sich alle 30 Tage oder
      nach größeren Updates von Claude Code.
═══════════════════════════════════════════════════
```

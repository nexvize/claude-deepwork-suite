---
name: deepwork-env-setup
description: "**When: MUST — Run once per machine before starting any deepwork project. Also run when starting a new project type (design, media, etc.) to check type-specific tools.** Prüft alle Tools, MCPs, Plugins und Einstellungen gegen eine Quality-Baseline. Führt Auto-Discovery aus: sucht auf GitHub und im Plugin-Store nach Skills/MCPs die deinen Workflow verbessern würden — und macht installierbare Vorschläge. Typ-bewusst: für Design-Projekte wird Figma MCP geprüft, für Media-Projekte higgsfield, etc. Trigger: 'umgebung einrichten', 'setup', 'claude code optimal einrichten', 'bevor wir starten', 'check environment', '/deepwork-env-setup', neue Maschine, oder nach Projekttyp-Wahl."
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
  - Bash
  - AskUserQuestion
  - Skill
---

# deepwork-env-setup: Umgebungs-Setup + Auto-Discovery

**Einmalig pro Maschine ausführen — oder nach Projekttyp-Wahl um typ-spezifische Tools zu prüfen.**

Ziel: Claude Code in die beste mögliche Arbeitsumgebung bringen. Findet was fehlt, macht installierbare Vorschläge — ohne jemals etwas ohne Bestätigung zu ändern.

**Lies zuerst:**
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap
- `references/quality-baseline.md` — was muss installiert sein
- `references/project-profiles.md` — welche MCPs/Tools pro Projekttyp gebraucht werden
- `references/auto-discovery-protocol.md` — wie Auto-Discovery durchgeführt wird
- `references/hooks-defaults.md` — empfohlene Hook-Konfiguration
- `references/vault-bootstrap.md` — Obsidian-Vault Aufbau

---

## Schritt 1 — Vollständige Inventur (nur lesen, nichts ändern)

> "Ich schaue mir jetzt an, welche Hilfsprogramme und Erweiterungen bei dir installiert sind."

**A. Skills prüfen** (aus system-reminder):
- Sind alle deepwork-Skills vorhanden?
- Welche anderen Skills (gsd-*, ui-ux-pro-max, etc.) sind installiert?

**B. MCPs prüfen** — jeden wirklich aufrufen, nicht nur Konfiguration prüfen:

| MCP | Test-Aufruf | Erfolg |
|---|---|---|
| `context7` | `mcp__context7__resolve-library-id` query="react" | Gibt Library-ID zurück |
| `filesystem` | `mcp__filesystem__list_allowed_directories` | Gibt Pfade zurück |
| `exa` | WebSearch mit Begriff | Gibt Ergebnisse zurück |
| `firecrawl` | `mcp__firecrawl__firecrawl_scrape` url="https://example.com" | Gibt Seiteninhalt zurück |
| `obsidian` | Vault-Ordner lesen falls vorhanden | Gibt Ordnerstruktur zurück |
| `playwright` | `mcp__plugin_playwright_playwright__browser_snapshot` | Gibt DOM zurück |
| `higgsfield` | `mcp__higgsfield__balance` | Gibt Account-Status zurück |

**C. Ruflo-Plugins prüfen** (aus system-reminder):
- ruflo-swarm, ruflo-autopilot, ruflo-loop-workers, ruflo-cost-tracker, ruflo-knowledge-graph

**D. Obsidian-Vault prüfen:**
- `D:\Claude\ObsidianVault\` vorhanden?
- Unterstruktur `Projects\` + `Inbox\` vorhanden?

**E. Hooks prüfen** (`~/.claude/settings.json`):
- Welche Hooks sind konfiguriert?

**F. Projekttyp-Kontext:**
Falls ein Projekt aktiv ist: `project_type` aus `.deepwork/planning/PROJECT.md` lesen.
Das bestimmt welche typ-spezifischen Tools zusätzlich geprüft werden.

---

## Schritt 2 — Gap-Analyse + Ergebnis zeigen

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DEINE CLAUDE CODE UMGEBUNG — AKTUELLER STAND
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✓ Vorhanden und funktioniert:
  <liste>

⚠️ Fehlt oder nicht optimal:
  <liste>

<Falls Projekttyp bekannt:>
📌 Typ-spezifische Lücken (<projekttyp>-Projekt):
  <was für diesen Typ besonders wichtig wäre>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Schritt 2.5 — Auto-Discovery: Was könnte fehlen?

Führe `references/auto-discovery-protocol.md` aus:

1. **GitHub-Scan** (via `mcp__plugin_github_github__search_repositories`):
   - Suche: `topic:claude-code-skill` + Projekttyp-Keywords
   - Vergleiche mit installierten Skills
   - Identifiziere relevante Repos mit >5 Stars

2. **Plugin-Store-Scan** (via `mcp__ruflo__transfer_plugin-search` falls verfügbar):
   - Suche nach Plugins relevant für aktiven Projekttyp
   - Vergleiche mit `enabledPlugins` in settings.json

3. **Typ-spezifische MCP-Lücken** (aus `references/project-profiles.md`):
   - Für coding-Projekte: context7 + github Pflicht
   - Für design-Projekte: Figma MCP Pflicht
   - Für media-Projekte: higgsfield Pflicht
   - Für research/analysis: exa + firecrawl Pflicht
   - etc.

**Empfehlungs-Block ausgeben:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AUTO-DISCOVERY — Potenzielle Verbesserungen
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
<Falls Projekttyp: "Für dein <typ>-Projekt gefunden:">

⚡ SOFORT INSTALLIERBAR (via claude mcp add):
  • <name> — <was es tut in 1 Satz>
    Befehl: claude mcp add <name> <command>

💡 EMPFOHLEN (manuelle Einrichtung):
  • <plugin-name> — <was es tut>

📦 INTERESSANT (optional):
  • <tool-name> — <warum nützlich>

Nichts gefunden? → Umgebung ist bereits optimal für diesen Projekttyp.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Sicherheitsregeln:
- Nur Quellen mit nachvollziehbarer Provenienz (offizielle Anthropic, bekannte MCPs, GitHub >5 stars)
- Niemals automatisch installieren — immer y/skip fragen
- Keine Änderungen an ~/.claude.json

---

## Schritt 3 — Lücken schließen

Für jede Lücke: erst erklären, dann fragen. Einzeln — nie mehrere auf einmal.

**Format pro Lücke:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
⚠️ FEHLT: <Name in normaler Sprache>

Was ist das?
<1–2 Sätze ohne Fachbegriffe>

Warum brauchst du das?
<Konkret: was geht ohne das nicht>

<Falls typ-spezifisch:>
Besonders wichtig für: <typ>-Projekte — <warum>

Soll ich das jetzt einrichten? (ja / überspringen / erklär mehr)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Reihenfolge (wichtig → optional):**
1. Obsidian-Vault (Langzeit-Gedächtnis)
2. context7 MCP (aktuelle Dokumentation)
3. filesystem MCP (Dateizugriff)
4. exa MCP (tiefe Web-Recherche)
5. firecrawl MCP (Webseiten einlesen)
6. Typ-spezifische MCPs (Figma für design, higgsfield für media, etc.)
7. Ruflo-Plugins (parallele Arbeit, Autopilot, Kosten)
8. Hooks
9. obsidian MCP (direkter Vault-Zugriff)
10. playwright MCP (Browser-Automatisierung)
11. Auto-Discovery-Empfehlungen

---

## Schritt 4 — Hooks konfigurieren

Lese `references/hooks-defaults.md`. Für jeden empfohlenen Hook einzeln bestätigen.

---

## Schritt 5 — Vault-Struktur anlegen

Lese `references/vault-bootstrap.md`. Vault-Pfad aus DEEPWORK-CONFIG.md.

Falls Vault fehlt oder unvollständig: anlegen.

---

## Schritt 6 — ENVIRONMENT.md schreiben / aktualisieren

```markdown
# Claude Code Environment — Baseline Snapshot
Datum: <ISO-8601>
Nächster empfohlener Check: in 30 Tagen

## Installierte MCPs
| MCP | Status | Zweck |
...

## Ruflo-Plugins
...

## Obsidian-Vault
Pfad: <DEEPWORK_VAULT_PATH>
Status: <vorhanden/angelegt/fehlt>

## Auto-Discovery Ergebnisse
Letzter Scan: <datum>
Empfehlungen umgesetzt: <liste>
Empfehlungen übersprungen: <liste>

## Aktive Hooks
<liste>

## Deepwork-Skills
<status>

## Offene Lücken
<was übersprungen wurde>
```

---

## Schritt 7 — Abschluss

```
═══════════════════════════════════════════════════
SETUP ABGESCHLOSSEN
═══════════════════════════════════════════════════
Deine Umgebung ist jetzt bereit für deepwork-Projekte.

Was eingerichtet wurde:
<kurze Liste>

Auto-Discovery: <N> Verbesserungen gefunden, <M> installiert

Was noch fehlt (falls übersprungen):
<liste + Hinweis>

Nächster Schritt:
Für ein neues Projekt:      /deepwork-00-bootstrap
Für bestehendes Projekt:    /deepwork-entry-analyze
Für einzelne Protokolle:    /deepwork-quick

Tipp: Dieser Check empfiehlt sich alle 30 Tage oder
      wenn du mit einem neuen Projekttyp beginnst.
═══════════════════════════════════════════════════
```

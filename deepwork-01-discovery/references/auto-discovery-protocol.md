# Auto-Discovery Protocol

## Zweck

Der Auto-Discovery-Protokoll macht die Deepwork Suite selbstverbessernd: anstatt stumm mit dem zu arbeiten was vorhanden ist, scannt das System aktiv nach Skills, MCPs, Plugins und Hooks die fehlen — und präsentiert dem User konkrete, sofort ausführbare Empfehlungen. Das Ziel ist, dass jedes Projekt mit dem bestmöglichen Toolset startet, nicht mit dem Toolset das zufällig schon installiert war. Discovery ist kein einmaliger Scan — er ist Teil des Onboardings für jeden Projekttyp und kann jederzeit auf Abruf wiederholt werden.

---

## Wann ausführen

- **In `deepwork-env-setup`:** vollständiger Scan (alle Projekttypen, keine Vorannahmen über den Kontext)
- **In `deepwork-00-bootstrap`:** nach Projekttyp-Wahl — typ-spezifischer Schnell-Scan (nur relevante Gaps)
- **Auf Abruf:** in `deepwork-quick` als wählbare Option "Auto-Discovery ausführen"
- **Manuell:** wenn der User explizit fragt "Welche Tools fehlen?" oder "Was sollte ich noch installieren?"

---

## Schritt 1 — Inventur: Was ist installiert?

Vor dem Scannen nach Lücken muss bekannt sein was bereits vorhanden ist. Immer alle vier Kategorien prüfen — nie nur eine, nie aus dem Gedächtnis.

### 1a — Installierte Skills

```
Glob("~/.claude/skills/**/*.md")
```

Aus dem Ergebnis: Verzeichnisnamen auf oberster Ebene unter `~/.claude/skills/` extrahieren — das sind die installierten Skills.

Alternativ: System-Reminder des aktuellen Turns enthält oft eine "available-skills" Liste — diese direkt verwenden wenn vorhanden und vollständig.

Ziel-Output: Eine flache Liste aller installierten Skill-Namen.
```
installierte_skills = [
  "deepwork-00-bootstrap",
  "deepwork-01-discovery",
  "frontend-design",
  "gsd-debug",
  ...
]
```

### 1b — Aktive MCPs

```
Read("~/.claude.json")
```

Navigiere zum Schlüssel `mcpServers`. Extrahiere alle Keys (= MCP-Namen) und deren `command`/`url`-Felder.

Ziel-Output:
```
aktive_mcps = [
  "context7",
  "filesystem",
  "exa",
  "playwright",
  "memory",
  ...
]
```

Hinweis: Wenn `~/.claude.json` nicht lesbar ist (Berechtigungsfehler), prüfe ob die MCPs im System-Reminder aufgeführt sind (MCP Server Instructions Block). Nutze diesen als Fallback.

### 1c — Aktive Plugins

```
Read("~/.claude/settings.json")
```

Navigiere zu `enabledPlugins` (Array von Plugin-Namen).

### 1d — Aktive Hooks

Im gleichen `settings.json`: navigiere zu `hooks`. Liste alle konfigurierten Hook-Typen und ihre Commands.

### 1e — Inventur dokumentieren

Falls `.deepwork/tool-inventory.md` noch nicht existiert, anlegen. Falls es existiert, aktualisieren.

---

## Schritt 2 — Projekttyp-Kontext laden

**Projekttyp ermitteln (Prioritätsreihenfolge):**
1. Lese `.deepwork/planning/PROJECT.md` → Feld `project_type`
2. Falls nicht vorhanden: Lese `handoff.md` → Feld `project_type`
3. Falls immer noch nicht bekannt: Frage den User via `AskUserQuestion`

---

## Schritt 3 — Lücken identifizieren

### 3a — Skills scannen (GitHub)

**Suchanfragen ausführen** (parallel, via `mcp__plugin_github_github__search_repositories`):

```
Query 1: "claude-code-skill topic:claude-code"
Query 2: "claude skill <project_type>"
Query 3: "anthropic claude code extension"
```

**Pro gefundenem Repo prüfen:**
- Mindestens 10 Stars? → Vertrauenswürdig
- Hat es eine `SKILL.md` oder `README.md` die es als Claude Code Skill identifiziert?
- Ist der Skill-Name bereits in `installierte_skills`? → Überspringen

### 3b — MCP-Lücken (typ-spezifisch)

| MCP | Projekttypen | Install-Command |
|---|---|---|
| `context7` | alle | `claude mcp add context7 -- npx -y @upstash/context7-mcp` |
| `exa` | research, content, marketing | `claude mcp add exa -- npx -y exa-mcp-server` |
| `firecrawl` | research, content, marketing | `claude mcp add firecrawl -- npx -y firecrawl-mcp` |
| `playwright` | software, frontend, fullstack | `claude mcp add playwright -- npx -y @playwright/mcp` |
| `filesystem` | alle | `claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem <allowed-paths>` |
| `memory` | alle langfristigen Projekte | `claude mcp add memory -- npx -y @modelcontextprotocol/server-memory` |
| `sequential-thinking` | research, analysis, concept | `claude mcp add sequential-thinking -- npx -y @modelcontextprotocol/server-sequential-thinking` |
| `github` | software, fullstack, alle mit Repo | `claude mcp add github -- npx -y @modelcontextprotocol/server-github` |

### 3c — Plugin-Lücken

**Mindest-Plugins für produktive Deepwork-Sessions:**
```
pflicht_plugins = [
  "ruflo-autopilot",   // für autonome Loops
  "ruflo-swarm",       // für parallele Agents
  "ruflo-loop-workers" // für Hintergrund-Tasks
]
```

### 3d — Hook-Lücken

| Hook-Typ | Command | Zweck | Priorität |
|---|---|---|---|
| `Stop` | ruflo hooks_post-task | Fortschritt nach jeder Antwort sichern | EMPFOHLEN |
| `PreToolUse` | ruflo hooks_pre-edit | Pre-Edit-Kontrolle | OPTIONAL |
| `PostToolUse` | ruflo hooks_post-edit | Post-Edit-Log | OPTIONAL |

---

## Schritt 4 — Empfehlungs-Block ausgeben

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AUTO-DISCOVERY ERGEBNIS — <project_type> — <datum>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

BEREITS INSTALLIERT ✓
  Skills: <N> installiert
  MCPs:   <N> aktiv
  Plugins: <N> aktiv
  Hooks:  <N> konfiguriert

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SOFORT INSTALLIERBAR (ich kann das für dich tun)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  [1] <mcp-name> — <was es macht für dieses Projekt>
      Befehl: claude mcp add <name> -- <full command>

Soll ich die "Sofort installierbar" Items jetzt installieren?
Antworte mit: "ja alle" / "ja [1] [3]" / "nein danke" / "zeig mir zuerst mehr zu [1]"
```

---

## Schritt 5 — Installation (auf Bestätigung)

**Erst nach expliziter User-Bestätigung handeln.** Nie sofort installieren.

---

## Sicherheits-Regeln

1. **Niemals automatisch installieren ohne y-Bestätigung**
2. **Keine Veränderungen an `~/.claude.json` außer via `claude mcp add`**
3. **Nur vertrauenswürdige Quellen:** Offizielle Anthropic-Packages, Ruflo-Ecosystem-Plugins, GitHub Repos mit ≥10 Stars
4. **Web-Safety-Regel gilt:** Kein Auto-Download von unbekannten Quellen
5. **Keine Entfernung existierender Konfiguration:** Discovery fügt hinzu — es entfernt nie
6. **Scope-Isolation:** Empfehlungen immer mit `--scope project` installieren wenn sinnvoll

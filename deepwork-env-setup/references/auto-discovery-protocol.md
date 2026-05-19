# Auto-Discovery Protocol

## Zweck

Der Auto-Discovery-Protokoll macht die Deepwork Suite selbstverbessernd: anstatt stumm mit dem zu arbeiten was vorhanden ist, scannt das System aktiv nach Skills, MCPs, Plugins und Hooks die fehlen — und präsentiert dem User konkrete, sofort ausführbare Empfehlungen. Das Ziel ist, dass jedes Projekt mit dem bestmöglichen Toolset startet, nicht mit dem Toolset das zufällig schon installiert war. Discovery ist kein einmaliger Scan — er ist Teil des Onboardings für jeden Projekttyp und kann jederzeit auf Abruf wiederholt werden.

---

## Wann ausführen

- **In `deepwork-env-setup`:** vollständiger Scan (alle Projekttypen, keine Vorannahmen)
- **In `deepwork-00-bootstrap`:** nach Projekttyp-Wahl — typ-spezifischer Schnell-Scan
- **Auf Abruf:** in `deepwork-quick` als wählbare Option
- **Manuell:** wenn der User explizit fragt "Welche Tools fehlen?"

---

## Schritt 1 — Inventur: Was ist installiert?

### 1a — Installierte Skills

```
Glob("~/.claude/skills/**/*.md")
```

Verzeichnisnamen auf oberster Ebene unter `~/.claude/skills/` extrahieren.

```
installierte_skills = [
  "deepwork-00-bootstrap",
  "deepwork-01-discovery",
  "frontend-design",
  ...
]
```

### 1b — Aktive MCPs

```
Read("~/.claude.json")
```

Schlüssel `mcpServers` navigieren. Alle Keys extrahieren.

```
aktive_mcps = ["context7", "filesystem", "exa", "playwright", "memory", ...]
```

Hinweis: Wenn `~/.claude.json` nicht lesbar, MCPs aus System-Reminder ziehen.

### 1c — Aktive Plugins

```
Read("~/.claude/settings.json")
```

Navigiere zu `enabledPlugins`.

### 1d — Aktive Hooks

Im gleichen `settings.json`: navigiere zu `hooks`.

### 1e — Inventur dokumentieren

Falls `.deepwork/tool-inventory.md` nicht existiert, anlegen. Falls vorhanden, aktualisieren:

```markdown
## Installed — <YYYY-MM-DD>

### Skills
<liste>

### MCPs
<liste>

### Plugins
<liste>

### Hooks
<liste>
```

---

## Schritt 2 — Projekttyp-Kontext laden

**Projekttyp ermitteln:**
1. Lese `.deepwork/planning/PROJECT.md` → Feld `project_type`
2. Falls nicht: Lese `handoff.md` → Feld `project_type`
3. Falls immer noch nicht: Frage User via `AskUserQuestion`

**Typ-Fokus-Mapping:**

| Projekttyp | Fokus-Scan |
|---|---|
| coding | Playwright, GitHub MCP, context7, security-review Skill |
| design | Figma MCP, frontend-design Skill, ui-ux-pro-max Skill |
| content / marketing | SEO Skill, exa, firecrawl |
| research / analysis | exa, firecrawl, context7, sequential-thinking MCP |
| media | higgsfield MCP, Figma MCP, exa |
| concept / education | exa, firecrawl, Gamma MCP |
| automation | context7, github, playwright |
| legal / finance | exa, firecrawl, sequential-thinking |
| unknown | Vollständiger Scan über alle Kategorien |

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
- Mindestens 10 Stars?
- Hat `SKILL.md` oder `README.md` die es als Claude Code Skill identifiziert?
- Skill-Name bereits in `installierte_skills`? → Überspringen

**Gap-Liste:**
```
skill_gaps = [
  {
    "name": "<skill-name>",
    "repo": "<github-url>",
    "stars": <n>,
    "description": "<was es macht>",
    "relevanz": "HIGH/MEDIUM/LOW für <project_type>"
  }
]
```

Relevanz-Kriterien:
- HIGH: Direkt für Kernaufgabe nötig
- MEDIUM: Würde Qualität oder Effizienz deutlich verbessern
- LOW: Interessant, aber optional

### 3b — MCP-Lücken (typ-spezifisch)

**Empfehlungs-Tabelle:**

| MCP | Projekttypen | Install-Command |
|---|---|---|
| `context7` | alle | `claude mcp add context7 -- npx -y @upstash/context7-mcp` |
| `exa` | research, content, marketing | `claude mcp add exa -- npx -y exa-mcp-server` |
| `firecrawl` | research, content, marketing | `claude mcp add firecrawl -- npx -y firecrawl-mcp` |
| `playwright` | coding, design, automation | `claude mcp add playwright -- npx -y @playwright/mcp` |
| `filesystem` | alle | `claude mcp add filesystem -- npx -y @modelcontextprotocol/server-filesystem <paths>` |
| `memory` | alle langfristigen Projekte | `claude mcp add memory -- npx -y @modelcontextprotocol/server-memory` |
| `sequential-thinking` | research, analysis, concept | `claude mcp add sequential-thinking -- npx -y @modelcontextprotocol/server-sequential-thinking` |
| `github` | coding, automation | `claude mcp add github -- npx -y @modelcontextprotocol/server-github` |

### 3c — Plugin-Lücken

**Mindest-Plugins für produktive Deepwork-Sessions:**
```
pflicht_plugins = [
  "ruflo-autopilot",   // für autonome Loops
  "ruflo-swarm",       // für parallele Agents
  "ruflo-loop-workers" // für Hintergrund-Tasks
]
```

Optionale Ergänzungen:
```
optional_plugins = {
  "coding / automation": ["ruflo-observability", "ruflo-cost-tracker"],
  "research": ["ruflo-knowledge-graph"],
  "alle": ["ruflo-cost-tracker"]
}
```

### 3d — Hook-Lücken

| Hook-Typ | Command | Zweck | Priorität |
|---|---|---|---|
| `Stop` | ruflo hooks_post-task | Fortschritt nach jeder Antwort sichern | EMPFOHLEN |
| `PreToolUse` | ruflo hooks_pre-edit | Pre-Edit-Kontrolle | OPTIONAL |
| `PostToolUse` | ruflo hooks_post-edit | Post-Edit-Log | OPTIONAL |

Hinweis: Hook-Installation immer via `update-config` Skill.

---

## Schritt 4 — Empfehlungs-Block ausgeben

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
AUTO-DISCOVERY ERGEBNIS — <project_type> — <datum>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

BEREITS INSTALLIERT ✓
  Skills: <N> installiert
  MCPs:   <N> aktiv
  Plugins: <N> aktiv
  Hooks:  <N> konfiguriert

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SOFORT INSTALLIERBAR (ich kann das für dich tun)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  [1] <mcp-name> — <was es macht für dieses Projekt>
      Befehl: claude mcp add <name> -- <full command>

  [2] <mcp-name> — <was es macht>
      Befehl: claude mcp add <name> -- <full command>

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
EMPFOHLEN — MANUELL (kurze Anleitung)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  • <plugin-name> — <Nutzen> — ruflo store
  • <skill-name> — <Nutzen> — git clone <repo> in ~/.claude/skills/

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
INTERESSANT (optional)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  • <name> — <warum interessant>

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Soll ich die "Sofort installierbar" Items jetzt installieren?
Antworte mit: "ja alle" / "ja [1] [3]" / "nein danke" / "zeig mir zuerst mehr zu [1]"
```

---

## Schritt 5 — Installation (auf Bestätigung)

**Erst nach expliziter User-Bestätigung handeln.** Nie sofort installieren.

**Wenn User "ja alle":** Alle Sofort-Installierbar-Items nacheinander ausführen.

**Wenn User einzelne Items nennt:** Nur die genannten installieren.

**Wenn User "nein danke":** Akzeptieren ohne Nachfragen.

**Nach jeder Installation — Log in `~/.claude/ENVIRONMENT.md`:**
```markdown
## <YYYY-MM-DD> — Auto-Discovery Installation

### Installiert
- <mcp-name>: `<install command>` — <warum empfohlen>

### Empfohlen aber nicht installiert
- <name>: User hat abgelehnt
```

**Hook-Installation:** Immer via `Skill` tool → `update-config` delegieren.

---

## Sicherheits-Regeln

1. **Niemals automatisch installieren ohne Bestätigung**
2. **Keine Veränderungen an `~/.claude.json` außer via `claude mcp add`**
3. **Nur vertrauenswürdige Quellen:** Offizielle Anthropic-Packages, Ruflo Store, GitHub Repos mit ≥10 Stars
4. **Web-Safety-Regel gilt:** Kein Auto-Download ohne Quell-Verifikation
5. **Keine Entfernung existierender Konfiguration:** Discovery fügt hinzu — entfernt nie
6. **Scope-Isolation:** Mit `--scope project` installieren wenn sinnvoll

---

## Fehlerbehandlung

- **GitHub MCP nicht verfügbar:** Schritt 3a überspringen, im Block als ersten Eintrag unter "Sofort installierbar" aufnehmen
- **`~/.claude.json` nicht lesbar:** MCP-Inventur aus System-Reminder ziehen
- **`settings.json` nicht lesbar:** `aktive_plugins = []` annehmen
- **Ruflo Plugin-Search nicht verfügbar:** Minimalliste (pflicht_plugins) verwenden
- **Kein Projekttyp:** Vollständiger Scan über alle Typen

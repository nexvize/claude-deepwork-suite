# Quality-Baseline — Was muss installiert sein

Diese Liste definiert, was für die bestmögliche deepwork-Umgebung benötigt wird. Die Skill `deepwork-env-setup` prüft gegen diese Baseline und hilft beim Schließen der Lücken.

---

## Pflicht-MCPs (ohne diese funktionieren Kernfunktionen nicht optimal)

| MCP | Was es tut (einfach erklärt) | Warum Pflicht | Ohne es fehlt |
|---|---|---|---|
| `context7` | Schlägt aktuelle Dokumentation für Programme und Bibliotheken nach | Falsche oder veraltete Infos beim Bauen vermeiden | Recherche kann auf veraltete Infos basieren |
| `filesystem` | Erlaubt Zugriff auf Dateien außerhalb des aktuellen Projektordners | Zugriff auf Vault, andere Projekte, System-Konfigurationen | Kann nur im aktuellen Ordner arbeiten |
| `exa` | Tiefe Web-Recherche (findet auch was normale Suchen übersehen) | Tellerrand-Recherche in deepwork-01 | Nur oberflächliche Web-Ergebnisse |
| `firecrawl` | Liest Webseiten vollständig ein — auch komplexe, JavaScript-basierte | Dokumentationen und Wissensquellen vollständig erfassen | Manche Seiten nur teilweise lesbar |

## Empfohlene MCPs (stark empfohlen, aber nicht zwingend)

| MCP | Was es tut | Wann besonders nützlich |
|---|---|---|
| `obsidian` | Direkter Zugriff auf den Obsidian-Vault über MCP | Schnelles Lesen/Schreiben in den Vault ohne filesystem-Umweg |
| `playwright` | Steuert einen Browser automatisch | Wenn Web-Aktionen nötig sind, die Claude sonst nicht tun kann |
| `sequential-thinking` | Strukturiertes Schritt-für-Schritt-Denken für komplexe Probleme | Bei schwierigen Analyse- und Planungsaufgaben |
| `memory` | Knowledge-Graph für semantisch verknüpfte Erinnerungen | Wenn Ruflo Memory nicht verfügbar oder als Ergänzung |

## Ruflo-Plugins (für Parallelarbeit, Autopilot und Kosten-Tracking)

| Plugin | Was es tut (einfach erklärt) | Ohne es fehlt |
|---|---|---|
| `ruflo-swarm` | Startet viele Helfer gleichzeitig, die parallel an verschiedenen Teilen arbeiten | Langsame sequentielle Arbeit, kein Mega-Prototyp-Modus |
| `ruflo-autopilot` | Vollautomatischer Modus (deepwork-alt-autopilot) | Autopilot-Skill funktioniert nicht |
| `ruflo-loop-workers` | Hintergrund-Aufgaben die regelmäßig ausgeführt werden | Keine automatischen Wiederholungen |
| `ruflo-cost-tracker` | Verfolgt genau was jede Aktion kostet | Kosten-Übersicht und Budget-Kontrolle fehlen |
| `ruflo-knowledge-graph` | Erstellt verknüpfte Wissens-Netzwerke aus Recherche-Ergebnissen | Weniger strukturierte Wissensorganisation |

### Ruflo-Plugins installieren — Schritt-für-Schritt

**Wichtig:** Ruflo-Plugins können NICHT automatisch von Claude installiert werden. Sie müssen manuell über das Claude Code Plugin-System eingerichtet werden.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MANUELLE INSTALLATION — Ruflo-Plugins
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Was zu tun ist:

1. Claude Code öffnen (falls nicht schon offen)

2. In Claude Code: Einstellungen öffnen
   → Drücke Ctrl+Shift+P (oder Cmd+Shift+P auf Mac)
   → Tippe "Claude Code: Open Settings"
   
3. Im Einstellungs-Fenster: "Plugins" oder "Extensions" suchen
   → Ruflo im Plugin-Verzeichnis suchen
   → Installieren klicken

4. Alternativ: Über die Ruflo-Website
   → https://ruflo.ai (prüfe aktuelle URL)
   → Anleitung für Claude Code Integration folgen
   → API-Key generieren und in Claude Code eintragen

5. Nach Installation: Claude Code neu starten
   → Neue Session öffnen
   → /deepwork-env-setup erneut ausführen um zu prüfen ob Plugins aktiv sind

Was Claude tun kann (automatisch):
  ✓ MCPs installieren: z.B. claude mcp add context7 npx -y @upstash/context7-mcp
  ✓ MCP-Status prüfen
  ✗ Ruflo-Plugins installieren (geht nicht, muss manuell sein)

Bei Fragen zur Ruflo-Installation: ruflo.ai/docs
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Obsidian-Vault (dauerhafter Projektspeicher)

| Was | Pfad | Warum wichtig |
|---|---|---|
| Vault-Root | `D:\Claude\ObsidianVault\` | Basisordner — ohne ihn kein Vault |
| Projekte | `D:\Claude\ObsidianVault\Projects\` | Ein Unterordner pro deepwork-Projekt |
| Inbox | `D:\Claude\ObsidianVault\Inbox\` | Für schnelle Notizen ohne Zuordnung |

Obsidian-App: https://obsidian.md/download (kostenlos, muss manuell installiert werden)

## Auto-Memory (eingebaut, immer aktiv)

Das eingebaute Memory-System (`~/.claude/projects/.../memory/`) ist immer aktiv und braucht keine Installation. Es dient als primärer Kurzzeit-Speicher zwischen Sessions.

## Deepwork-Skills

Alle diese Skills müssen vorhanden sein:

| Skill | Rolle |
|---|---|
| `deepwork-env-setup` | Einmalig: Umgebung einrichten |
| `deepwork-00-bootstrap` | Neues Projekt starten |
| `deepwork-01-discovery` | Recherche und Plan |
| `deepwork-02-refine` | Plan in Arbeitsschritte aufteilen |
| `deepwork-03-execute` | Arbeitsschritte umsetzen |
| `deepwork-alt-autopilot` | Alles autonom durchführen |
| `deepwork-end-report` | Abschlussbericht |
| `deepwork-entry-analyze` | Bestehendes Projekt einsteigen |
| `deepwork-migrate` | Altes Projekt auf neue Struktur umziehen |

---

## Was NICHT auf dieser Baseline ist

Diese Entscheidungen sind bewusst:
- **Obsidian-App**: Muss manuell installiert werden — Claude Code kann keine Desktop-Apps installieren
- **API-Keys für externe Dienste**: Sensible Daten, nur der User kann diese einrichten
- **Firewall/Netzwerk-Konfigurationen**: Außerhalb von Claude Code's Reichweite

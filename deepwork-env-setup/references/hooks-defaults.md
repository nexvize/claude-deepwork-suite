# Hooks-Defaults — Empfohlene Einstellungen

Hooks sind automatische Verhaltensregeln für Claude Code. Sie werden in der Datei `~/.claude/settings.json` gespeichert und laufen im Hintergrund, ohne dass man jedes Mal daran denken muss.

Die Skill `deepwork-env-setup` schlägt diese Hooks vor und aktiviert sie nur nach ausdrücklicher Bestätigung.

---

## Was sind Hooks?

Einfach erklärt: Hooks sind wie Erinnerungs-Zettel für Claude Code. Du kannst sagen "Bevor Claude etwas ändert, soll er immer X tun" oder "Nachdem Claude etwas gebaut hat, soll er automatisch Y prüfen".

Beispiel: "Immer wenn eine Datei gespeichert wird, führe die Tests aus" — das ist ein Hook.

---

## Empfohlene Hooks für deepwork-Projekte

### Hook 1: Statuszeile (statusline)
**Was es tut:** Zeigt unten im Claude Code-Fenster was gerade passiert — welche Phase, welches Projekt, wie viel es bisher gekostet hat.

**Warum nützlich:** Du siehst auf einen Blick wo du bist, ohne in Dateien schauen zu müssen.

**Wann aktiv:** Immer.

**Konfiguration:**
```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": ".*",
      "hooks": [{"type": "command", "command": "echo 'Status: OK'"}]
    }]
  }
}
```

---

### Hook 2: Session-Restore (session-start)
**Was es tut:** Beim Start einer neuen Unterhaltung liest Claude automatisch was zuletzt gemacht wurde und bringt sich selbst auf den neuesten Stand — aus handoff.md und Memory.

**Warum nützlich:** Du musst nicht jedes Mal erklären wo du aufgehört hast.

**Wann aktiv:** Zu Beginn jeder neuen Session (wenn /deepwork aktiv ist).

**Konfiguration (via update-config Skill):**
Diesen Hook richtet `deepwork-env-setup` direkt ein nach Bestätigung. Er liest handoff.md falls vorhanden und gibt eine kurze Zusammenfassung aus.

---

### Hook 3: Pre-Commit-Tests (pre-commit)
**Was es tut:** Bevor Code gespeichert/committed wird, führt Claude die vorhandenen Tests aus. Schlägt ein Test fehl, wird gewarnt.

**Warum nützlich:** Fehler werden sofort gefunden, nicht erst Stunden später.

**Wann aktiv:** Nur wenn Tests im Projekt vorhanden sind (package.json mit test-Script, pytest.ini, etc.).

**Bedingung:** Wird nur aktiviert wenn im aktuellen Projekt tatsächlich Tests existieren. Ansonsten sinnlos.

---

### Hook 4: Telemetrie nach Edits (post-edit)
**Was es tut:** Nach jeder Dateiänderung wird eine kurze Notiz ins `.deepwork/journal/` geschrieben — was wurde geändert, warum.

**Warum nützlich:** Automatisches Protokoll was wann geändert wurde. Hilfreich wenn man nachvollziehen will was passiert ist.

**Wann aktiv:** Immer wenn deepwork aktiv ist (handoff.md vorhanden).

---

## Hooks die NICHT empfohlen werden

| Hook | Warum nicht |
|---|---|
| Auto-Push zu GitHub | Zu riskant — Versionierung sollte bewusst passieren |
| Auto-Deploy | Riskant für produktive Systeme, außer explizit gewünscht |
| Alle Befehle ohne Bestätigung ausführen | Sicherheitsrisiko |

---

## Wie Hooks eingerichtet werden

Die Skill `update-config` übernimmt die technische Konfiguration. Du musst nichts manuell in JSON-Dateien schreiben — `deepwork-env-setup` koordiniert das.

Wenn du Hooks manuell anpassen willst: `~/.claude/settings.json` (global) oder `.claude/settings.json` im Projektordner (nur für dieses Projekt).

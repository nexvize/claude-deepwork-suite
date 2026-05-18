---
name: deepwork-quick
description: "**When: CAN — Nutze einzelne deepwork-Protokolle ohne die vollständige Pipeline zu starten.** Code Review, Debug-Session, Spike, Refactor, Brainstorm — auf jedes beliebige Projekt, ohne handoff.md oder Pflichtkette. Trigger: 'code review machen', 'bug fixen', 'spike', 'refactoring', 'brainstorm', 'schnell helfen', '/deepwork-quick', oder wenn jemand eine konkrete Einzelaufgabe braucht ohne das ganze deepwork zu starten. Auch gut als Brücke zurück in den vollen deepwork-Modus."
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - AskUserQuestion
  - Skill
---

# deepwork-quick: Einzelne Protokolle — ohne Pipeline

**Für wenn du nicht das ganze deepwork brauchst, nur das Richtige für jetzt.**
Kein handoff.md nötig. Kein Discovery. Direkt zum Protokoll.

**Lies zuerst:**
- `DEEPWORK-CONFIG.md`
- `references/native-protocols.md` — alle Protokolle
- `references/user-profile.md`
- `references/tool-awareness.md`

---

## Schritt 0 — Was brauchst du? ⚐

Frage via `AskUserQuestion`. Nutze die 5-stufige Empfehlung wenn die Intensität unklar ist.

| Aufgabe | Protokoll | Typische Situation |
|---|---|---|
| Code Review | Code Review Protocol | "Schau mal drüber, ist das gut?" |
| Bug fixen | Debug Protocol (inkl. Self-Verification-first) | "Ich hab einen Bug der sich nicht lösen lässt" |
| Technische Frage klären | Spike Protocol | "Ich weiß nicht ob X mit Y überhaupt funktioniert" |
| Code aufräumen | Refactor Protocol | "Der Code ist unübersichtlich geworden" |
| Ideen entwickeln | Brainstorm Protocol | "Ich weiß nicht wie ich anfangen soll" |
| Docs/Research einlesen | Document Ingest Protocol | "Ich hab Dokumente die du kennen sollst" |
| Ergebnis prüfen | Verification Protocol | "Ich will wissen ob das wirklich funktioniert" |

**Complexity Check:** Falls die Aufgabe mehrere Protokolle braucht, oder das Resultat ein eigenständiges Projekt wird → klar kommunizieren:
```
Diese Aufgabe würde vom vollständigen deepwork-Workflow profitieren.
Soll ich:
  (a) Trotzdem nur den Quick-Mode machen (weniger gründlich)
  (b) Den Transfer-Einstieg starten: /deepwork-entry-analyze
  (c) Ein neues Projekt von Null anlegen: /deepwork-00-bootstrap
```

---

## Schritt 1 — Kontext einlesen ⚐

Je nach gewähltem Protokoll:

**Code Review / Debug / Refactor / Verification:**
- `Glob` → alle relevanten Dateien finden
- `Read` → wichtigste Dateien lesen
- Falls `.deepwork/` vorhanden: `handoff.md` und `decisions.md` für Kontext lesen

**Spike:**
- Nur die Frage formulieren — kein Codebase-Scan nötig
- MCP-Routing aus `references/tool-awareness.md` beachten

**Brainstorm:**
- Nur User-Input nötig — keine Dateien

**Document Ingest:**
- Alle bereitgestellten Docs lesen

**Kein `.deepwork/` vorhanden?**
Kurze Orientierung via `AskUserQuestion`:
- "Was ist das für ein Projekt?"
- "Was soll ich über den Kontext wissen bevor ich anfange?"

---

## Schritt 2 — Protokoll ausführen ⚐

Führe das gewählte Protokoll aus `references/native-protocols.md` vollständig aus. Nicht abkürzen.

**Intensität anpassen (5-stufige Skala, wenn relevant):**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TIEFE — wie gründlich soll ich sein?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Überblick: Offensichtlichstes, 5–10 Minuten
2. Basis: Wichtigste Punkte, 15–20 Minuten
⭐ 3. Standard (empfohlen): Vollständig, alle Aspekte
4. Tiefgehend: Mit Gegenprüfung, jede Annahme hinterfragen
5. Exhaustiv: Alles — maximale Kosten, maximale Abdeckung

Mein Tipp für diese Situation: Option <N> — <konkreter Grund>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Schritt 3 — Dokumentation ⚐

**Falls `.deepwork/` vorhanden:** Ergebnis ins Journal (`journal/<date>-quick-<protokoll>.md`).

**Falls nicht vorhanden:** Frage kurz wo das Ergebnis hin soll:
- Als Datei im aktuellen Ordner
- Nur im Chat (keine Datei)
- Deepwork-Struktur anlegen für spätere Nutzung

---

## Schritt 4 — Abschluss + Weiterführung ⚐

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
QUICK-SESSION FERTIG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Protokoll: <Name>
Ergebnis: <1–2 Sätze in Klartext was herausgekommen ist>

Falls du mehr willst:
  → Anderes Protokoll:            /deepwork-quick
  → Projekt vollständig einbinden: /deepwork-entry-analyze
  → Neues Projekt von Null:       /deepwork-00-bootstrap
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

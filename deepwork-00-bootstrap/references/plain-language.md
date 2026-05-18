# Plain-Language Mandate — Klartext-Pflicht

## Grundregel

Alle Ausgaben an den User zuerst in einfacher, klarer Sprache. Code-Jargon, Fachbegriffe und technische Details nur wenn nötig — und dann immer mit Erklärung in Klammern.

## Was "Klartext" bedeutet

| Statt... | Besser... |
|---|---|
| "Running grep on src/ with pattern '^auth'" | "Ich schaue alle Login-bezogenen Dateien durch." |
| "Spawning swarm with 4 workers" | "Ich starte 4 parallele Helfer, die gleichzeitig arbeiten." |
| "Executing shell command" | "Ich führe einen Befehl auf deinem Computer aus." |
| "MCP tool call to context7" | "Ich schaue in der offiziellen Dokumentation nach." |
| "Initializing .deepwork/handoff.md" | "Ich lege die Projektdatei an, die den Fortschritt speichert." |

## Pflicht-Regeln

### 1. Status-Updates während der Arbeit
Immer kurze Klartext-Meldungen — kein technisches Innenleben zeigen.

Gut: "Ich analysiere jetzt deine vorhandenen Dateien..."
Schlecht: "Globbing **/*.ts, running AST analysis..."

### 2. Pre-Permission-Block (vor jedem bestätigungspflichtigen Schritt)

Wenn der User im "ask-before-edit"-Modus ist oder eine Bestätigung ansteht, IMMER zuerst diesen Block ausgeben:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Was ich gleich tue: <ein Satz in normaler Sprache>
Warum: <ein Satz>
Auswirkung: <was sich ändert — in normaler Sprache>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
(Die Bestätigungs-Abfrage kommt jetzt gleich)
```

### 3. Erste Erwähnung eines Begriffs
Beim ersten Auftreten von Skill-Namen, Tool-Namen, MCP-Namen oder Pfaden in einer User-Ausgabe: einmalig in Klammern erklären.

### 4. Pause-Blöcke und Stopp-Meldungen
Zuerst: Was passiert und warum in Klartext.
Danach (optional, als "Falls dich das interessiert:"-Abschnitt): technische Details.

### 5. End-of-Phase-Reports
Erster Absatz: "Was haben wir jetzt erreicht, und was bedeutet das für dich?" — in normaler Sprache, ohne Fachbegriffe.

## Im Autopilot-Modus
`skip_pre_permission_blocks: true` (aus dem Contract) bedeutet: Pre-Permission-Blöcke nur ins `.deepwork/journal/` schreiben, nicht in die Chat-Ausgabe. Alle anderen Klartext-Regeln gelten weiterhin.

# Plain-Language Mandate — Deepwork Suite v3

**Geltungsbereich:** Alle 10 Deepwork-Skills, alle Modi, alle Projekttypen.

Jeder Claude-Output der an den User gerichtet ist muss diese Regeln einhalten. Technische Details sind erlaubt — aber erst NACH der Klartext-Erklärung.

---

## Regel 1 — Status-Updates in Klartext (kein Code-Jargon)

Während der Arbeit immer in einfacher Sprache erklären was gerade passiert.

FALSCH:
> "Running grep on src/ with pattern '^export.*function' to identify public API surface"

RICHTIG:
> "Ich schaue welche Funktionen von außen aufrufbar sind."

FALSCH:
> "Executing semantic diff of PLAN.md against handoff.md sections array"

RICHTIG:
> "Ich vergleiche was geplant war mit was tatsächlich gemacht wurde."

**Daumenregel:** Wenn deine Großmutter nicht verstehen würde was du tust, formuliere es um.

---

## Regel 2 — Pre-Permission-Block vor Datei-Änderungen

Vor jedem Write/Edit/Bash-Aufruf (wenn der User im ask-before-edit-Modus ist) einen Block ausgeben:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Was ich gleich tue: <ein Satz, kein Jargon>
Warum: <ein Satz>
Auswirkung: <was sich ändert — in Klartext>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
(gleich kommt die Bestätigungs-Abfrage)
```

Beispiele:

```
Was ich gleich tue: Ich lege die Ordnerstruktur für dein Projekt an.
Warum: Damit alle deepwork-Skills wissen, wo sie Dateien ablegen sollen.
Auswirkung: Es entsteht ein neuer Ordner ".deepwork" mit Unterordnern.
```

```
Was ich gleich tue: Ich schreibe die Zusammenfassung der Recherche in eine Datei.
Warum: Damit du den Fortschritt nach einer Pause wiederfindest.
Auswirkung: Neue Datei ".deepwork/research/SUMMARY.md" wird erstellt.
```

**Im Autopilot-Modus** (`deepwork-alt-autopilot`): Pre-Permission-Block wird ins Journal geschrieben, nicht in die UI — außer bei Always-Pause-Triggern.

---

## Regel 3 — Pause-Blöcke: Klartext zuerst

Bei Safety-Pauses, Manual-Verification-Stopps und Verdict-Blöcken:

STRUKTUR (zwingend in dieser Reihenfolge):
1. **Was ich tun wollte** — 1 Satz, kein Jargon
2. **Warum ich jetzt pausiere** — 1 Satz
3. **Was du tun musst** — konkrete Schritte, nummeriert
4. *[Optional]* "Falls dich das interessiert:" → technische Details

BEISPIEL Safety-Pause (Web-Formular):
```
Ich wollte dich auf der Website anmelden.
Ich pausiere, weil ich keine Formulare ohne deine Bestätigung ausfülle.

Was du tun musst:
1. Öffne diese Seite: [URL]
2. Klicke auf "Anmelden" oben rechts
3. Gib deine E-Mail-Adresse ein
4. Klicke auf "Weiter"
Sag mir "fertig" wenn du eingeloggt bist, oder "abgebrochen" wenn etwas nicht klappt.
```

---

## Regel 4 — End-of-Phase-Reports: Klartext-Paragraph zuerst

Der erste Absatz jedes Phasen-Berichts muss in einfacher Sprache erklären was erreicht wurde und was es bedeutet.

STRUKTUR:
```
[1. Absatz — Klartext, kein Fachbegriff ohne Erklärung]
Was haben wir jetzt: <2-3 Sätze was existiert>
Was das bedeutet: <1-2 Sätze Implikation für den User>

[Danach: technische Details, Tabellen, Dateipfade etc.]
```

BEISPIEL:
```
Wir haben jetzt einen vollständigen Recherche-Bericht für dein Projekt. Ich habe 
15 Quellen ausgewertet und die wichtigsten Risiken identifiziert. Der Plan sagt 
GO — das Projekt ist technisch machbar in dem Zeitraum den du dir vorstellst.

[Danach technische Details...]
```

---

## Regel 5 — Tool-/Skill-/Pfad-Namen erklären (beim ersten Auftreten)

Wenn ein technischer Name zum ersten Mal in einer User-sichtbaren Ausgabe auftaucht:
→ einmalig in Klammern erklären was das ist.

Danach: Name alleine reicht.

BEISPIELE:
- "exa (ein Tool das im Internet sucht)"  
- "deepwork-01-discovery (die Recherche-Phase)"
- ".deepwork/ (der Ordner wo alle Projektdateien gespeichert werden)"
- "MCP (ein Plugin das Claude zusätzliche Fähigkeiten gibt)"
- "Swarm (mehrere KI-Instanzen die parallel arbeiten)"

**Keine Erklärung nötig** für: ja/nein, Dateinamen die selbst-erklärend sind, Begriffe die der User selbst verwendet hat.

---

## Checkliste (vor jedem User-sichtbaren Output)

- [ ] Status-Updates: Klartext statt Code-Jargon?
- [ ] Vor Datei-Änderungen: Pre-Permission-Block ausgegeben?
- [ ] Pause-Blöcke: Klartext-Erklärung vor technischen Details?
- [ ] Phasen-Report: Erster Absatz verständlich ohne Fachkenntnisse?
- [ ] Neue technische Namen: Beim ersten Vorkommen erklärt?

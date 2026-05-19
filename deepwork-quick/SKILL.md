---
name: deepwork-quick
description: "**When: CAN — Nutze einzelne deepwork-Protokolle ohne die vollständige Pipeline zu starten.** Code Review, Debug-Session, Spike, Refactor, Brainstorm — auf jedes beliebige Projekt, ohne handoff.md oder Pflichtkette. Unterstützt alle 12 Projekttypen (coding, research, content, design, media, marketing, analysis, concept, education, automation, legal, finance) — Protokoll-Auswahl passt sich dynamisch an den Projekttyp an. Trigger: 'code review machen', 'bug fixen', 'spike', 'refactoring', 'brainstorm', 'schnell helfen', '/deepwork-quick', oder wenn jemand eine konkrete Einzelaufgabe braucht ohne das ganze deepwork zu starten. Auch gut als Brücke zurück in den vollen deepwork-Modus."
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
- `references/plain-language.md` — Klartext-Pflicht (Status-Updates, Pre-Permission-Blocks, Pause-Blöcke)
- `DEEPWORK-CONFIG.md`
- `references/native-protocols.md` — alle Protokolle
- `references/user-profile.md`
- `references/tool-awareness.md`
- `references/project-profiles.md` — Projekttyp-Profile (für dynamische Protokoll-Auswahl)

## Projekttyp-Präambel ⚐

Am Start jeder Session:

1. `PROJECT.md` lesen (`.deepwork/planning/PROJECT.md`)
2. `project_type` auslesen (coding | research | content | design | media | marketing | analysis | concept | education | automation | legal | finance)
3. Falls nicht vorhanden: kurz fragen welcher Typ
4. `references/project-profiles.md` — Profil für diesen Typ laden
5. Profil-Einstellungen übernehmen: bevorzugte Protokolle, MCPs, Verification-Kriterien, Swarm-Sizing

---

## Schritt 0 — Projekttyp erkennen + Protokoll wählen ⚐

**Projekttyp laden:**
- `.deepwork/planning/PROJECT.md` lesen falls vorhanden → `project_type` auslesen
- Falls nicht: kurz fragen (1 Klick-Auswahl aus 12 Typen)
- Profil aus `references/project-profiles.md` laden

**Protokoll-Tabelle (dynamisch nach Typ):**

Zeige dem User NUR die Protokolle die für seinen Projekttyp relevant sind:

| Typ | Primäre Protokoll-Optionen |
|---|---|
| coding | Code Review, Debug (Self-Verification-first), Refactor, Spike, TDD, Verification |
| research | Document Ingest, Spike, Verification, Brainstorm |
| content | Brainstorm, Outline, Draft, Edit, Proofread, SEO-Optimize |
| design | WireframeReview, DesignAudit, UX-Heuristics, FigmaSpec, ComponentInventory |
| media | PromptEngineering, Storyboard, AssetInventory, VideoScript |
| marketing | Brainstorm, CampaignPlan, CopyReview, Verification, SEO-Optimize |
| analysis | DataIngest, InsightExtraction, Hypothesis-Test, ReportDraft |
| concept | Brainstorm, StructuredPlanning, Spike, PitchDeck, RoadmapBuild |
| education | LearningOutcomes, CurriculumOutline, ExerciseDesign, AssessmentDesign |
| automation | Spike, CodeReview, IntegrationTest, Verification |
| legal | Document Ingest, Verification, Draft, Spike |
| finance | DataIngest, Hypothesis-Test, Verification, ReportDraft |

**Alle anderen Protokolle auch verfügbar** — aber zeige zuerst die typ-relevanten.

**Neu: Auto-Discovery als Protokoll-Option:**
Immer als Option anbieten: "Auto-Discovery — Findet fehlende Skills/MCPs/Plugins für diesen Projekttyp"

**Protokoll-Quellen:** Protokolle für coding/research/brainstorm/debug: `references/native-protocols.md`. Protokolle für content: `references/content-protocols.md`. Für design: `references/design-protocols.md`. Für media: `references/media-protocols.md`. Für analysis: `references/analysis-protocols.md`. Für concept/education: `references/concept-protocols.md` + `references/education-protocols.md`.

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

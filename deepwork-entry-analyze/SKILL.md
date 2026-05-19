---
name: deepwork-entry-analyze
description: "**When: MUST — Alternative entry point to deepwork-00-bootstrap for projects that already exist and were NOT set up with deepwork.** Bestandsaufnahme und Analyse eines bestehenden Projekts, das NICHT mit deepwork aufgesetzt wurde. Führt eine strukturierte Analyse durch: Codebase-Scan, Architektur-Mapping, Qualitäts-Check, offene Fragen identifizieren — und baut dann die deepwork-Struktur (handoff.md, .deepwork/) rückwirkend auf, damit alle anderen deepwork-Skills funktionieren. Erkennt automatisch den Projekttyp (coding, research, content, design, media, marketing, analysis, concept, education, automation, legal, finance) und legt typ-spezifische Ordnerstrukturen an. Trigger: 'analysiere dieses projekt', 'bestandsaufnahme', 'wie ist der stand', 'ich habe ein bestehendes projekt', 'deepwork für bestehendes projekt', '/deepwork-entry-analyze'. Auch triggern: wenn jemand fragen stellt die sich auf ein laufendes Projekt beziehen, ohne deepwork-Struktur sichtbar zu sein."
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
  - Grep
  - Bash
  - Task
  - AskUserQuestion
  - Skill
---

# deepwork-entry-analyze: Bestandsaufnahme

**Für bestehende Projekte die nicht mit deepwork erstellt wurden.** Dieser Skill führt eine vollständige Analyse durch und baut die deepwork-Infrastruktur rückwirkend auf — damit danach alle anderen deepwork-Skills nahtlos funktionieren.

**Read first:**
- `DEEPWORK-CONFIG.md` — Vault-Pfad, Swarm-Limit, Cost-Cap (zuerst lesen!)
- `references/native-protocols.md` — Quality Gate Checklist
- `references/handoff-protocol.md`
- `references/model-selection.md`
- `references/tool-awareness.md`
- `references/self-reflection.md` — controlling during analysis
- `references/user-profile.md` — non-technical user assumption
- `references/project-profiles.md` — Projekttyp-Profile (für Typ-Erkennung und typ-spezifische Ordnerstrukturen)

## Projekttyp-Präambel ⚐

Am Start jeder Session:

1. `PROJECT.md` lesen (`.deepwork/planning/PROJECT.md`)
2. `project_type` auslesen (coding | research | content | design | media | marketing | analysis | concept | education | automation | legal | finance)
3. Falls nicht vorhanden: kurz fragen welcher Typ
4. `references/project-profiles.md` — Profil für diesen Typ laden
5. Profil-Einstellungen übernehmen: bevorzugte Protokolle, MCPs, Verification-Kriterien, Swarm-Sizing

Hinweis: Dieser Skill muss den Projekttyp ggf. SELBST ERKENNEN falls nicht gesetzt — siehe Step 0b.

---

## Step 0 — Struktur-Erkennung: Welcher Modus? ⚐

**Erster Check — bevor irgendetwas analysiert wird:**

| Situation | Erkennungszeichen | Modus |
|---|---|---|
| Aktives deepwork-Projekt | `handoff.md` vorhanden + `.deepwork/` vollständig | Kein Einstieg hier — verweise auf `/deepwork-00-bootstrap` |
| Altes / unvollständiges deepwork | `.deepwork/` vorhanden, aber Ordner fehlen oder `handoff.md` veraltet | **Migrate-Modus** (erst Struktur ergänzen, dann leichte Analyse) |
| Kein deepwork vorhanden | Kein `.deepwork/`, kein `handoff.md` | **Vollanalyse-Modus** (3-Agent Scan + Interview + aufbauen) |

**Wenn aktives deepwork-Projekt erkannt:**
```
Dieses Projekt hat bereits eine aktive deepwork-Struktur (handoff.md gefunden).
Einstieg hier nicht nötig.

Nächste Schritte:
  → /deepwork-00-bootstrap — prüft den aktuellen Stand und führt weiter
  → /deepwork-03-execute — wenn du direkt eine Section ausführen willst
```
→ Stop.

**Wenn Migrate-Modus (alte/unvollständige Struktur):**

Zeige in Klartext was fehlt und was ergänzt wird:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MIGRATIONSPLAN — Was ich ergänzen würde:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Neue Ordner: <liste>
Neue Dateien (leer): <liste>
Bestehende Dateien: bleiben UNVERÄNDERT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Soll ich das durchführen? (ja / nein / was ist das genau?)
```
Nach Bestätigung: additiv ergänzen, nichts löschen → danach leichte Analyse (nur Gap-Check, kein voller 3-Agent Codebase-Scan). Weiter mit Step 1 (Interview) statt vollständigem Scan.

**Typ-spezifische Ordner prüfen (Migrate-Modus):** Nach dem Struktur-Fix prüfen ob die für den Projekttyp empfohlenen Ordner vorhanden sind:
- `coding` → `src/`, `tests/`, `docs/`
- `design` → `wireframes/`, `mockups/`, `assets/`, `design-system/`
- `content` → `drafts/`, `published/`, `assets/`
- `research` → `sources/`, `notes/`, `literature/`
- `media` → `assets/`, `scripts/`, `exports/`
- `analysis` → `data/`, `notebooks/`, `outputs/`
- (Vollständige Liste in `references/project-profiles.md`)
Falls Ordner fehlen: in Migrationsplan aufnehmen und mit anlegen.

**Wenn Vollanalyse-Modus:** Weiter mit Step 0b.

---

## Step 0b — Projekt-Scan (Vollanalyse-Modus) ⚐

**Projekttyp-Erkennung:** Falls `project_type` in PROJECT.md fehlt oder PROJECT.md noch nicht existiert:
- Code-Dateien dominant (`.js`, `.ts`, `.py`, `.go`, `.rs`, etc.) → `coding`
- Text-/Markdown-Dateien dominant, kein Code → `content`
- Design-Assets (`.fig`, `wireframes/`, `mockups/`, design tokens) → `design`
- Jupyter Notebooks, Daten-CSVs, Analyse-Skripte → `analysis`
- Medien-Assets dominant (`.mp4`, `.mp3`, `assets/`, `media/`) → `media`
- Recherche-Dokumente, Quellen-Ordner, Literatur → `research`
- Falls unklar: kurz fragen (1 Klick aus 12 Typen)
→ Erkannten Typ in PROJECT.md als `project_type` nachtragen.

**Tool inventory:** Welche Skills, MCPs, Plugins sind verfügbar? Schreibe `.deepwork/tool-inventory.md` (Format aus deepwork-00).

**Codebase-Scan (parallel, 3 Agents):**

**Agent A — Struktur:**
- Verzeichnisstruktur, Haupt-Einstiegspunkte
- Package.json / requirements.txt / Cargo.toml / etc.
- Build-System, Scripts, CI/CD
- Output: `.deepwork/analysis/structure.md`

**Agent B — Architektur:**
- Welche Muster werden verwendet? (MVC, event-driven, microservices, monolith...)
- Welche Frameworks / Libraries?
- Welche Datenmodelle / Datenbanken?
- Wie kommunizieren die Teile miteinander?
- Output: `.deepwork/analysis/architecture.md`

**Agent C — Qualität:**
- Gibt es Tests? Welche Art? Wie viele?
- Gibt es Dokumentation?
- Gibt es bekannte Bugs / TODO-Kommentare / FIXME?
- Wie alt ist der Code? Git-History-Scan.
- Output: `.deepwork/analysis/quality.md`

---

## Step 1 — Kontext-Interview ⚐

Nach dem Scan: gezielte Fragen via `AskUserQuestion` — nur was der Scan nicht beantworten konnte:

**User Profile ⚐** (see `references/user-profile.md`): Assume the user is non-technical. They may not know technical terms for what they built or are using. Adapt all questions to plain language. Watch for knowledge gaps that explain architectural decisions in the codebase.

**Round A — Was und Warum:**
1. Wofür ist dieses Projekt? Was ist das Hauptproblem, das es löst?
2. Wer nutzt es? (intern / extern / geplant aber noch nicht live)
3. Was ist der aktuelle Stand — in Produktion, in Entwicklung, eingefroren?

**Round B — Geschichte:**
4. Wann wurde es gestartet? Warum?
5. Was hat nicht funktioniert oder wurde geändert? Größte Probleme bisher?
6. Was fehlt noch? Was wäre der nächste Schritt gewesen?

**Round C — Zukunft:**
7. Warum jetzt die Bestandsaufnahme? Was soll danach passieren?
8. Gibt es Constraints die ich kennen muss? (kein Breaking Change, muss kompatibel bleiben mit X, etc.)

---

## Step 2 — Deepwork-Struktur aufbauen ⚐

Erstelle alle fehlenden deepwork-Dateien rückwirkend:

**`.deepwork/`** Verzeichnis erstellen (falls nicht vorhanden) mit:
- `journal/` — leer, für zukünftige Einträge
- `outputs/` — leer
- `research/` — leer
- `decisions.md` — vorausgefüllt mit dem was aus dem Interview bekannt ist
- `cost-log.md` — leer (bisherige Kosten unbekannt, da kein deepwork genutzt)

**`./handoff.md`** — Schreibe es vollständig aus (Format: `references/handoff-protocol.md`):
- Fülle alle bekannten Felder aus dem Scan + Interview
- `current_phase: analyze` (neu)
- `verdict: pending` (noch nicht bewertet)
- Sections: leite aus dem Interview ab was als nächstes getan werden soll
- Assumptions: alle aus dem Scan abgeleiteten Annahmen, als `unverified` markieren
- Risks: offensichtliche Risiken aus Code-Qualität-Scan

---

## Step 3 — Gap-Analyse ⚐

Bewerte strukturiert was fehlt oder problematisch ist:

Schreibe `.deepwork/analysis/GAP-ANALYSIS.md`:

```markdown
# Gap-Analyse: <Projektname>
Datum: <ISO-8601>

## Codebase-Zustand
| Bereich | Status | Details |
|---------|--------|---------|
| Tests | Vorhanden / Unvollständig / Fehlen | <coverage, typen> |
| Dokumentation | Vorhanden / Veraltet / Fehlt | <was fehlt> |
| Fehlerbehandlung | Robust / Lückenhaft | <spezifische Probleme> |
| Sicherheit | Geprüft / Ungeprüft | <auffälligkeiten> |
| Performance | Optimiert / Ungeprüft | <bottlenecks sichtbar?> |

## Was Gut Funktioniert
- <Stärke 1>
- <Stärke 2>

## Was Problematisch Ist
| Problem | Schwere | Empfehlung |
|---------|---------|------------|
| <problem> | Kritisch / Mittel / Niedrig | <was zu tun ist> |

## Was Komplett Fehlt
- <fehlendes Feature / Komponente>: <warum es wichtig ist>

## Technische Schulden
- <schuld>: <einschätzung des aufwands um sie zu beheben>

## Externe Abhängigkeiten & Risiken
- <dependency>: <aktuell? gepflegt? Sicherheitslücken?>

## Empfohlene nächste Schritte (priorisiert)
1. <kritischstes Problem zuerst>
2. <zweites>
3. <drittes>
```

**Self-reflection check ⚐:** Before finalizing the gap analysis, check:
- Am I assessing this codebase against the right standard? (startup vs. enterprise has different norms)
- Are any of my "gaps" actually intentional design decisions that make sense in this context?
- Am I recommending things the user can actually implement given their non-technical background?

**Non-technical translation ⚐:** The gap analysis must be written in plain language. Every technical finding needs a plain-language explanation of: what it means, why it matters, and what the user can realistically do about it.

---

## Step 3.5 — Kreuzverhoer: Gap-Analyse Stress-Test ⚐

**Invoke kreuzverhoer:** Run `Skill` tool → `kreuzverhoer` auf `GAP-ANALYSIS.md`. Für jeden Befund hinterfragen:
- Ist das wirklich eine Lücke — oder eine bewusste Designentscheidung die im Kontext Sinn ergibt?
- Ist die Schwereeinschätzung (Kritisch / Mittel / Niedrig) korrekt, oder wurde sie unter- bzw. überschätzt?
- Ist die Empfehlung realistisch für einen nicht-technischen User mit diesem Projekt?
- Passt die Priorisierung der nächsten Schritte zu dem was der User wirklich erreichen will?

Output → Anpassungen in `GAP-ANALYSIS.md` einarbeiten, Begründungen in `.deepwork/decisions.md` dokumentieren.

---

## Step 4 — Realism Check ⚐

Führe eine vereinfachte Verdict-Bewertung durch (aus deepwork-01):

- Ist das Projekt technisch feasible in seinem aktuellen Zustand fortzuführen?
- Sind die Schulden und Risiken manageable?
- Macht der Plan (was als nächstes passieren soll) Sinn angesichts dessen was existiert?

Schreibe `.deepwork/VERDICT.md` (Format aus verdict-rubric.md):
- Statt 6-dim-scoring: fokussierte Bewertung der 3 kritischsten Dimensionen
- Verdict: `GO` (weiter so), `GO-WITH-CLEANUP` (erst Schulden abbauen), `RESTRUCTURE` (fundamentale Neuausrichtung nötig), `ABANDON` (weiterzumachen macht keinen Sinn)

Präsentiere via `AskUserQuestion`:
- Gap-Analyse Zusammenfassung
- Verdict + Begründung
- Empfohlene nächste Skills: `/deepwork-01`, `/deepwork-03`, `/deepwork-end-report`

---

## Step 5 — Quality Gate + Obsidian Sync ⚐

**Quality Gate:** Prüfe ob alle Kernanalyse-Dokumente vorhanden und vollständig sind:
- [ ] `.deepwork/analysis/architecture.md`
- [ ] `.deepwork/analysis/GAP-ANALYSIS.md`
- [ ] `handoff.md` mit status = `entry-analyze`

**Obsidian sync** (wenn vault konfiguriert): Sync gap-analysis, architecture nach `<DEEPWORK_VAULT_PATH>\Projects\<slug>\Deepwork\`.

---

## Step 6 — Handoff + Output ⚐

Update `handoff.md` mit den finalen Findings aus der Analyse.

Schreibe `.deepwork/cost-log.md` Eintrag für diese Analyse-Session.

```
═══════════════════════════════════════════
BESTANDSAUFNAHME ABGESCHLOSSEN
═══════════════════════════════════════════
Projekt: <name>
Codebase-Scan: ✓
Gap-Analyse (Lücken-Bericht): .deepwork/analysis/GAP-ANALYSIS.md ✓
handoff.md (Projekt-Statusdokument): aufgebaut ✓
Bewertung: <GO | GO-WITH-CLEANUP | RESTRUCTURE | ABANDON>

Empfohlene nächste Schritte:
  Bewertung GO:               /deepwork-03-execute (neue Aufgabe hinzufügen)
  Bewertung GO-WITH-CLEANUP:  /deepwork-01-discovery (Umfang der Bereinigung klären)
  Bewertung RESTRUCTURE:      /deepwork-01-discovery (Neuausrichtung planen)
  Bewertung ABANDON:          /deepwork-end-report (Abschluss-Dokumentation)
═══════════════════════════════════════════
```

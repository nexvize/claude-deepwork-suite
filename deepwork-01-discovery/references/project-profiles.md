# Project Profiles — Deepwork Suite v3

## Wie Skills dieses Dokument nutzen

Jeder Deepwork-Skill liest beim Start den `project_type`-Wert aus `PROJECT.md` und lädt das passende Profil aus diesem Dokument. Das Profil definiert, welche Protokolle in welcher Priorität eingesetzt werden, welche MCPs bevorzugt geroutet werden, wie groß Swarms dimensioniert werden, wie die Ordnerstruktur aussieht und was "fertig" für diesen Projekttyp bedeutet — sodass alle Skills konsistent und ohne manuelle Konfiguration auf den jeweiligen Kontext zugeschnitten agieren.

## Lesen: Projekttyp aus PROJECT.md

```yaml
# .deepwork/PROJECT.md — minimales Pflichtfeld
project_type: coding            # Primärer Typ (Pflicht)
project_type_secondary: marketing  # Optionaler Sekundärtyp
```

Skills lesen das Feld wie folgt (Pseudocode):

```python
project = load_yaml(".deepwork/PROJECT.md")
profile  = load_profile(project["project_type"])        # Primär-Profil
if "project_type_secondary" in project:
    secondary = load_profile(project["project_type_secondary"])
    profile.protocols += secondary.protocols[:3]        # Top-3 als Optional
```

---

## Profil: coding

**Beschreibung:** Softwareentwicklungsprojekte jeder Größe — von einzelnen Skripten bis zu vollständigen Systemen. Umfasst Debugging, Refactoring, Feature-Entwicklung, Code-Reviews und testgetriebene Entwicklung.

**Beispiele:** API-Backend in FastAPI, React-Frontend-Komponenten, CLI-Tool in Rust, Datenpipeline in Python, Microservice-Migration, Open-Source-Library-Beitrag

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Debug | Fehler lokalisieren, Stack Traces analysieren, Reproduktionsschritte definieren |
| Primär | CodeReview | Code-Qualität prüfen, Sicherheitslücken finden, Architektur bewerten |
| Primär | TDD | Neue Features über Tests spezifizieren, Red-Green-Refactor-Zyklus |
| Sekundär | Refactor | Bestehenden Code verbessern ohne Verhalten zu ändern |
| Sekundär | Spike | Technische Unsicherheiten explorativ klären (PoC-Zeitbox) |
| Optional | DocIngest | Fremde Codebasen oder Bibliotheken verstehen |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **context7** — Offizielle Bibliotheks-Dokumentation direkt abrufen, API-Referenzen, Framework-Guides; verhindert halluzinierte APIs
2. **filesystem** — Lokale Codebase traversieren, Dateien lesen/schreiben, Ordnerstruktur analysieren
3. **github** — PRs öffnen, Issues tracken, Commit-History analysieren, Branches verwalten
4. **playwright** — E2E-Tests ausführen, UI-Verhalten überprüfen, Regressions-Screenshots
5. **sequential-thinking** — Komplexe Debugging-Ketten strukturiert durchdenken

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Single-File-Fix | 1–2 | Kontext bleibt überschaubar, sequentielle Änderung sicherer |
| Standard-Feature | 3–6 | Parallele Analyse von Tests, Implementierung und Docs möglich |
| Modul-Refactor | 5–8 | Jeder Worker übernimmt eine Komponente oder Schicht |
| Große Codebase-Analyse | 8–20 | Parallelisierung nach Verzeichnis/Modul, dann Synthese |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
src/
tests/
docs/
scripts/
```

### Verifikations-Kriterien

"Fertig" für diesen Typ bedeutet:
- [ ] Alle Tests grün (Unit, Integration, ggf. E2E)
- [ ] Code läuft ohne Fehler in der Zielumgebung
- [ ] Kein neuer Linting-/Typ-Fehler eingeführt
- [ ] Code Review abgeschlossen (mind. eine Durchsicht)
- [ ] Relevante Dokumentation aktualisiert (README, Docstrings, Changelog)
- [ ] Kein offener TODO/FIXME ohne Ticket

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/coding/`
- Datei-Format: `.py`, `.ts`, `.md` für Dokumentation, `.json` für Konfigurationen

---

## Profil: research

**Beschreibung:** Wissensrecherche-Projekte, die externe Quellen systematisch sammeln, bewerten und synthetisieren. Ziel ist ein verlässliches Wissensfundament — nicht Spekulation, sondern belegbare Aussagen.

**Beispiele:** Markt- und Wettbewerbsanalyse, State-of-the-Art-Review für ein KI-Modell, technische Machbarkeitsstudie, akademische Literaturrecherche, Branchentrend-Bericht, Due-Diligence-Recherche

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DocIngest | Quellen einlesen, indexieren, initial kategorisieren |
| Primär | Verification | Fakten gegen mehrere Quellen prüfen, Widersprüche markieren |
| Primär | Brainstorm | Forschungsfragen generieren, Blinde Flecken identifizieren |
| Sekundär | Spike | Schnelle Erstorientierung in unbekanntem Feld (Zeitbox 25 min) |
| Sekundär | InsightExtraction | Kernaussagen aus gescannten Quellen destillieren |
| Optional | ReportDraft | Ergebnisse zu lesbarem Bericht verdichten |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **exa** — Semantische Websuche für Fachinhalte, aktuelle Quellen, wissenschaftliche Artikel; beste Qualität für Research-Intent
2. **firecrawl** — Vollständigen Seiteninhalt scrapen, Quelltext extrahieren, strukturierte Daten aus Websites ziehen
3. **context7** — Bibliotheken und Frameworks in technischen Research-Projekten dokumentieren
4. **memory** — Gefundene Fakten und Quellen sitzungsübergreifend speichern, Knowledge-Graph aufbauen
5. **sequential-thinking** — Hypothesen schrittweise ausarbeiten, Kausalitätsketten prüfen

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelquelle analysieren | 1–2 | Fokus auf Tiefe, kein Parallelisierungsvorteil |
| Standard-Recherche | 5–10 | Jeder Worker durchsucht eine Quellengruppe parallel |
| Große Literaturrecherche | 10–20 | Parallelisierung nach Themencluster, dann Synthesizer-Worker |

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
sources/
sources/raw/
sources/annotated/
synthesis/
reports/
```

### Verifikations-Kriterien

- [ ] Alle Kernaussagen durch mindestens zwei unabhängige Quellen belegt
- [ ] Widersprüche zwischen Quellen explizit dokumentiert und bewertet
- [ ] Synthesis-Dokument vollständig und lesbar
- [ ] Quellenverzeichnis mit vollständigen Metadaten (URL, Datum, Autor)
- [ ] Offene Fragen und Forschungslücken benannt
- [ ] Kein Halluziniertes Zitat ohne Verifikation

---

## Profil: content

**Beschreibung:** Textproduktions-Projekte mit Fokus auf Qualität, Ton-Konsistenz und faktischer Korrektheit.

**Beispiele:** Blog-Artikel-Serie, Newsletter-Ausgaben, Whitepaper für SaaS-Produkt, Produktbeschreibungen, Social-Media-Content-Plan, Buchkapitel, Landing-Page-Texte

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Brainstorm | Themen, Winkel und Formate generieren |
| Primär | Outline | Strukturentwurf und Argumentationsfluss klären |
| Primär | Draft | Erstentwurf schreiben, Placeholder für fehlende Facts setzen |
| Sekundär | Edit | Ton, Klarheit, Lesbarkeit verbessern; Struktur optimieren |
| Sekundär | Proofread | Grammatik, Rechtschreibung, Fakten-Endcheck |
| Optional | Verification | Faktencheck für spezifische Claims |

### MCP-Routing

1. **firecrawl** — Konkurrenz-Content scrapen, Inspiration von Top-Quellen ziehen, Fakten extrahieren
2. **exa** — Aktuelle Quellen für Fakten-Backing finden, Trending Topics recherchieren
3. **memory** — Stil-Guide und Tonalitätsvorgaben sitzungsübergreifend speichern
4. **Gamma MCP** — Präsentationen und Slidedeck-Versionen von Content generieren

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelner Artikel | 1–2 | Schreiben ist sequential; zu viele Worker fragmentieren den Ton |
| Content-Batch (5–10 Stücke) | 3–4 | Ein Worker pro Stück, ein Synthesizer für Ton-Konsistenz |
| Großes Content-Projekt | 4–6 | Struktur-, Schreib- und Faktencheck-Worker trennen |

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
drafts/
drafts/v1/
drafts/final/
published/
assets/
assets/images/
```

### Verifikations-Kriterien

- [ ] Text liest sich flüssig und hat einen konsistenten Ton
- [ ] Alle Fakten und Zahlen sind verifiziert und mit Quellen belegt
- [ ] Headline und Opener sind stark und klar
- [ ] Zielgruppensprache passt
- [ ] SEO-Grundregeln erfüllt (wenn relevant)
- [ ] Korrekturgelesen — keine Tippfehler, Grammatikfehler

---

## Profil: design

**Beschreibung:** UI/UX-Design-Projekte von der Wireframe-Phase bis zum Dev-Handoff.

**Beispiele:** Onboarding-Flow für Mobile App, Design-System-Aufbau, Landingpage-Redesign, Dashboard-UX-Audit

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | WireframeReview | Frühe Strukturkonzepte bewerten, Informationsarchitektur prüfen |
| Primär | DesignAudit | Bestehende Designs gegen Heuristiken und Markenstandards prüfen |
| Primär | UX-Heuristics | Nielsen-Heuristiken systematisch durcharbeiten |
| Sekundär | FigmaSpec | Design-Spezifikation für Entwickler erstellen |
| Sekundär | Brainstorm | Konzeptalternativen und Lösungsansätze generieren |
| Optional | Verification | Accessibility-Check, WCAG-Compliance |

### MCP-Routing

1. **Figma MCP** — Figma-Files lesen, Screenshots ziehen, Code-Connect-Mappings, Design-Tokens extrahieren
2. **playwright** — Live-UI im Browser screenshotten, Interaktionen testen
3. **exa** — Design-Inspiration, Branchen-Benchmarks, UX-Pattern-Recherche
4. **filesystem** — Assets exportieren, Spezifikations-Dokumente schreiben

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelner Screen | 1–2 | Fokussierter Review ohne parallelen Overhead |
| Flow-Review (5–10 Screens) | 3–5 | Ein Worker pro Screen-Gruppe, ein Synthesizer |
| Design-System-Audit | 5–10 | Parallelisierung nach Komponentenkategorie |
| Vollständiges Produkt-Audit | 8–15 | Parallele Heuristik-Worker, dann Konsolidierung |

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
wireframes/
specs/
specs/components/
assets/
assets/icons/
assets/images/
components/
```

### Verifikations-Kriterien

- [ ] Figma-Datei vollständig mit allen States
- [ ] Design-Spezifikation geschrieben
- [ ] Dev-Handoff-Kommentar in Figma vorhanden
- [ ] Accessibility-Mindestanforderungen erfüllt
- [ ] Responsive-Verhalten für alle Breakpoints definiert
- [ ] Asset-Export bereit

---

## Profil: media

**Beschreibung:** KI-gestützte Medienproduktion — Bild- und Videogeneration, Prompt-Engineering, Asset-Pipelines.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | PromptEngineering | Optimale Generierungsprompts entwickeln, iterativ verfeinern |
| Primär | Storyboard | Sequenzen planen, Shot-Liste erstellen, Timing definieren |
| Primär | AssetPipeline | Batch-Generierung orchestrieren, Assets organisieren und exportieren |
| Sekundär | Brainstorm | Konzepte, Stilrichtungen und Variationsideen generieren |
| Optional | Verification | Qualitätskontrolle, Brand-Konsistenz, Lizenz-Checks |

### MCP-Routing

1. **higgsfield** — Bild- und Videogeneration, Modell-Selektion, Workspace-Management
2. **filesystem** — Asset-Ordnerstruktur verwalten
3. **Figma MCP** — Moodboards erstellen, Storyboard-Frames in Figma layouten
4. **exa** — Stil-Referenzen recherchieren

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelasset | 1–2 | Iterative Prompt-Verfeinerung |
| Prompt-Variationstest | 5–10 | Parallele Generierung verschiedener Stile |
| Großes Asset-Batch | 10–20 | Jeder Worker generiert eine Kategorie parallel |

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
prompts/
prompts/templates/
prompts/iterations/
assets/
assets/generated/
assets/approved/
exports/
storyboards/
```

### Verifikations-Kriterien

- [ ] Assets in gewünschter Auflösung und Format generiert
- [ ] Qualitätskontrolle durchgeführt
- [ ] Finale Prompts dokumentiert (für Reproduzierbarkeit)
- [ ] Assets sinnvoll benannt und in finale Ordnerstruktur überführt
- [ ] Lizenz und Nutzungsrechte klar
- [ ] Storyboard mit Assets abgeglichen

---

## Profil: marketing

**Beschreibung:** Marketing- und Wachstumsprojekte — Strategie, Copywriting, Kampagnenplanung.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Brainstorm | Kampagnenkonzepte, Hooks, Zielgruppenanalyse |
| Primär | CampaignPlan | Kampagnenstruktur, Timeline, Kanalauswahl |
| Primär | CopyReview | Texte gegen Best Practices prüfen |
| Sekundär | Verification | Faktencheck für Claims |
| Sekundär | Outline | Content-Kalender strukturieren |
| Optional | DesignAudit | Visuelle Konsistenz der Kampagnen-Assets prüfen |

### MCP-Routing

1. **exa** — Wettbewerber-Analyse, Branchentrends, Keyword-Recherche
2. **firecrawl** — Landingpages und Kampagnenseiten von Wettbewerbern extrahieren
3. **Figma MCP** — Brand-Assets abrufen, Kampagnen-Visuals reviewen
4. **memory** — Brand-Voice und Kampagnen-History speichern

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
copy/
copy/drafts/
copy/approved/
campaigns/
assets/
assets/visuals/
briefs/
```

### Verifikations-Kriterien

- [ ] Kampagnenziel und KPIs klar definiert
- [ ] Copy reviewed und freigegeben
- [ ] Alle Assets produziert und organisiert
- [ ] Zeitplan und Verantwortlichkeiten festgelegt
- [ ] Legal-Check für Claims durchgeführt
- [ ] Tracking und Erfolgsmetriken eingerichtet

---

## Profil: analysis

**Beschreibung:** Datengetriebene Analyseprojekte — von Rohdaten-Ingestion über Hypothesen-Tests bis zum Insight-Report.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DataIngest | Rohdaten laden, Qualität prüfen, Struktur verstehen |
| Primär | InsightExtraction | Muster, Anomalien und Kernergebnisse aus Daten destillieren |
| Primär | Hypothesis-Test | Annahmen gegen Daten prüfen, Konfidenz bewerten |
| Sekundär | ReportDraft | Erkenntnisse in lesbaren Bericht überführen |
| Sekundär | Verification | Ergebnisse cross-validieren |
| Optional | Brainstorm | Hypothesen und Analysefragen generieren |

### MCP-Routing

1. **exa** — Benchmarks und Vergleichsdaten recherchieren
2. **firecrawl** — Externe Datensätze und Reports scrapen
3. **context7** — Analyse-Bibliotheken (pandas, numpy, R) dokumentieren
4. **filesystem** — Datendateien lesen, Analyse-Notebooks schreiben
5. **sequential-thinking** — Kausalitätsketten strukturiert aufbauen

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
data/
data/raw/
data/processed/
reports/
insights/
models/
notebooks/
```

### Verifikations-Kriterien

- [ ] Alle Datenquellen zitiert und Qualität dokumentiert
- [ ] Kernaussagen statistisch abgesichert
- [ ] Methodik transparent und reproduzierbar beschrieben
- [ ] Annahmen explizit gemacht und kritisch bewertet
- [ ] Handlungsempfehlungen klar und priorisiert
- [ ] Bericht auch für Nicht-Datenmenschen lesbar

---

## Profil: concept

**Beschreibung:** Konzeptionelle Planungsprojekte — Ideen strukturieren, Annahmen testen, kohärente Vision für Stakeholder erstellen.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Brainstorm | Ideen generieren, Möglichkeitsraum öffnen |
| Primär | StructuredPlanning | Beste Ideen in kohärenten Plan überführen |
| Primär | Spike | Kritische Annahmen in Zeitbox explorativ testen |
| Sekundär | Verification | Kernbehauptungen gegen Quellen prüfen |
| Sekundär | ReportDraft | Konzept in präsentierbares Dokument überführen |
| Optional | StakeholderMap | Interessengruppen identifizieren |

### MCP-Routing

1. **exa** — Marktrecherche, Wettbewerber, Branchenstudien
2. **sequential-thinking** — Konzepte Schritt für Schritt durchdenken
3. **memory** — Konzeptversionen und Stakeholder-Feedback speichern
4. **Gamma MCP** — Pitchdeck und Präsentation aus Konzept generieren
5. **firecrawl** — Referenzkonzepte und Fallstudien extrahieren

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
ideas/
ideas/brainstorms/
roadmaps/
pitches/
stakeholders/
assumptions/
```

### Verifikations-Kriterien

- [ ] Kernkonzept klar und in einem Satz erklärbar
- [ ] Kritische Annahmen explizit und gegen Quellen geprüft
- [ ] Alternativen erwogen und Entscheidung begründet
- [ ] Stakeholder-Perspektiven berücksichtigt
- [ ] Nächste Schritte und offene Risiken benannt
- [ ] Präsentierbares Dokument / Deck vorhanden

---

## Profil: education

**Beschreibung:** Lernmaterial-Entwicklungs-Projekte — von der didaktischen Konzeption über Übungsdesign bis zur Assessment-Kalibrierung.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Outline | Lernziele definieren, Curriculum strukturieren |
| Primär | ExerciseDesign | Übungen und Praxisaufgaben entwickeln |
| Primär | AssessmentDesign | Tests, Quizze und Bewertungsrubriken entwickeln |
| Sekundär | Verification | Fachliche Korrektheit prüfen |
| Sekundär | Draft | Lernmaterialien ausformulieren |
| Optional | DocIngest | Bestehende Lehrpläne einlesen |

### MCP-Routing

1. **context7** — Fachspezifische Dokumentation
2. **firecrawl** — Bestehende Kurse und Curricula als Referenz extrahieren
3. **exa** — Lernforschung, didaktische Methoden
4. **filesystem** — Kursmaterialien ablegen
5. **memory** — Lernziel-Taxonomien speichern

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
modules/
modules/01-intro/
exercises/
assessments/
resources/
resources/references/
```

### Verifikations-Kriterien

- [ ] Lernziele klar, messbar und nach Taxonomie klassifiziert
- [ ] Übungen mit Musterlösungen und Bewertungshinweisen vorhanden
- [ ] Assessments auf Lernziele rückgebunden und kalibriert
- [ ] Fachliche Korrektheit bestätigt
- [ ] Materialien für Zielgruppe sprachlich angemessen
- [ ] Zeitaufwand-Schätzung pro Modul angegeben

---

## Profil: automation

**Beschreibung:** Automatisierungsprojekte — Skripte, Workflows, Integrationen. Robustheit, Fehlerbehandlung und Dokumentation entscheidend.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Spike | Machbarkeit und Integrations-Grenzen klären |
| Primär | CodeReview | Automatisierungs-Logik, Edge-Cases und Sicherheit prüfen |
| Primär | IntegrationTest | End-to-End-Verhalten testen |
| Sekundär | Debug | Fehler in Automatisierungs-Runs analysieren |
| Sekundär | Refactor | Workflows vereinfachen |
| Optional | DocIngest | API-Dokumentation einlesen |

### MCP-Routing

1. **context7** — API-Dokumentation für Drittdienste
2. **filesystem** — Skripte lesen/schreiben
3. **github** — Workflows in Repositories verwalten
4. **playwright** — Web-basierte Automationen testen
5. **exa** — Integrations-Tutorials suchen

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
scripts/
scripts/utils/
configs/
tests/
tests/fixtures/
workflows/
docs/
```

### Verifikations-Kriterien

- [ ] Automatisierung läuft fehlerfrei in der Zielumgebung
- [ ] Edge-Cases und Fehler-Szenarien explizit behandelt
- [ ] Logs und Monitoring vorhanden
- [ ] Rollback-Strategie dokumentiert
- [ ] Dokumentation vollständig
- [ ] Kein Hard-coded Secret im Code

---

## Profil: legal

**Beschreibung:** Rechtliche Arbeits-Projekte — Dokumente analysieren, juristische Recherchen, Compliance, Vertragsentwurfe. Präzision und Quellenangaben nicht verhandelbar.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DocIngest | Rechtsdokumente einlesen, Schlüsselklauseln identifizieren |
| Primär | Verification | Rechtliche Grundlagen gegen aktuelle Quellen prüfen |
| Primär | Draft | Vertragsentwürfe und Compliance-Dokumente formulieren |
| Sekundär | Spike | Spezifische Rechtsfragen klären |
| Sekundär | CodeReview | Technische Klauseln auf Korrektheit prüfen |
| Optional | Brainstorm | Risikobereiche ermitteln |

### MCP-Routing

1. **exa** — Aktuelle Gesetzestexte, Gerichtsurteile, Compliance-Guidelines
2. **firecrawl** — Offizielle Behörden-Webseiten scrapen
3. **filesystem** — Rechtsdokumente lesen und überarbeitete Versionen speichern
4. **memory** — Rechtliche Präzedenzfälle speichern

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
contracts/
contracts/drafts/
contracts/final/
research/
research/case-law/
compliance/
```

### Verifikations-Kriterien

- [ ] Alle Rechtsgrundlagen mit konkreten Quellen belegt
- [ ] Dokument von Fachperson freigegeben oder Vorbehalt dokumentiert
- [ ] Compliance-Anforderungen für alle relevanten Jurisdiktionen geprüft
- [ ] Risiken und offene Fragen explizit benannt
- [ ] Versionierung des Dokuments klar
- [ ] Hinweis: Kein Ersatz für Rechtsberatung (wenn für Endnutzer)

---

## Profil: finance

**Beschreibung:** Finanzanalyse- und Modellierungsprojekte — Unternehmensmodelle, Investment-Analysen, Budget-Forecasts.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DataIngest | Finanzdaten laden, Qualität prüfen |
| Primär | Hypothesis | Annahmen für Modelle formulieren und Sensitivität testen |
| Primär | Verification | Zahlen cross-validieren |
| Sekundär | ReportDraft | Ergebnisse in Executive-Summary überführen |
| Sekundär | InsightExtraction | Treiberanalyse, Haupthebel und Risiko-Szenarien identifizieren |
| Optional | Brainstorm | Szenarien (Base, Bull, Bear) entwickeln |

### MCP-Routing

1. **exa** — Branchenmultiplikatoren, Benchmark-Daten, Marktgröße-Studien
2. **firecrawl** — Jahresberichte und Investor-Präsentationen extrahieren
3. **context7** — Finanz-Bibliotheken dokumentieren
4. **filesystem** — Excel/CSV-Modelle lesen
5. **sequential-thinking** — Kausalitäten in Finanzmodellen durchdenken

### Adaptive Ordnerstruktur

```
.deepwork/planning/
.deepwork/research/
.deepwork/outputs/
.deepwork/journal/
models/
models/versions/
data/
data/raw/
data/processed/
reports/
forecasts/
assumptions/
```

### Verifikations-Kriterien

- [ ] Alle Eingangsdaten mit Quelle und Datum dokumentiert
- [ ] Modell-Annahmen explizit und nachvollziehbar begründet
- [ ] Sensitivitätsanalyse für kritische Treiber durchgeführt
- [ ] Zahlen in sich konsistent
- [ ] Base-, Bull- und Bear-Case definiert
- [ ] Executive Summary für Nicht-Finanz-Lesende verständlich

---

## Mischtypen (Mixed Projects)

Wenn ein Projekt mehrere Typen hat:

```yaml
project_type: coding
project_type_secondary: marketing  # z.B. SaaS mit Landing Page
```

**Primär-Typ bestimmt:** Haupt-Ordnerstruktur, Primäre Protokolle, Swarm-Sizing, MCP-Routing

**Sekundär-Typ fügt hinzu:** Top-3 Protokolle als Optional, Top-2 MCPs ans Ende, typ-spezifische Unterordner

### Häufige Mischtyp-Kombinationen

| Primär | Sekundär | Typischer Kontext |
|---|---|---|
| `coding` | `marketing` | SaaS-Produkt mit Landing Page und Ads |
| `coding` | `design` | Fullstack-Projekt mit UI-Eigenentwicklung |
| `research` | `content` | Whitepaper oder Thought-Leadership-Artikel |
| `concept` | `finance` | Business Plan oder Startup-Pitch |
| `content` | `marketing` | Content-Marketing-Strategie mit Umsetzung |
| `analysis` | `finance` | Datengetriebene Investment- oder Geschäfts-Analyse |
| `design` | `coding` | Design-System mit Implementierung |
| `education` | `content` | Kurs-Produktion mit Content-Marketing |

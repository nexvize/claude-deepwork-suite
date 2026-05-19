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

- [ ] Alle Tests grün (Unit, Integration, ggf. E2E)
- [ ] Code läuft ohne Fehler in der Zielumgebung
- [ ] Kein neuer Linting-/Typ-Fehler eingeführt
- [ ] Code Review abgeschlossen (mind. eine Durchsicht)
- [ ] Relevante Dokumentation aktualisiert
- [ ] Kein offener TODO/FIXME ohne Ticket

### Output-Konventionen

- Haupt-Outputs: `.deepwork/outputs/<section-id>/`
- Vault-Sync: `<VAULT>/Projects/<project-slug>/coding/`

---

## Profil: research

**Beschreibung:** Wissensrecherche-Projekte, die externe Quellen systematisch sammeln, bewerten und synthetisieren.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DocIngest | Quellen einlesen, indexieren, initial kategorisieren |
| Primär | Verification | Fakten gegen mehrere Quellen prüfen |
| Primär | Brainstorm | Forschungsfragen generieren, Blinde Flecken identifizieren |
| Sekundär | Spike | Schnelle Erstorientierung in unbekanntem Feld |
| Sekundär | InsightExtraction | Kernaussagen aus gescannten Quellen destillieren |
| Optional | ReportDraft | Ergebnisse zu lesbarem Bericht verdichten |

### MCP-Routing

1. **exa** — Semantische Websuche für Fachinhalte
2. **firecrawl** — Vollständigen Seiteninhalt scrapen
3. **context7** — Bibliotheken und Frameworks dokumentieren
4. **memory** — Gefundene Fakten sitzungsübergreifend speichern
5. **sequential-thinking** — Hypothesen schrittweise ausarbeiten

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

- [ ] Alle Kernaussagen durch mind. zwei unabhängige Quellen belegt
- [ ] Widersprüche explizit dokumentiert
- [ ] Synthesis-Dokument vollständig
- [ ] Quellenverzeichnis mit vollständigen Metadaten

---

## Profil: content

**Beschreibung:** Textproduktions-Projekte mit Fokus auf Qualität, Ton-Konsistenz und faktischer Korrektheit.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Brainstorm | Themen, Winkel und Formate generieren |
| Primär | Outline | Strukturentwurf und Argumentationsfluss klären |
| Primär | Draft | Erstentwurf schreiben |
| Sekundär | Edit | Ton, Klarheit, Lesbarkeit verbessern |
| Sekundär | Proofread | Grammatik, Rechtschreibung, Fakten-Endcheck |
| Optional | Verification | Faktencheck für spezifische Claims |

### MCP-Routing

1. **firecrawl** — Konkurrenz-Content scrapen, Fakten extrahieren
2. **exa** — Aktuelle Quellen für Fakten-Backing finden
3. **memory** — Stil-Guide sitzungsübergreifend speichern
4. **Gamma MCP** — Präsentationen und Slidedeck-Versionen generieren

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

---

## Profil: design

**Beschreibung:** UI/UX-Design-Projekte von der Wireframe-Phase bis zum Dev-Handoff.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | WireframeReview | Frühe Strukturkonzepte bewerten |
| Primär | DesignAudit | Bestehende Designs gegen Heuristiken prüfen |
| Primär | UX-Heuristics | Nielsen-Heuristiken systematisch durcharbeiten |
| Sekundär | FigmaSpec | Design-Spezifikation für Entwickler erstellen |
| Sekundär | Brainstorm | Konzeptalternativen generieren |
| Optional | Verification | Accessibility-Check, WCAG-Compliance |

### MCP-Routing

1. **Figma MCP** — Figma-Files lesen, Screenshots ziehen, Design-Tokens extrahieren
2. **playwright** — Live-UI im Browser screenshotten
3. **exa** — Design-Inspiration, Branchen-Benchmarks
4. **filesystem** — Assets exportieren, Spezifikations-Dokumente schreiben

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

---

## Profil: media

**Beschreibung:** KI-gestützte Medienproduktion — Bild- und Videogeneration, Prompt-Engineering, Asset-Pipelines.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | PromptEngineering | Optimale Generierungsprompts entwickeln |
| Primär | Storyboard | Sequenzen planen, Shot-Liste erstellen |
| Primär | AssetPipeline | Batch-Generierung orchestrieren |
| Sekundär | Brainstorm | Konzepte und Stilrichtungen generieren |
| Optional | Verification | Qualitätskontrolle, Brand-Konsistenz |

### MCP-Routing

1. **higgsfield** — Bild- und Videogeneration, Modell-Selektion
2. **filesystem** — Asset-Ordnerstruktur verwalten
3. **Figma MCP** — Moodboards erstellen, Storyboard-Frames layouten
4. **exa** — Stil-Referenzen recherchieren

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

---

## Profil: marketing

**Beschreibung:** Marketing- und Wachstumsprojekte, die Strategie, Copywriting, Kampagnenplanung und Asset-Koordination verbinden.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Brainstorm | Kampagnenkonzepte, Hooks, Zielgruppenanalyse |
| Primär | CampaignPlan | Kampagnenstruktur, Timeline, Kanalauswahl |
| Primär | CopyReview | Texte gegen Best Practices prüfen |
| Sekundär | Verification | Faktencheck für Claims |
| Sekundär | Outline | Content-Kalender strukturieren |
| Optional | DesignAudit | Visuelle Konsistenz prüfen |

### MCP-Routing

1. **exa** — Wettbewerber-Analyse, Branchentrends
2. **firecrawl** — Landingpages von Wettbewerbern extrahieren
3. **Figma MCP** — Brand-Assets abrufen
4. **memory** — Brand-Voice und Zielgruppenprofile speichern

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

---

## Profil: analysis

**Beschreibung:** Datengetriebene Analyseprojekte — von der Rohdaten-Ingestion über Hypothesen-Tests bis zum fertigen Insight-Report.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DataIngest | Rohdaten laden, Qualität prüfen |
| Primär | InsightExtraction | Muster und Kernergebnisse destillieren |
| Primär | Hypothesis-Test | Annahmen gegen Daten prüfen |
| Sekundär | ReportDraft | Erkenntnisse in Bericht überführen |
| Sekundär | Verification | Ergebnisse cross-validieren |
| Optional | Brainstorm | Hypothesen und Analysefragen generieren |

### MCP-Routing

1. **exa** — Benchmarks und Vergleichsdaten recherchieren
2. **firecrawl** — Externe Datensätze scrapen
3. **context7** — Analyse-Bibliotheken dokumentieren
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

---

## Profil: concept

**Beschreibung:** Konzeptionelle Planungsprojekte, bei denen Ideen strukturiert werden und eine kohärente Vision entsteht.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Brainstorm | Ideen generieren, Möglichkeitsraum öffnen |
| Primär | StructuredPlanning | Beste Ideen in kohärenten Plan überführen |
| Primär | Spike | Kritische Annahmen explorativ testen |
| Sekundär | Verification | Kernbehauptungen gegen Quellen prüfen |
| Sekundär | ReportDraft | Konzept in präsentierbares Dokument überführen |
| Optional | StakeholderMap | Interessengruppen identifizieren |

### MCP-Routing

1. **exa** — Marktrecherche, Wettbewerber, Branchenstudien
2. **sequential-thinking** — Konzepte Schritt für Schritt durchdenken
3. **memory** — Konzeptversionen und Stakeholder-Feedback speichern
4. **Gamma MCP** — Pitchdeck und Präsentation generieren
5. **firecrawl** — Referenzkonzepte aus dem Web extrahieren

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

1. **context7** — Fachspezifische Dokumentation (für Tech-Kurse)
2. **firecrawl** — Bestehende Kurse als Referenz extrahieren
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

---

## Profil: automation

**Beschreibung:** Automatisierungsprojekte, die wiederkehrende Prozesse mit Skripten, Workflows oder Integrationen effizienter machen.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Spike | Machbarkeit und Integrations-Grenzen klären |
| Primär | CodeReview | Automatisierungs-Logik und Sicherheit prüfen |
| Primär | IntegrationTest | End-to-End-Verhalten testen |
| Sekundär | Debug | Fehler in Automatisierungs-Runs analysieren |
| Sekundär | Refactor | Workflows vereinfachen und wartbarer machen |
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

---

## Profil: legal

**Beschreibung:** Rechtliche Arbeits-Projekte, die Dokumente analysieren, juristische Recherchen durchführen oder Vertragsentwürfe erstellen.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DocIngest | Rechtsdokumente einlesen, Schlüsselklauseln identifizieren |
| Primär | Verification | Rechtliche Grundlagen gegen aktuelle Quellen prüfen |
| Primär | Draft | Vertragsentwürfe und Compliance-Dokumente formulieren |
| Sekundär | Spike | Spezifische Rechtsfragen explorativ klären |
| Sekundär | CodeReview | Technische Klauseln auf Korrektheit prüfen |
| Optional | Brainstorm | Risikobereiche systematisch ermitteln |

### MCP-Routing

1. **exa** — Aktuelle Gesetzestexte, Gerichtsurteile suchen
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

---

## Profil: finance

**Beschreibung:** Finanzanalyse- und Modellierungsprojekte — von Unternehmensmodellen über Investment-Analysen bis zu Budget-Forecasts.

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DataIngest | Finanzdaten laden, Qualität prüfen |
| Primär | Hypothesis | Annahmen für Modelle formulieren und Sensitivität testen |
| Primär | Verification | Zahlen cross-validieren gegen externe Benchmarks |
| Sekundär | ReportDraft | Ergebnisse in Executive-Summary überführen |
| Sekundär | InsightExtraction | Treiberanalyse und Risiko-Szenarien identifizieren |
| Optional | Brainstorm | Szenarien (Base, Bull, Bear) entwickeln |

### MCP-Routing

1. **exa** — Branchenmultiplikatoren, Benchmark-Daten suchen
2. **firecrawl** — Jahresberichte von Vergleichs-Unternehmen extrahieren
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

---

## Mischtypen (Mixed Projects)

```yaml
project_type: coding
project_type_secondary: marketing  # z.B. SaaS mit Landing Page
```

**Primär-Typ bestimmt:** Haupt-Ordnerstruktur, primäre Protokolle, Swarm-Sizing, MCP-Routing.

**Sekundär-Typ fügt hinzu:** Top-3 Protokolle als Optional, Top-2 MCPs ans Ende, typ-spezifische Unterordner.

### Häufige Mischtyp-Kombinationen

| Primär | Sekundär | Typischer Kontext |
|---|---|---|
| `coding` | `marketing` | SaaS-Produkt mit Landing Page |
| `coding` | `design` | Fullstack-Projekt mit UI-Eigenentwicklung |
| `research` | `content` | Whitepaper oder Thought-Leadership |
| `concept` | `finance` | Business Plan oder Startup-Pitch |
| `content` | `marketing` | Content-Marketing-Strategie mit Umsetzung |
| `analysis` | `finance` | Datengetriebene Investment-Analyse |
| `design` | `coding` | Design-System mit Implementierung |
| `education` | `content` | Kurs-Produktion mit Content-Marketing |

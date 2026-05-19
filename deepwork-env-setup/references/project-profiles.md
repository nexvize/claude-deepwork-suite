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

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Alle Kernaussagen durch mindestens zwei unabhängige Quellen belegt
- [ ] Widersprüche zwischen Quellen explizit dokumentiert und bewertet
- [ ] Synthesis-Dokument vollständig und lesbar
- [ ] Quellenverzeichnis mit vollständigen Metadaten (URL, Datum, Autor)
- [ ] Offene Fragen und Forschungslücken benannt
- [ ] Kein Halluziniertes Zitat ohne Verifikation

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/research/`
- Datei-Format: `.md` für Synthesis und Berichte, `.bib` oder `.json` für Quellenverzeichnis, `.csv` für strukturierte Datensätze

---

## Profil: content

**Beschreibung:** Textproduktions-Projekte mit Fokus auf Qualität, Ton-Konsistenz und faktischer Korrektheit. Schreibprozess ist überwiegend sequenziell — von Outline über Drafts bis zum fertigen Stück.

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

Bevorzugte Reihenfolge für diesen Typ:
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

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Text liest sich flüssig und hat einen konsistenten Ton
- [ ] Alle Fakten und Zahlen sind verifiziert und mit Quellen belegt
- [ ] Headline und Opener sind stark und klar
- [ ] Zielgruppensprache passt (technisch vs. Business vs. Consumer)
- [ ] SEO-Grundregeln erfüllt (wenn relevant: Keywords, Meta, Struktur)
- [ ] Korrekturgelesen — keine Tippfehler, Grammatikfehler

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/content/`
- Datei-Format: `.md` für Drafts, `.html` für Publishing-Export, `.docx` für Kunden-Übergabe

---

## Profil: design

**Beschreibung:** UI/UX-Design-Projekte von der Wireframe-Phase bis zum Dev-Handoff. Umfasst Heuristik-Reviews, Figma-Arbeit, Komponentenspezifikation und Design-System-Pflege.

**Beispiele:** Onboarding-Flow für Mobile App, Design-System-Aufbau, Landingpage-Redesign, Dashboard-UX-Audit, Icon-Set-Produktion, Accessibility-Review

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

Bevorzugte Reihenfolge für diesen Typ:
1. **Figma MCP** — Figma-Files lesen, Screenshots ziehen, Code-Connect-Mappings, Design-Tokens extrahieren
2. **playwright** — Live-UI im Browser screenshotten, Interaktionen testen, Responsive-Verhalten prüfen
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

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Figma-Datei vollständig mit allen States (Default, Hover, Active, Error, Empty, Loading)
- [ ] Design-Spezifikation geschrieben (Abstände, Farben, Typografie, Breakpoints)
- [ ] Dev-Handoff-Kommentar in Figma vorhanden
- [ ] Accessibility-Mindestanforderungen erfüllt (Kontrastverhältnis, Touch-Target-Größe)
- [ ] Responsive-Verhalten für alle Breakpoints definiert
- [ ] Asset-Export (SVG, PNG) bereit

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/design/`
- Datei-Format: Figma-Links, `.png`/`.svg` für Assets, `.md` für Spezifikationen

---

## Profil: media

**Beschreibung:** KI-gestützte Medienproduktion — Bild- und Videogeneration, Prompt-Engineering, Asset-Pipelines und Storyboard-Entwicklung für visuelle Projekte.

**Beispiele:** Social-Media-Bilderserie, KI-generiertes Produktvideo, Storyboard für Werbespot, Avatar-Charakterentwicklung, Stock-Foto-Alternative-Produktion, Motion-Design-Konzept

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | PromptEngineering | Optimale Generierungsprompts entwickeln, iterativ verfeinern |
| Primär | Storyboard | Sequenzen planen, Shot-Liste erstellen, Timing definieren |
| Primär | AssetPipeline | Batch-Generierung orchestrieren, Assets organisieren und exportieren |
| Sekundär | Brainstorm | Konzepte, Stilrichtungen und Variationsideen generieren |
| Optional | Verification | Qualitätskontrolle, Brand-Konsistenz, Lizenz-Checks |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **higgsfield** — Bild- und Videogeneration, Modell-Selektion, Workspace-Management, Batch-Jobs
2. **filesystem** — Asset-Ordnerstruktur verwalten, exportierte Dateien organisieren
3. **Figma MCP** — Moodboards erstellen, Storyboard-Frames in Figma layouten
4. **exa** — Stil-Referenzen recherchieren, Prompt-Inspiration aus kuratierten Quellen

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelasset | 1–2 | Iterative Prompt-Verfeinerung, kein Parallelisierungsvorteil |
| Prompt-Variationstest | 5–10 | Parallele Generierung verschiedener Stile und Parameter |
| Großes Asset-Batch | 10–20 | Jeder Worker generiert eine Kategorie parallel, dann Kuratierung |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Assets in gewünschter Auflösung und Format generiert
- [ ] Qualitätskontrolle durchgeführt (Artefakte, Inkonsistenzen, Brand-Fit)
- [ ] Finale Prompts dokumentiert (für Reproduzierbarkeit)
- [ ] Assets sinnvoll benannt und in finale Ordnerstruktur überführt
- [ ] Lizenz und Nutzungsrechte der generierten Medien klar
- [ ] Storyboard mit Assets abgeglichen

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/media/`
- Datei-Format: `.png`, `.jpg`, `.mp4`, `.webm` für Assets; `.md` für Prompt-Dokumentation

---

## Profil: marketing

**Beschreibung:** Marketing- und Wachstumsprojekte, die Strategie, Copywriting, Kampagnenplanung und Asset-Koordination verbinden. Fokus auf Zielgruppenansprache, Positionierung und messbare Ergebnisse.

**Beispiele:** Go-to-Market-Strategie für SaaS-Launch, E-Mail-Kampagne für Produktfeature, SEO-Content-Strategie, Social-Media-Kampagne, Werbetexte A/B-Test, Wettbewerber-Positionierungsanalyse

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Brainstorm | Kampagnenkonzepte, Hooks, Zielgruppenanalyse, Positionierungswinkel |
| Primär | CampaignPlan | Kampagnenstruktur, Timeline, Kanalauswahl, Budget-Verteilung |
| Primär | CopyReview | Texte gegen Best Practices und Zielgruppenfeedback prüfen |
| Sekundär | Verification | Faktencheck für Claims, Wettbewerber-Vergleiche, Rechtliches |
| Sekundär | Outline | Content-Kalender und Redaktionsplan strukturieren |
| Optional | DesignAudit | Visuelle Konsistenz der Kampagnen-Assets prüfen |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **exa** — Wettbewerber-Analyse, Branchentrends, Keyword-Recherche, Zielgruppenrecherche
2. **firecrawl** — Landingpages und Kampagnenseiten von Wettbewerbern extrahieren, Pricing scrapen
3. **Figma MCP** — Brand-Assets abrufen, Kampagnen-Visuals reviewen, Design-System prüfen
4. **memory** — Brand-Voice, Zielgruppenprofile und Kampagnen-History speichern

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelne Anzeige / Copy | 1–3 | Copy-Variationen parallel, dann Pick |
| Kampagnen-Konzept | 4–8 | Konzept, Zielgruppe, Kanal und Asset-Worker parallel |
| Multi-Channel-Kampagne | 6–12 | Jeder Worker übernimmt einen Kanal oder eine Phase |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Kampagnenziel und KPIs klar definiert
- [ ] Copy reviewed und von Stakeholder freigegeben
- [ ] Alle Assets (Text, Bild, Video) produziert und organisiert
- [ ] Zeitplan und Verantwortlichkeiten festgelegt
- [ ] Legal-Check für Claims und Versprechen durchgeführt
- [ ] Tracking und Erfolgsmetriken eingerichtet

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/marketing/`
- Datei-Format: `.md` für Briefs und Copy, `.pdf` für Kunden-Präsentation, `.csv` für Redaktionspläne

---

## Profil: analysis

**Beschreibung:** Datengetriebene Analyseprojekte — von der Rohdaten-Ingestion über Hypothesen-Tests bis zum fertigen Insight-Report. Fokus auf Reproduzierbarkeit, Validierung und handlungsorientierte Erkenntnisse.

**Beispiele:** Nutzungsverhalten-Analyse einer App, Conversion-Funnel-Optimierung, Umfrage-Auswertung, Finanzmodell-Validierung, Produktfeedback-Cluster-Analyse, A/B-Test-Auswertung

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DataIngest | Rohdaten laden, Qualität prüfen, Struktur verstehen |
| Primär | InsightExtraction | Muster, Anomalien und Kernergebnisse aus Daten destillieren |
| Primär | Hypothesis-Test | Annahmen gegen Daten prüfen, Konfidenz bewerten |
| Sekundär | ReportDraft | Erkenntnisse in lesbaren, handlungsorientierten Bericht überführen |
| Sekundär | Verification | Ergebnisse cross-validieren, Methodikfehler suchen |
| Optional | Brainstorm | Hypothesen und Analysefragen generieren |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **exa** — Benchmarks und Vergleichsdaten recherchieren, Methodiken suchen
2. **firecrawl** — Externe Datensätze und Reports scrapen
3. **context7** — Analyse-Bibliotheken (pandas, numpy, R) dokumentieren
4. **filesystem** — Datendateien lesen, Analyse-Notebooks schreiben
5. **sequential-thinking** — Kausalitätsketten und Hypothesenbäume strukturiert aufbauen

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelne Metrik | 1–3 | Fokus auf Tiefe, sequentielle Analyse |
| Standard-Analyse | 5–10 | Parallelisierung nach Datensegment oder Hypothese |
| Großes Multi-Datensatz-Projekt | 10–20 | Jeder Worker analysiert eine Datensegment-Gruppe |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Alle Datenquellen zitiert und Qualität dokumentiert
- [ ] Kernaussagen statistisch abgesichert (Konfidenzintervalle, N dokumentiert)
- [ ] Methodik transparent und reproduzierbar beschrieben
- [ ] Annahmen explizit gemacht und kritisch bewertet
- [ ] Handlungsempfehlungen klar und priorisiert
- [ ] Bericht auch für Nicht-Datenmenschen lesbar

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/analysis/`
- Datei-Format: `.ipynb` für Notebooks, `.csv`/`.parquet` für Daten, `.md`/`.pdf` für Reports

---

## Profil: concept

**Beschreibung:** Konzeptionelle Planungsprojekte, bei denen Ideen strukturiert werden, Annahmen getestet werden und eine kohärente Vision für Stakeholder und Entscheidungsträger entsteht.

**Beispiele:** Startup-Konzept und Business Model, Produkt-Roadmap für neues Feature, Organisations-Redesign, Innovationsprojekt-Pitch, Service-Design-Konzept, Strategiepapier für Vorstand

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Brainstorm | Ideen generieren, Möglichkeitsraum öffnen, Alternativen entwickeln |
| Primär | StructuredPlanning | Beste Ideen in kohärenten Plan überführen, Abhängigkeiten klären |
| Primär | Spike | Kritische Annahmen in Zeitbox explorativ testen |
| Sekundär | Verification | Kernbehauptungen und Marktannahmen gegen Quellen prüfen |
| Sekundär | ReportDraft | Konzept in präsentierbares Dokument oder Pitch überführen |
| Optional | StakeholderMap | Interessengruppen identifizieren und Kommunikationsstrategie planen |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **exa** — Marktrecherche, Wettbewerber, Branchenstudien, vergleichbare Konzepte
2. **sequential-thinking** — Konzepte Schritt für Schritt durchdenken, Argumente schärfen
3. **memory** — Konzeptversionen und Stakeholder-Feedback sitzungsübergreifend speichern
4. **Gamma MCP** — Pitchdeck und Präsentation aus Konzept generieren
5. **firecrawl** — Referenzkonzepte und Fallstudien aus dem Web extrahieren

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelnes Konzept-Element | 1–2 | Tiefe schlägt Breite in konzeptioneller Arbeit |
| Konzept-Entwicklung | 3–6 | Verschiedene Winkel parallel erkunden, dann Synthese |
| Pitch-Vorbereitung | 4–8 | Inhalt, Visualisierung, Argumentation und Gegenfragen parallel |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Kernkonzept klar und in einem Satz erklärbar (Elevator Pitch)
- [ ] Kritische Annahmen explizit und gegen Quellen geprüft
- [ ] Alternativen erwogen und Entscheidung begründet
- [ ] Stakeholder-Perspektiven berücksichtigt
- [ ] Nächste Schritte und offene Risiken benannt
- [ ] Präsentierbares Dokument / Deck vorhanden

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/concept/`
- Datei-Format: `.md` für Konzeptdokumente, Gamma/PDF für Pitchdecks, `.canvas` für Obsidian-Mindmaps

---

## Profil: education

**Beschreibung:** Lernmaterial-Entwicklungs-Projekte — von der didaktischen Konzeption über Übungsdesign bis zur Assessment-Kalibrierung. Ziel sind klare Lernziele und messbare Lernergebnisse.

**Beispiele:** Online-Kurs zu Python für Einsteiger, Workshop-Curriculum für Design Thinking, Schulungsunterlagen für Softwareeinführung, Quiz-Bibliothek für Zertifizierungsvorbereitung, Lehrplan-Redesign, E-Learning-Modul

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Outline | Lernziele definieren, Curriculum strukturieren, Sequenz festlegen |
| Primär | ExerciseDesign | Übungen und Praxisaufgaben entwickeln, Schwierigkeitsgrad kalibrieren |
| Primär | AssessmentDesign | Tests, Quizze und Bewertungsrubriken entwickeln |
| Sekundär | Verification | Fachliche Korrektheit prüfen, didaktische Prinzipien anwenden |
| Sekundär | Draft | Lernmaterialien ausformulieren |
| Optional | DocIngest | Bestehende Lehrpläne und Referenzmaterialien einlesen |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **context7** — Fachspezifische Dokumentation (für Tech-Kurse: Bibliotheken, Frameworks, Specs)
2. **firecrawl** — Bestehende Kurse und Curricula als Referenz extrahieren
3. **exa** — Lernforschung, didaktische Methoden, Branchen-Benchmarks
4. **filesystem** — Kursmaterialien in strukturierter Ordnerhierarchie ablegen
5. **memory** — Lernziel-Taxonomien und Kurs-Progressions-Stand speichern

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelnes Modul | 1–3 | Didaktische Kohärenz erfordert starken gemeinsamen Kontext |
| Kurs-Entwicklung | 3–6 | Modul-Worker parallel, Synthesizer für Curriculum-Kohärenz |
| Großes Curriculum | 5–10 | Jeder Worker übernimmt ein Themenblock oder Lernziel-Cluster |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Lernziele klar, messbar und nach Taxonomie klassifiziert (z.B. Bloom)
- [ ] Übungen mit Musterlösungen und Bewertungshinweisen vorhanden
- [ ] Assessments auf Lernziele rückgebunden und kalibriert
- [ ] Fachliche Korrektheit von Experten oder zweiter Quelle bestätigt
- [ ] Materialien für Zielgruppe sprachlich und didaktisch angemessen
- [ ] Zeitaufwand-Schätzung pro Modul angegeben

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/education/`
- Datei-Format: `.md` für Lernmaterialien, `.json`/`.yaml` für Quizze, `.pdf` für Lernende

---

## Profil: automation

**Beschreibung:** Automatisierungsprojekte, die wiederkehrende Prozesse mit Skripten, Workflows oder Integrationen effizienter machen. Robustheit, Fehlerbehandlung und Dokumentation sind entscheidend.

**Beispiele:** GitHub Actions CI/CD-Pipeline, Zapier-/Make-Workflow für CRM-Integration, Python-Skript für täglichen Report-Export, n8n-Automatisierung für E-Mail-Routing, Shell-Skript für Server-Maintenance, API-Webhook-Integration

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Spike | Machbarkeit und Integrations-Grenzen in Zeitbox klären |
| Primär | CodeReview | Automatisierungs-Logik, Edge-Cases und Sicherheit prüfen |
| Primär | IntegrationTest | End-to-End-Verhalten unter realen Bedingungen testen |
| Sekundär | Debug | Fehler in Automatisierungs-Runs analysieren und beheben |
| Sekundär | Refactor | Workflows vereinfachen und wartbarer machen |
| Optional | DocIngest | API-Dokumentation von Integrations-Partnern einlesen |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **context7** — API-Dokumentation für Drittdienste, Framework-Docs für Workflow-Tools
2. **filesystem** — Skripte lesen/schreiben, Konfigurationsdateien verwalten
3. **github** — Workflows in Repositories verwalten, Actions-Logs lesen
4. **playwright** — Web-basierte Automationen testen, Browser-Workflows verifizieren
5. **exa** — Integrations-Tutorials und Fehler-Lösungen suchen

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelner Workflow-Schritt | 1–2 | Fokussierter Kontext, sequentielle Logik |
| Standard-Automatisierung | 2–5 | Entwicklung, Test und Doku parallel |
| Komplexes Integrations-Projekt | 4–8 | Jeder Worker übernimmt eine System-Integration |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Automatisierung läuft fehlerfrei in der Zielumgebung
- [ ] Edge-Cases und Fehler-Szenarien explizit behandelt (Timeouts, leere Inputs, API-Fehler)
- [ ] Logs und Monitoring vorhanden (was passiert wann mit welchem Ergebnis)
- [ ] Rollback-Strategie oder manuelle Override-Möglichkeit dokumentiert
- [ ] Dokumentation: Zweck, Trigger, Inputs, Outputs, Abhängigkeiten
- [ ] Kein Hard-coded Secret oder Credential im Code

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/automation/`
- Datei-Format: `.py`, `.sh`, `.yaml`/`.json` für Konfigurationen, `.md` für Runbooks

---

## Profil: legal

**Beschreibung:** Rechtliche Arbeits-Projekte, die Dokumente analysieren, juristische Recherchen durchführen, Compliance prüfen oder Vertragsentwürfe erstellen. Präzision und Quellenangaben sind nicht verhandelbar.

**Beispiele:** AGB-Review für SaaS-Produkt, DSGVO-Compliance-Prüfung, Vertragsentwurf für Freelancer-Vereinbarung, NDA-Analyse, Lizenzmodell-Vergleich, Datenschutzerklärung aktualisieren

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DocIngest | Rechtsdokumente einlesen, Struktur und Schlüsselklauseln identifizieren |
| Primär | Verification | Rechtliche Grundlagen gegen aktuelle Quellen prüfen, Widersprüche aufdecken |
| Primär | Draft | Vertragsentwürfe und Compliance-Dokumente formulieren |
| Sekundär | Spike | Spezifische Rechtsfragen in Zeitbox explorativ klären |
| Sekundär | CodeReview | Technische Klauseln (z.B. in Software-Verträgen) auf Korrektheit prüfen |
| Optional | Brainstorm | Risikobereiche und blinde Flecken systematisch ermitteln |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **exa** — Aktuelle Gesetzestexte, Gerichtsurteile, Compliance-Guidelines suchen
2. **firecrawl** — Offizielle Behörden-Webseiten und Gesetzesdatenbanken scrapen
3. **filesystem** — Rechtsdokumente lesen und überarbeitete Versionen speichern
4. **memory** — Rechtliche Präzedenzfälle und projektspezifische Compliance-Entscheidungen speichern

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelnes Dokument | 1–2 | Hohe Präzision erfordert fokussierten Kontext |
| Compliance-Audit | 3–5 | Jeder Worker prüft einen Rechtsbereich parallel |
| Multi-Jurisdiktions-Analyse | 4–8 | Pro Jurisdiktion ein Worker, dann Synthesizer |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Alle Rechtsgrundlagen mit konkreten Quellen (Gesetz, Paragraph, Urteil) belegt
- [ ] Dokument von Fachperson (Anwalt oder qualifizierter Reviewer) freigegeben oder Vorbehalt dokumentiert
- [ ] Compliance-Anforderungen für alle relevanten Jurisdiktionen geprüft
- [ ] Risiken und offene Fragen explizit benannt — nichts unter den Tisch gekehrt
- [ ] Versionierung des Dokuments klar (Datum, Änderungshistorie)
- [ ] Hinweis enthalten: Kein Ersatz für Rechtsberatung (wenn für Endnutzer)

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/legal/`
- Datei-Format: `.docx` für Verträge (Track-Changes-fähig), `.md` für interne Analyse, `.pdf` für finale Versionen

---

## Profil: finance

**Beschreibung:** Finanzanalyse- und Modellierungsprojekte — von Unternehmensmodellen über Investment-Analysen bis zu Budget-Forecasts. Datenqualität, Nachvollziehbarkeit und Szenario-Denken stehen im Mittelpunkt.

**Beispiele:** SaaS-Finanzmodell für Investor-Deck, Break-even-Analyse für neues Produkt, Liquiditätsplanung, Marktgröße-Schätzung (TAM/SAM/SOM), ROI-Kalkulation für Marketing-Kanal, Jahresbudget-Planung

### Protokolle

| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | DataIngest | Finanzdaten laden, Qualität prüfen, Periodizität verstehen |
| Primär | Hypothesis | Annahmen für Modelle formulieren und Sensitivität testen |
| Primär | Verification | Zahlen cross-validieren, Annahmen gegen externe Benchmarks prüfen |
| Sekundär | ReportDraft | Ergebnisse in Executive-Summary und Investor-Material überführen |
| Sekundär | InsightExtraction | Treiberanalyse, Haupthebel und Risiko-Szenarien identifizieren |
| Optional | Brainstorm | Szenarien (Base, Bull, Bear) und Sensitivity-Cases entwickeln |

### MCP-Routing

Bevorzugte Reihenfolge für diesen Typ:
1. **exa** — Branchenmultiplikatoren, Benchmark-Daten, Marktgröße-Studien, Vergleichs-Unternehmen
2. **firecrawl** — Jahresberichte und Investor-Präsentationen von vergleichbaren Unternehmen extrahieren
3. **context7** — Finanz-Bibliotheken (z.B. pandas-datareader, yfinance) dokumentieren
4. **filesystem** — Excel/CSV-Modelle lesen, bearbeitete Versionen speichern
5. **sequential-thinking** — Kausalitäten in Finanzmodellen systematisch durchdenken

### Swarm-Sizing

| Section-Typ | Empfohlene Größe | Begründung |
|---|---|---|
| Einzelne Kalkulation | 1–2 | Fokus auf Korrektheit, sequentiell sicherer |
| Finanzmodell-Aufbau | 3–6 | Umsatz, Kosten, Cash-Flow und Bewertung parallel |
| Investor-Deck-Vorbereitung | 4–8 | Modell, Narrativ, Visualisierung und Sensitivität parallel |

### Adaptive Ordnerstruktur

Ordner die deepwork-00-bootstrap anlegt:

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

"Fertig" für diesen Typ bedeutet:
- [ ] Alle Eingangsdaten mit Quelle und Datum dokumentiert
- [ ] Modell-Annahmen explizit und nachvollziehbar begründet
- [ ] Sensitivitätsanalyse für kritische Treiber durchgeführt
- [ ] Zahlen in sich konsistent (keine zirkulären Bezüge, kein Copy-Paste-Fehler)
- [ ] Base-, Bull- und Bear-Case definiert
- [ ] Executive Summary für Nicht-Finanz-Lesende verständlich

### Output-Konventionen

- Haupt-Outputs gehen nach: `.deepwork/outputs/<section-id>/`
- Vault-Sync nach: `<VAULT>/Projects/<project-slug>/finance/`
- Datei-Format: `.xlsx` für Modelle, `.md` für Analyse-Berichte, `.pdf` für Investor-Ausgaben

---

## Mischtypen (Mixed Projects)

Wenn ein Projekt mehrere Typen hat, können beide in `PROJECT.md` angegeben werden:

```yaml
project_type: coding
project_type_secondary: marketing  # z.B. SaaS mit Landing Page
```

### Verhaltensregeln für Mischtypen

**Primär-Typ bestimmt:**
- Haupt-Ordnerstruktur (deepwork-00-bootstrap verwendet Primär-Typ-Ordner)
- Primäre und sekundäre Protokolle (vollständige Protokoll-Liste des Primär-Typs)
- Swarm-Sizing-Vorgabe
- Haupt-MCP-Routing-Reihenfolge

**Sekundär-Typ fügt hinzu:**
- Top-3 Protokolle des Sekundär-Typs als `Optional` in die Protokoll-Liste
- Top-2 MCPs des Sekundär-Typs ans Ende der MCP-Routing-Reihenfolge (wenn nicht bereits vorhanden)
- Typ-spezifische Unterordner werden zusätzlich angelegt

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

### Verifikation bei Mischtypen

"Fertig" bedeutet: Alle Verifikations-Kriterien des Primär-Typs sind erfüllt, plus die Top-3 Kriterien des Sekundär-Typs.

### Output-Konventionen bei Mischtypen

Vault-Sync nach: `<VAULT>/Projects/<project-slug>/<primär-typ>/` (Haupt-Outputs)  
Sekundär-Typ-Outputs in: `<VAULT>/Projects/<project-slug>/<sekundär-typ>/` (Zusatz-Outputs)

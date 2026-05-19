→ Vollständiges Profil-Dokument: siehe `deepwork-env-setup/references/project-profiles.md`

Dieses Dokument ist die kanonische Quelle für alle 12 Projekttyp-Profile.
Der gleiche Inhalt ist in kompakter Form unten als Schnell-Referenz verfügbar.

# Project Profiles — Schnell-Referenz (deepwork-03-execute)

## Projekttyp aus PROJECT.md lesen

```yaml
project_type: coding
project_type_secondary: marketing  # optional
```

## Protokoll-Kurzreferenz nach Typ

| Typ | Primäre Protokolle | Key MCPs |
|---|---|---|
| coding | Debug, CodeReview, TDD, Refactor, Spike | context7, filesystem, github, playwright |
| research | DocIngest, Verification, Brainstorm, Spike | exa, firecrawl, context7, memory |
| content | Brainstorm, Outline, Draft, Edit, Proofread | firecrawl, exa, memory, Gamma |
| design | WireframeReview, DesignAudit, UX-Heuristics, FigmaSpec | Figma MCP, playwright, exa |
| media | PromptEngineering, Storyboard, AssetPipeline | higgsfield, filesystem, Figma MCP |
| marketing | Brainstorm, CampaignPlan, CopyReview, Verification | exa, firecrawl, Figma MCP, memory |
| analysis | DataIngest, InsightExtraction, Hypothesis-Test, ReportDraft | exa, firecrawl, context7, filesystem |
| concept | Brainstorm, StructuredPlanning, Spike, Verification | exa, sequential-thinking, memory, Gamma |
| education | Outline, ExerciseDesign, AssessmentDesign, Draft | context7, firecrawl, exa, filesystem |
| automation | Spike, CodeReview, IntegrationTest, Debug | context7, filesystem, github, playwright |
| legal | DocIngest, Verification, Draft, Spike | exa, firecrawl, filesystem, memory |
| finance | DataIngest, Hypothesis, Verification, ReportDraft | exa, firecrawl, context7, filesystem |

## Verifikations-Kriterien nach Typ (für deepwork-03 Section-Abschluss)

| Typ | "Fertig" bedeutet |
|---|---|
| coding | Tests grün, kein Linting-Fehler, Code Review done |
| research | Alle Claims belegt, Synthesis vollständig |
| content | Text gelesen, Fakten geprüft, Proofread done |
| design | Alle States definiert, Figma-Handoff ready |
| media | Assets generiert, Qualität geprüft, Prompts dokumentiert |
| marketing | Copy reviewed, Assets produziert, Tracking eingerichtet |
| analysis | Methodik transparent, Zahlen cross-validiert |
| concept | Elevator Pitch klar, Annahmen geprüft, Deck vorhanden |
| education | Lernziele messbar, Übungen mit Lösungen, Assessment kalibriert |
| automation | Automation läuft fehlerfrei, Edge-Cases behandelt, Logs vorhanden |
| legal | Rechtsgrundlagen belegt, Fachperson-Review, Risiken benannt |
| finance | Datenquellen zitiert, Modell-Annahmen begründet, Base/Bull/Bear definiert |

## Adaptive Ordnerstruktur nach Typ

| Typ | Typ-spezifische Ordner (zusätzlich zu .deepwork/) |
|---|---|
| coding | src/, tests/, docs/, scripts/ |
| research | sources/raw/, sources/annotated/, synthesis/, reports/ |
| content | drafts/v1/, drafts/final/, published/, assets/images/ |
| design | wireframes/, specs/components/, assets/icons/, components/ |
| media | prompts/templates/, assets/generated/, exports/, storyboards/ |
| marketing | copy/drafts/, campaigns/, assets/visuals/, briefs/ |
| analysis | data/raw/, reports/, insights/, models/, notebooks/ |
| concept | ideas/brainstorms/, roadmaps/, pitches/, stakeholders/ |
| education | modules/01-intro/, exercises/, assessments/, resources/references/ |
| automation | scripts/utils/, configs/, tests/fixtures/, workflows/ |
| legal | contracts/drafts/, research/case-law/, compliance/ |
| finance | models/versions/, data/raw/, reports/, forecasts/, assumptions/ |

## Mischtypen

```yaml
project_type: coding
project_type_secondary: marketing
```

Primär-Typ bestimmt Hauptstruktur + primäre Protokolle. Sekundär-Typ fügt Top-3 Protokolle als Optional hinzu.

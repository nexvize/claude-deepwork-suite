→ Vollständiges Profil-Dokument: siehe `deepwork-env-setup/references/project-profiles.md`

Dieses Dokument ist die kanonische Quelle für alle 12 Projekttyp-Profile.
Der gleiche Inhalt ist in kompakter Form unten als Schnell-Referenz verfügbar.

# Project Profiles — Schnell-Referenz (deepwork-quick)

## Projekttyp aus PROJECT.md lesen

```yaml
project_type: coding
project_type_secondary: marketing  # optional
```

## Dynamische Protokoll-Tabelle nach Typ

| Typ | Primäre Protokoll-Optionen | Protokoll-Quelle |
|---|---|---|
| coding | Code Review, Debug, Refactor, Spike, TDD, Verification | native-protocols.md |
| research | Document Ingest, Spike, Verification, Brainstorm | native-protocols.md |
| content | Brainstorm, Outline, Draft, Edit, Proofread, SEO-Optimize | content-protocols.md |
| design | WireframeReview, DesignAudit, UX-Heuristics, FigmaSpec, ComponentInventory | design-protocols.md |
| media | PromptEngineering, Storyboard, AssetInventory, VideoScript | media-protocols.md |
| marketing | Brainstorm, CampaignPlan, CopyReview, Verification, SEO-Optimize | native + content-protocols.md |
| analysis | DataIngest, InsightExtraction, Hypothesis-Test, ReportDraft | analysis-protocols.md |
| concept | Brainstorm, StructuredPlanning, Spike, PitchDeck, RoadmapBuild | concept-protocols.md |
| education | LearningOutcomes, CurriculumOutline, ExerciseDesign, AssessmentDesign | education-protocols.md |
| automation | Spike, CodeReview, IntegrationTest, Verification | native-protocols.md |
| legal | Document Ingest, Verification, Draft, Spike | native-protocols.md |
| finance | DataIngest, Hypothesis-Test, Verification, ReportDraft | analysis-protocols.md |

## Intensitäts-Skala

1. Überblick: Offensichtlichstes, 5–10 Minuten
2. Basis: Wichtigste Punkte, 15–20 Minuten
3. ⭐ Standard (empfohlen): Vollständig, alle Aspekte
4. Tiefgehend: Mit Gegenprüfung, jede Annahme hinterfragen
5. Exhaustiv: Alles — maximale Kosten, maximale Abdeckung

## Mischtypen

```yaml
project_type: coding
project_type_secondary: marketing
```

Zeige primäre Protokolle des Haupttyps + Top-3 des Sekundärtyps als Optional.

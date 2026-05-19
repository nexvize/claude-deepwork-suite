# Concept Protocols — Stub (deepwork-00-bootstrap)

Canonical source: `deepwork-env-setup/references/concept-protocols.md`

Nicht benoetigt waehrend Bootstrap. Relevante Protokolle werden von deepwork-01-discovery oder deepwork-quick geladen, sobald `project_type: concept`, `research` oder `marketing` erkannt wurde.

Typ-spezifische Ordnerstruktur fuer concept (wird in Step 3 angelegt):
```
.deepwork/
  planning/    <- StructuredPlan, RiskMatrix, StakeholderMap
  outputs/     <- Pitch-Decks, Roadmaps, Analysen
ideas/         <- Ideensammlungen
roadmaps/      <- Roadmap-Dokumente
pitches/       <- Pitch-Materialien
stakeholders/  <- Stakeholder-Dokumentation
```

# Education Protocols — Stub (deepwork-00-bootstrap)

Canonical source: `deepwork-env-setup/references/education-protocols.md`

Nicht benoetigt waehrend Bootstrap. Relevante Protokolle werden von deepwork-01-discovery oder deepwork-quick geladen, sobald `project_type: education`, `concept` oder `content` erkannt wurde.

Typ-spezifische Ordnerstruktur fuer education (wird in Step 3 angelegt):
```
.deepwork/
  planning/      <- LearningOutcomes, CurriculumOutline, LearnerPersona
  outputs/       <- Modul-Outputs, Assessments
modules/         <- Kursmodule
exercises/       <- Uebungsaufgaben
assessments/     <- Tests und Pruefungen
resources/       <- Lernmaterialien
```

# Education Protocols — deepwork-alt-autopilot Context

Fuer project_type: education, concept, content

Vollstaendige Protokoll-Definitionen: `deepwork-env-setup/references/education-protocols.md`

## Auto-Sequenzen fuer Education-Projekte

**Standard-Kurs:**
LearnerPersona → LearningOutcomes → CurriculumOutline → ConceptExplanation (je Modul) → ExerciseDesign → AssessmentDesign

**Tutorial/How-To:**
LearnerPersona → LearningOutcomes (2-3 Ziele) → ConceptExplanation → ExerciseDesign

**Workshop (1 Tag):**
LearnerPersona → LearningOutcomes → CurriculumOutline (kompakt) → ExerciseDesign

## Swarm-Sizing fuer Education

| Aufgabe | Swarm-Groesse | Begruendung |
|---|---|---|
| LearnerPersona | 1-2 Worker | Pro Zielgruppe ein Worker |
| LearningOutcomes | 1 Worker | Sequenziell (Constructive Alignment) |
| CurriculumOutline | 1 Worker | Abhaengigkeits-Graph erfordert Sequenz |
| ConceptExplanation | 1 Worker pro Modul | Parallel wenn Module unabhaengig |
| ExerciseDesign | 2-4 Worker | Je Lernziel-Gruppe ein Worker |
| AssessmentDesign | 1 Worker | Interne Konsistenz erfordert Sequenz |

**Always-Pause bei:** Publikation von Lernmaterialien auf externe Plattformen, Zertifizierungs-Entscheidungen.

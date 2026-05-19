# Education Protocols — deepwork-entry-analyze Context

## Projekttyp-Erkennung: education / concept / content

**Indikatoren fuer project_type: education:**
- Ordner: `modules/`, `exercises/`, `assessments/`, `resources/`
- Dateien: Curriculum-Dokumente, Quiz-Dateien, Modul-Beschreibungen
- Keywords in PROJECT.md: "kurs", "tutorial", "lernziel", "modul", "uebung", "assessment", "onboarding"
- Plattformen: Moodle, Teachable, Thinkific, Udemy, Notion (als Wiki)

**Indikatoren fuer project_type: content (mit Education-Elementen):**
- Keywords: "erklaerung", "how-to", "blog", "guide", "anleitung"

## Migration-Checks fuer education-Projekte

Fehlende Ordner (anlegen bei Migration):
- `.deepwork/planning/` — LearningOutcomes, CurriculumOutline, LearnerPersona
- `.deepwork/outputs/` — Modul-Outputs, Assessment-Outputs
- `modules/` — Falls noch nicht vorhanden
- `exercises/` — Falls noch nicht vorhanden
- `assessments/` — Falls noch nicht vorhanden

Protokoll-Referenz: `deepwork-env-setup/references/education-protocols.md`

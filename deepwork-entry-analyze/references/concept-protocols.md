# Concept Protocols — deepwork-entry-analyze Context

## Projekttyp-Erkennung: concept / research / marketing

**Indikatoren fuer project_type: concept:**
- Ordner: `ideas/`, `roadmaps/`, `pitches/`, `stakeholders/`
- Dateien: Pitch-Decks (.pptx), Roadmaps, Strategiepapiere (.md/.docx)
- Keywords in PROJECT.md: "konzept", "strategie", "roadmap", "pitch", "stakeholder", "vision"

**Indikatoren fuer project_type: marketing:**
- Keywords: "kampagne", "copy", "brief", "brand", "SEO", "conversion", "funnel"
- Ordner: `copy/`, `campaigns/`, `assets/`, `briefs/`
- Tools: Mailchimp, HubSpot, Google Ads, Meta Ads

**Indikatoren fuer project_type: research:**
- Keywords: "recherche", "literatur", "studie", "quellen", "analyse", "synthese"
- Ordner: `sources/`, `synthesis/`, `reports/`

## Migration-Checks fuer concept-Projekte

Fehlende Ordner (anlegen bei Migration):
- `.deepwork/planning/` — StructuredPlan, RiskMatrix, StakeholderMap
- `.deepwork/outputs/` — Pitch-Decks, Roadmap-Outputs
- `roadmaps/` — Falls noch nicht vorhanden
- `stakeholders/` — Falls noch nicht vorhanden

Protokoll-Referenz: `deepwork-env-setup/references/concept-protocols.md`

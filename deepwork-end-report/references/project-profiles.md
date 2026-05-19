→ Vollständiges Profil-Dokument: siehe `deepwork-env-setup/references/project-profiles.md`

Dieses Dokument ist die kanonische Quelle für alle 12 Projekttyp-Profile.
Der gleiche Inhalt ist in kompakter Form unten als Schnell-Referenz verfügbar.

# Project Profiles — Schnell-Referenz (deepwork-end-report)

## Projekttyp aus PROJECT.md lesen

```yaml
project_type: coding
project_type_secondary: marketing  # optional
```

## Typ-spezifische Abschluss-Sektionen für PROJECT-COMPLETE.md

| Typ | Pflicht-Sektionen in PROJECT-COMPLETE.md |
|---|---|
| coding | Test-Coverage-Report, Tech-Debt-Log, Architecture-Snapshot, Deployment-Guide |
| research | Source-Quality-Assessment, Confidence-Levels, Knowledge-Gaps, Citation-Index |
| content | Publication-Checklist, SEO-Meta, Distribution-Plan, Performance-Baseline |
| design | Design-System-Inventory, Handoff-Completeness, Accessibility-Score, Asset-Catalog |
| media | Asset-Catalog, Prompt-Library, Brand-Consistency-Report, License-Clearance |
| marketing | Campaign-Results, KPI-Achievement, Copy-Archive, Lessons-Learned |
| analysis | Methodology-Documentation, Data-Lineage, Insight-Summary, Recommendation-Tracker |
| concept | Decision-Log, Stakeholder-Sign-off, Risk-Resolved, Roadmap-Next-Phase |
| education | Learning-Outcomes-Achievement, Assessment-Results, Curriculum-Review, Learner-Feedback |
| automation | Runbook, Monitoring-Setup, Error-Handling-Docs, Rollback-Procedure |
| legal | Compliance-Clearance, Legal-Review-Sign-off, Document-Version-History, Risk-Register |
| finance | Model-Assumptions-Log, Sensitivity-Analysis, Executive-Summary, Audit-Trail |

## Verifikations-Kriterien nach Typ (Abschluss-Check)

| Typ | Abschluss-Kriterien |
|---|---|
| coding | Tests grün, kein Linting-Fehler, Code Review done, Docs aktuell |
| research | Alle Claims belegt, Synthesis vollständig, Quellenverzeichnis komplett |
| content | Text gelesen, Fakten geprüft, Proofread done, SEO-Grundregeln erfüllt |
| design | Alle States definiert, Figma-Handoff ready, WCAG-Mindestanforderungen erfüllt |
| media | Assets generiert + qualitätsgecheckt, Prompts dokumentiert, Lizenzen klar |
| marketing | Copy reviewed, Assets produziert, Tracking eingerichtet, Legal-Check done |
| analysis | Methodik transparent, Zahlen cross-validiert, Handlungsempfehlungen klar |
| concept | Elevator Pitch klar, Annahmen geprüft, Alternativen erwogen, Deck vorhanden |
| education | Lernziele messbar, Übungen mit Lösungen, Assessment kalibriert, Zeitschätzungen da |
| automation | Automation fehlerfrei, Edge-Cases behandelt, Logs + Monitoring vorhanden |
| legal | Rechtsgrundlagen belegt, Fachperson-Review, Versionierung klar |
| finance | Datenquellen zitiert, Sensitivitätsanalyse done, Base/Bull/Bear definiert |

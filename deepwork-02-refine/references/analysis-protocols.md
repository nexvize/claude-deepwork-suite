# Analysis Protocols — deepwork-02-refine Context

Fuer project_type: analysis, research, finance

Vollstaendige Protokoll-Definitionen: `deepwork-env-setup/references/analysis-protocols.md`

## Section-Splitting fuer Analysis-Projekte

Jede Section entspricht einer Analyse-Frage oder einem Daten-Bereich:

| Section-Typ | Protokoll | Output |
|---|---|---|
| Pro Datensatz/Quelle | DataIngest | Schema + Qualitaetsbericht |
| Pro Analysefrage | InsightExtraction | Insight-Dokument mit Quantifizierung |
| Pro Hypothese | Hypothesis-Test | Test-Ergebnis + Business-Empfehlung |
| Dashboard (falls geplant) | DashboardSpec | Spec-Dokument fuer BI-Tool |
| Abschlussbericht | ReportDraft | Executive Summary + Findings + Appendix |
| Marktanalyse | CompetitiveAnalysis | Positionierungsmatrix + Implikationen |

**Vertical Slice:** Jede Section muss eigenstaendige, lieferbare Outputs haben die auch ohne andere Sections verstaendlich sind.

**Reihenfolge-Empfehlung:** DataIngest zuerst (alle anderen bauen darauf auf), dann InsightExtraction / Hypothesis-Test parallel, dann ReportDraft zuletzt.

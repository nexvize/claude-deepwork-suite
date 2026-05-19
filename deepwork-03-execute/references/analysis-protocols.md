# Analysis Protocols — deepwork-03-execute Context

Fuer project_type: analysis, research, finance

Vollstaendige Protokoll-Definitionen: `deepwork-env-setup/references/analysis-protocols.md`

## Empfohlene Ausfuehrungs-Reihenfolge

1. **DataIngest** → Schema + Qualitaets-Report
2. **InsightExtraction** → Key Insights mit Quantifizierung + Chart-Empfehlungen
3. **Hypothesis-Test** → p-Wert, Konfidenzintervall, Business-Empfehlung
4. **DashboardSpec** → falls Dashboard geplant: Metriken, Layout, Datenquellen
5. **ReportDraft** → Executive Summary zuerst schreiben, dann Findings
6. **CompetitiveAnalysis** → falls Marktanalyse Teil des Projekts

## Verification-Kriterien fuer Analysis-Sections

- Jeder Insight muss quantifiziert sein (keine vagen Aussagen wie "gestiegen")
- Jede Empfehlung durch ein Finding belegt
- Alle Datenquellen in Appendix dokumentiert
- Konfidenz-Level pro Insight: Hoch / Mittel / Niedrig
- Limitationen und Annahmen explizit gemacht
- Executive Summary ohne Fachkenntnisse verstaendlich

## Self-Verification (Analysis)

Nach jeder Section:
- Sind die Outputs im richtigen plain-text Format? (keine Markdown-Tabellen in Reports)
- Stimmen alle Zahlen intern ueberein (kein Widerspruch zwischen Executive Summary und Appendix)?

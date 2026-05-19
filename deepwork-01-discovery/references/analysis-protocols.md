# Analysis Protocols — deepwork-01-discovery Context

Fuer project_type: analysis, research, finance

Vollstaendige Protokoll-Definitionen: `deepwork-env-setup/references/analysis-protocols.md`

## Fuer Discovery am relevantesten

**DataIngest** — Inventarisiere und dokumentiere alle Datenquellen. Erstelle Schema + Datenqualitaets-Report. Entscheide ob Daten ausreichen fuer die Ziel-Insights.

**CompetitiveAnalysis** — Fuer research- und marketing-Projekte: Markt und Wettbewerb verstehen, Positionierungsmatrix erstellen.

**Hypothesis-Test** — Formuliere Analysefragen als testbare Hypothesen mit Konfidenz-Level und definiertem Test-Design.

## Discovery Deliverables (analysis/research/finance)

- DataIngest Output falls Daten verfuegbar (Schema + Qualitaetsbericht)
- Analysefragen priorisiert nach Business-Impact
- Methodologie-Entscheidung (quantitativ / qualitativ / gemischt)
- MCPs fuer diese Phase: exa (Marktdaten-Research), firecrawl (Web-Scraping fuer Competitive)
- VERDICT.md: Sind die Daten ausreichend? Ist die Analysefrage beantwortbar? GO / NO-GO

## MCP-Routing fuer analysis

- exa: Marktdaten, Branchenberichte, Wettbewerber-Infos
- firecrawl: Web-Scraping fuer Pricing-Seiten, Review-Plattformen (G2/Capterra)
- context7: Statistik-Bibliotheken (pandas, scipy, dbt)
- memory: Zwischenergebnisse persistent halten

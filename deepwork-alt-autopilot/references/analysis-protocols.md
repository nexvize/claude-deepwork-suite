# Analysis Protocols — deepwork-alt-autopilot Context

Fuer project_type: analysis, research, finance

Vollstaendige Protokoll-Definitionen: `deepwork-env-setup/references/analysis-protocols.md`

## Auto-Sequenzen fuer Analysis-Projekte

**Standard-Analyse:**
DataIngest → InsightExtraction → ReportDraft

**Mit Dashboard:**
DataIngest → InsightExtraction → DashboardSpec → ReportDraft

**Markt-/Wettbewerbsanalyse:**
CompetitiveAnalysis → InsightExtraction → ReportDraft

**Vollstaendige Forschungsanalyse:**
DataIngest → Hypothesis-Test → InsightExtraction → ReportDraft

## Swarm-Sizing fuer Analysis

| Aufgabe | Swarm-Groesse | Begruendung |
|---|---|---|
| DataIngest | 1 Worker pro Datenquelle | Parallel wenn mehrere Quellen |
| InsightExtraction | 3-5 Worker | Je Analysefrage ein Worker |
| Hypothesis-Test | 1-2 Worker | Sequenziell (H0/H1 -> Test -> Interpretation) |
| ReportDraft | 1 Worker | Narrativer Fluss erfordert Sequenz |
| CompetitiveAnalysis | 3-8 Worker | Je Wettbewerber ein Worker |

## Auto-Permissions (allow_auto_mcp_install aktiviert)

- exa: Marktdaten, Branchenberichte
- firecrawl: Web-Scraping fuer Competitive (nur lesend)

**Always-Pause bei:** Daten mit PII, externe API-Schreibzugriffe, Cost-Cap 100%.

# Analysis Protocols — deepwork-entry-analyze Context

## Projekttyp-Erkennung: analysis / research / finance

**Indikatoren fuer project_type: analysis:**
- Dateien: `.csv`, `.xlsx`, `.json` Datensaetze, Jupyter Notebooks (`.ipynb`)
- Ordner: `data/`, `reports/`, `insights/`, `models/`
- Keywords in PROJECT.md: "analyse", "dashboard", "bericht", "daten", "metriken", "kpi"
- Tools: pandas, dbt, Metabase, Looker, Power BI, Grafana

**Indikatoren fuer project_type: finance:**
- Keywords: "budget", "forecast", "P&L", "cashflow", "KPI", "EBITDA"
- Dateien: Excel-Modelle, Finanzberichte (.xlsx/.pdf)
- Ordner: `models/`, `forecasts/`

**Indikatoren fuer project_type: research:**
- Keywords: "recherche", "studie", "literatur", "quellen", "synthese"
- Ordner: `sources/`, `synthesis/`, `reports/`

## Migration-Checks fuer analysis-Projekte

Fehlende Ordner (anlegen bei Migration):
- `.deepwork/research/` — Rohdaten-Dokumentation, DataIngest-Outputs
- `.deepwork/outputs/<section>/` — Analyse-Outputs je Frage
- `data/` — Falls noch nicht vorhanden
- `reports/` — Falls noch nicht vorhanden

Protokoll-Referenz: `deepwork-env-setup/references/analysis-protocols.md`

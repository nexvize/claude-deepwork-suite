# Analysis Protocols — Stub (deepwork-00-bootstrap)

Canonical source: `deepwork-env-setup/references/analysis-protocols.md`

Nicht benoetigt waehrend Bootstrap. Relevante Protokolle werden von deepwork-01-discovery oder deepwork-quick geladen, sobald `project_type: analysis`, `research` oder `finance` erkannt wurde.

Typ-spezifische Ordnerstruktur fuer analysis (wird in Step 3 angelegt):
```
.deepwork/
  research/    <- Rohdaten-Dokumentation, Schema
  outputs/     <- Analyse-Outputs je Section
data/          <- Datensaetze
reports/       <- Fertige Berichte
insights/      <- Insight-Dokumente
models/        <- Statistische Modelle / Notebooks
```

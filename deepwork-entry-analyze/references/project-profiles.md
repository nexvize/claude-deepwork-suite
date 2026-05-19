→ Vollständiges Profil-Dokument: siehe `deepwork-env-setup/references/project-profiles.md`

Dieses Dokument ist die kanonische Quelle für alle 12 Projekttyp-Profile.
Der gleiche Inhalt ist in kompakter Form unten als Schnell-Referenz verfügbar.

# Project Profiles — Schnell-Referenz (deepwork-entry-analyze)

## Projekttyp aus PROJECT.md lesen

```yaml
project_type: coding
project_type_secondary: marketing  # optional
```

## Typ-Erkennungs-Heuristiken (für automatische Typ-Erkennung)

| Datei-Signatur | Wahrscheinlicher Typ |
|---|---|
| .js/.ts/.py/.go/.rs/.java/.cs + package.json/requirements.txt | coding |
| Dominanter Markdown-Anteil + docs/ + keine Code-Dateien | content |
| .fig/.sketch + wireframes/ + components/ + design-tokens | design |
| .ipynb/.csv/.parquet + notebooks/ + data/ | analysis |
| .mp4/.mp3/.png-batch + prompts/ + storyboards/ | media |
| Forschungs-Markdown + sources/ + bibliography | research |
| Kampagnen-Markdown + copy/ + campaigns/ + briefs/ | marketing |
| Konzept-Markdown + pitches/ + stakeholders/ + roadmaps/ | concept |
| modules/ + exercises/ + assessments/ + learning-objectives | education |
| .yaml/.sh + workflows/ + configs/ + scripts/ | automation |
| contracts/ + compliance/ + case-law/ | legal |
| models/ + forecasts/ + assumptions/ + financial-data | finance |

## Migrate-Modus: Typ-spezifische Ordner-Checks

Wenn ein Projekt eine alte .deepwork/-Struktur hat aber keine typ-spezifischen Ordner:

| Erkannter Typ | Fehlende Ordner anlegen |
|---|---|
| coding | src/, tests/, docs/, scripts/ |
| research | sources/raw/, synthesis/, reports/ |
| content | drafts/v1/, published/, assets/ |
| design | wireframes/, specs/, components/ |
| media | prompts/, assets/generated/, storyboards/ |
| marketing | copy/, campaigns/, briefs/ |
| analysis | data/raw/, reports/, insights/, notebooks/ |
| concept | ideas/, roadmaps/, pitches/ |
| education | modules/, exercises/, assessments/ |
| automation | scripts/, configs/, workflows/ |
| legal | contracts/, research/, compliance/ |
| finance | models/, data/, reports/, forecasts/ |

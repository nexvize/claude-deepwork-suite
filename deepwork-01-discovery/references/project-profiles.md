# Project Profiles — Deepwork Suite v3

## Wie Skills dieses Dokument nutzen

Jeder Deepwork-Skill liest beim Start den `project_type`-Wert aus `PROJECT.md` und lädt das passende Profil aus diesem Dokument. Das Profil definiert, welche Protokolle in welcher Priorität eingesetzt werden, welche MCPs bevorzugt geroutet werden, wie groß Swarms dimensioniert werden, wie die Ordnerstruktur aussieht und was "fertig" für diesen Projekttyp bedeutet — sodass alle Skills konsistent und ohne manuelle Konfiguration auf den jeweiligen Kontext zugeschnitten agieren.

## Lesen: Projekttyp aus PROJECT.md

```yaml
# .deepwork/PROJECT.md — minimales Pflichtfeld
project_type: coding            # Primärer Typ (Pflicht)
project_type_secondary: marketing  # Optionaler Sekundärtyp
```

---

## Profil: coding

**Beschreibung:** Softwareentwicklungsprojekte jeder Größe.

### Protokolle
| Priorität | Protokoll | Wann einsetzen |
|---|---|---|
| Primär | Debug | Fehler lokalisieren |
| Primär | CodeReview | Code-Qualität prüfen |
| Primär | TDD | Features über Tests spezifizieren |
| Sekundär | Refactor | Code verbessern |
| Sekundär | Spike | Technische Unsicherheiten klären |

### MCP-Routing
1. context7, 2. filesystem, 3. github, 4. playwright, 5. sequential-thinking

### Swarm-Sizing
Single-File: 1-2 | Standard-Feature: 3-6 | Modul-Refactor: 5-8 | Große Analyse: 8-20

### Ordnerstruktur
src/, tests/, docs/, scripts/

### Verifikation
- Tests grün, Code läuft, kein Linting-Fehler, Code Review, Doku aktualisiert

---

## Profil: research
**MCP-Routing:** 1. exa, 2. firecrawl, 3. context7, 4. memory, 5. sequential-thinking
**Ordner:** sources/, sources/raw/, sources/annotated/, synthesis/, reports/

## Profil: content
**MCP-Routing:** 1. firecrawl, 2. exa, 3. memory, 4. Gamma MCP
**Ordner:** drafts/, drafts/v1/, drafts/final/, published/, assets/

## Profil: design
**MCP-Routing:** 1. Figma MCP, 2. playwright, 3. exa, 4. filesystem
**Ordner:** wireframes/, specs/, specs/components/, assets/, components/

## Profil: media
**MCP-Routing:** 1. higgsfield, 2. filesystem, 3. Figma MCP, 4. exa
**Ordner:** prompts/, assets/, assets/generated/, assets/approved/, exports/, storyboards/

## Profil: marketing
**MCP-Routing:** 1. exa, 2. firecrawl, 3. Figma MCP, 4. memory
**Ordner:** copy/, campaigns/, assets/, briefs/

## Profil: analysis
**MCP-Routing:** 1. exa, 2. firecrawl, 3. context7, 4. filesystem, 5. sequential-thinking
**Ordner:** data/, data/raw/, data/processed/, reports/, insights/, models/, notebooks/

## Profil: concept
**MCP-Routing:** 1. exa, 2. sequential-thinking, 3. memory, 4. Gamma MCP, 5. firecrawl
**Ordner:** ideas/, roadmaps/, pitches/, stakeholders/, assumptions/

## Profil: education
**MCP-Routing:** 1. context7, 2. firecrawl, 3. exa, 4. filesystem, 5. memory
**Ordner:** modules/, exercises/, assessments/, resources/

## Profil: automation
**MCP-Routing:** 1. context7, 2. filesystem, 3. github, 4. playwright, 5. exa
**Ordner:** scripts/, configs/, tests/, workflows/, docs/

## Profil: legal
**MCP-Routing:** 1. exa, 2. firecrawl, 3. filesystem, 4. memory
**Ordner:** contracts/, contracts/drafts/, research/, compliance/

## Profil: finance
**MCP-Routing:** 1. exa, 2. firecrawl, 3. context7, 4. filesystem, 5. sequential-thinking
**Ordner:** models/, data/, reports/, forecasts/, assumptions/

---

## Mischtypen

```yaml
project_type: coding
project_type_secondary: marketing
```

Primär-Typ bestimmt Ordnerstruktur, Protokolle und Swarm-Sizing. Sekundär-Typ fügt Top-3 Protokolle und Top-2 MCPs hinzu.

**Häufige Kombinationen:** coding+marketing, coding+design, research+content, concept+finance, content+marketing, analysis+finance, design+coding, education+content

> **Vollständige Profile** (inkl. Swarm-Sizing-Tabellen, Verifikations-Kriterien, Output-Konventionen): Siehe die Datei mit dem vollen Inhalt in deepwork-env-setup/references/project-profiles.md

→ Vollständiges Profil-Dokument: siehe `deepwork-env-setup/references/project-profiles.md`

Dieses Dokument ist die kanonische Quelle für alle 12 Projekttyp-Profile.
Der gleiche Inhalt ist in kompakter Form unten als Schnell-Referenz verfügbar.

# Project Profiles — Schnell-Referenz (deepwork-alt-autopilot)

## Projekttyp aus PROJECT.md lesen

```yaml
project_type: coding
project_type_secondary: marketing  # optional
```

## Protokoll-Stack nach Typ (für Autopilot-Auswahl)

| Typ | Primäre Protokolle | Key MCPs | Swarm-Default |
|---|---|---|---|
| coding | Debug, CodeReview, TDD, Refactor, Spike | context7, filesystem, github, playwright | 3–6 Worker |
| research | DocIngest, Verification, Brainstorm, Spike | exa, firecrawl, context7, memory | 5–10 Worker |
| content | Brainstorm, Outline, Draft, Edit, Proofread | firecrawl, exa, memory, Gamma | 1–4 Worker |
| design | WireframeReview, DesignAudit, UX-Heuristics, FigmaSpec | Figma MCP, playwright, exa | 3–10 Worker |
| media | PromptEngineering, Storyboard, AssetPipeline | higgsfield, filesystem, Figma MCP | 5–20 Worker |
| marketing | Brainstorm, CampaignPlan, CopyReview, Verification | exa, firecrawl, Figma MCP, memory | 4–12 Worker |
| analysis | DataIngest, InsightExtraction, Hypothesis-Test, ReportDraft | exa, firecrawl, context7, filesystem | 5–20 Worker |
| concept | Brainstorm, StructuredPlanning, Spike, Verification | exa, sequential-thinking, memory, Gamma | 3–8 Worker |
| education | Outline, ExerciseDesign, AssessmentDesign, Draft | context7, firecrawl, exa, filesystem | 3–10 Worker |
| automation | Spike, CodeReview, IntegrationTest, Debug | context7, filesystem, github, playwright | 2–8 Worker |
| legal | DocIngest, Verification, Draft, Spike | exa, firecrawl, filesystem, memory | 1–8 Worker |
| finance | DataIngest, Hypothesis, Verification, ReportDraft | exa, firecrawl, context7, filesystem | 3–8 Worker |

## Autopilot Auto-Permissions (Standard-Werte)

| Flag | Default | Wirkung |
|---|---|---|
| allow_auto_migration | true | Alte .deepwork/-Struktur ohne Pause migrieren |
| allow_auto_vault_bootstrap | true | Vault-Ordner ohne Pause anlegen |
| allow_auto_mcp_install | true | Fehlende Pflicht-MCPs auto-installieren |
| allow_auto_hooks_setup | true | Default-Hook-Set ohne Einzel-Bestätigung |
| allow_large_swarms | true | Swarm > 20 Worker ohne Pre-Confirm |
| prefer_parallel_sections | true | Unabhängige Sections auto-parallelisieren |
| skip_pre_permission_blocks | true | Pre-Permission-Klartext nur ins Journal |

## Always-Pause Triggers (nicht überschreibbar)

1. Verdikt = NO-GO
2. Killer-Risk materialisiert
3. Cost-Cap 100%
4. Verifikation 3× hintereinander fehlgeschlagen
5. Web-Safety-Pause (Login, Form, Download, Upload, Zahlung)
6. Externe Schreibzugriffe (git push, API-write, Infrastruktur)
7. Out-of-Contract-Entscheidung ohne Default
8. Major Course Correction (≥ 2 Sections invalidiert)

## Mischtypen

```yaml
project_type: coding
project_type_secondary: marketing
```

Primär-Typ bestimmt Protokoll-Stack und Swarm-Größe. Sekundär-Typ fügt Top-3 Protokolle als Optional hinzu.

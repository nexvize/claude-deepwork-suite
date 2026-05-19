# Deepwork-Suite v3 — Übersicht

Diese Suite bringt Claude Code in die bestmögliche Arbeitsumgebung — für **alle Projekttypen**, in jedem Stadium.
Neue Projekte, bestehende Projekte, einzelne Aufgaben, vollautomatisch oder kollaborativ.

---

## Welchen Modus brauchst du?

### Modus 1 — Vollständig (Neues Projekt, geführt oder kollaborativ)

```
deepwork-env-setup       ← einmalig pro Maschine (Umgebung + Auto-Discovery)
deepwork-00-bootstrap    ← Projekt starten (Typ wählen, Struktur anlegen)
deepwork-01-discovery    ← Recherche + Plan + GO/NO-GO
deepwork-02-refine       ← Plan in Sections aufteilen (typ-spezifisch)
deepwork-03-execute      ← Umsetzen + Recap + Refactor (Section für Section)
deepwork-end-report      ← Abschluss + Next Steps (typ-spezifischer Bericht)
```

**Arbeitsmodi in Bootstrap wählbar:**
- **Standard** → klassische Pipeline, Section für Section mit /clear
- **Co-Planning** → Plan gemeinsam erarbeiten, Schritt für Schritt
- **Autopilot** → direkt zu deepwork-alt-autopilot

---

### Modus 2 — Quick-Use (Einzelnes Protokoll, ohne Pipeline)

```
deepwork-quick           ← wählt dynamisch das passende Protokoll für den Projekttyp
```

**Protokolle nach Projekttyp:**

| Typ | Protokoll-Optionen |
|---|---|
| `coding` | Code Review, Debug (Self-Verification-first), Refactor, Spike, TDD, Verification |
| `research` | Document Ingest, Spike, Verification, Brainstorm |
| `content` | Brainstorm, Outline, Draft, Edit, Proofread, SEO-Optimize |
| `design` | WireframeReview, DesignAudit, UX-Heuristics, FigmaSpec, ComponentInventory |
| `media` | PromptEngineering, Storyboard, AssetInventory, VideoScript |
| `marketing` | Brainstorm, CampaignPlan, CopyReview, SEO-Optimize, Verification |
| `analysis` | DataIngest, InsightExtraction, Hypothesis-Test, ReportDraft |
| `concept` | Brainstorm, StructuredPlanning, PitchDeck, RoadmapBuild |
| `education` | LearningOutcomes, CurriculumOutline, ExerciseDesign, AssessmentDesign |
| `automation` | Spike, CodeReview, IntegrationTest, Verification |
| `legal` | Document Ingest, Verification, Draft, Spike |
| `finance` | DataIngest, Hypothesis-Test, Verification, ReportDraft |

**+ Auto-Discovery** immer verfügbar: findet fehlende Skills/MCPs/Plugins für den Projekttyp.

---

### Modus 3 — Autopilot (Vollautomatisch)

```
deepwork-alt-autopilot   ← Mega-Interview → Contract → autonome Ausführung
```

Typ-bewusst: wählt automatisch Protokolle, MCPs, Swarm-Strategien nach Projekttyp.
Einzige Pausen: NO-GO, Killer-Risiken, Cost-Cap, Web-Safety.

---

### Modus 4 — Transfer (Bestehendes Projekt einbinden)

```
deepwork-entry-analyze   ← erkennt Projekttyp automatisch + 3 Sub-Modi:
                            • Kein deepwork → Vollanalyse (3-Agent-Scan)
                            • Alte Struktur → Migration + typ-spez. Ordner ergänzen
                            • Aktives deepwork → Weiterleitung zur richtigen Phase
```

---

## Die 12 Projekttypen

| Typ | Kern-Use-Case | Primär-MCPs | Typischer Output |
|---|---|---|---|
| `coding` | Software bauen, debuggen, deployen | context7, filesystem, github | Code, Tests, Docs |
| `research` | Themen erforschen, Wissen aggregieren | exa, firecrawl, context7 | Reports, Knowledge Base |
| `content` | Texte, Artikel, Bücher, Skripte | firecrawl, exa | Texte, Artikel, Bücher |
| `design` | UI/UX, Wireframes, DesignSystem | Figma MCP, playwright | Specs, Figma-Files |
| `media` | Bilder, Videos, kreative Assets | higgsfield, filesystem | Prompts, Scripts, Assets |
| `marketing` | Kampagnen, Copy, Strategie | exa, firecrawl, Figma | Copy, Kampagnen-Docs |
| `analysis` | Daten analysieren, Reports | exa, firecrawl, context7 | Reports, Insights |
| `concept` | Konzepte, Strategien, Roadmaps | exa, sequential-thinking | Konzepte, Roadmaps, Pitches |
| `education` | Kurse, Tutorials, Lernmaterial | context7, firecrawl | Kurse, Module, Übungen |
| `automation` | Workflows, Scripts, Integrationen | filesystem, github, context7 | Workflows, Scripts |
| `legal` | Verträge, Compliance, Legal Research | exa, firecrawl | Verträge, Compliance-Docs |
| `finance` | Finanzmodelle, Prognosen, Reports | exa, firecrawl, context7 | Modelle, Reports |

**Mischtypen möglich:** `project_type: coding` + `project_type_secondary: marketing`

Vollständige Profil-Details (Protokolle, Swarm-Sizing, Ordnerstruktur, Verification-Kriterien) in `references/project-profiles.md`.

---

## Alle Skills im Überblick

| Skill | Modus | Beschreibung |
|---|---|---|
| `deepwork-env-setup` | Voraussetzung | MCPs, Plugins, Vault, Hooks prüfen + Auto-Discovery (findet fehlende Tools per GitHub/Plugin-Store-Scan) |
| `deepwork-00-bootstrap` | 1 | Projekt starten: Typ wählen (12 Typen), adaptive Ordnerstruktur, Co-Planning oder Autopilot |
| `deepwork-01-discovery` | 1 | Recherche + Plan + GO/NO-GO — Protokolle und MCPs nach Projekttyp |
| `deepwork-02-refine` | 1 | Plan → Sections (typ-spezifische Section-Definitionen: Features/Kapitel/Screens/etc.) |
| `deepwork-03-execute` | 1 | Section umsetzen: Recap + Refactor, typ-spezifische Verification |
| `deepwork-end-report` | 1 | Abschluss: typ-spezifischer Bericht (Test-Coverage für coding, Quellen-Qualität für research, etc.) |
| `deepwork-quick` | 2 | Einzelne Protokolle — dynamisch nach Projekttyp, + Auto-Discovery-Option |
| `deepwork-alt-autopilot` | 3 | Autonome Vollausführung — Typ-bewusst, wählt Protokolle und Swarm-Strategien |
| `deepwork-entry-analyze` | 4 | Bestehendes Projekt: Typ erkennen, Struktur aufbauen, in Pipeline überführen |
| `deepwork-migrate` | — | Veraltet — Redirect zu deepwork-entry-analyze |

---

## Wann welcher Einstieg?

```
Erste Einrichtung (einmalig)?
  → deepwork-env-setup

Neues Projekt (Coding / Design / Content / Marketing / ...)?
  → deepwork-00-bootstrap (wählt dann Typ + Modus)

Neues Projekt, hands-off?
  → deepwork-alt-autopilot

Bestehendes Projekt einbinden?
  → deepwork-entry-analyze

Einzelne Aufgabe ohne Pipeline?
  → deepwork-quick

Fehlende Tools finden?
  → deepwork-env-setup ODER deepwork-quick → "Auto-Discovery"
```

---

## Shared References (in allen Skills verfügbar)

### Kern-Referenzen (alle Typen)

| Datei | Inhalt |
|---|---|
| `project-profiles.md` | **NEU** — 12 Projekttypen: Protokolle, MCPs, Ordnerstruktur, Verification, Swarm-Sizing |
| `auto-discovery-protocol.md` | **NEU** — GitHub + Plugin-Store-Scan für fehlende Tools |
| `native-protocols.md` | Brainstorm, Spike, Verification, Debug, TDD, DocIngest, CodeReview, Refactor, ContextBudget, QualityGate |
| `tool-awareness.md` | Welches Tool für welche Aufgabe + MCP-Routing + Web-Safety |
| `plain-language.md` | Klartext-Pflicht: wie mit dem User kommuniziert wird |
| `swarm-sizing.md` | Wie viele parallele Helfer für welche Aufgabe |
| `user-profile.md` | Umbrella-Prinzip: aktive Advocacy, nicht stille Ausführung |
| `handoff-protocol.md` | Format und Schema von handoff.md |
| `memory-persistence.md` | Drei-Schicht-Persistenz (Dateisystem / Ruflo / MCP) |
| `model-selection.md` | Wann Opus, wann Sonnet |
| `self-reflection.md` | Internes Controlling: Goal ← Plan ← Execution |
| `decision-levels.md` | 5-Stufen-Empfehlung für alle User-Entscheidungen |

### Typ-spezifische Protokoll-Referenzen

| Datei | Für Typen | Protokolle |
|---|---|---|
| `content-protocols.md` | content, marketing, concept, education | Outline, Draft, Edit, Proofread, Translation, SEO-Optimize |
| `design-protocols.md` | design, marketing | WireframeReview, DesignAudit, UX-Heuristics, FigmaSpec, ComponentInventory, AccessibilityReview |
| `media-protocols.md` | media, marketing | PromptEngineering, StoryboardPlanning, AssetInventory, ConceptArt-Brief, VideoScript, BrandConsistency |
| `analysis-protocols.md` | analysis, research, finance | DataIngest, InsightExtraction, Hypothesis-Test, ReportDraft, DashboardSpec, CompetitiveAnalysis |
| `concept-protocols.md` | concept, research, marketing | StructuredPlanning, StakeholderMap, ScenarioAnalysis, PitchDeck, RoadmapBuild, RiskMatrix |
| `education-protocols.md` | education, concept, content | LearningOutcomes, CurriculumOutline, ExerciseDesign, AssessmentDesign, ConceptExplanation, LearnerPersona |

---

## Auto-Discovery

Die Suite sucht aktiv nach fehlenden Verbesserungen:

- **GitHub-Scan** — findet claude-code-skill Repos die deinen Workflow verbessern würden
- **Plugin-Store-Scan** — findet Ruflo-Plugins für deinen Projekttyp
- **MCP-Lücken** — vergleicht installierte MCPs mit dem Profil deines Projekttyps
- **Hook-Lücken** — prüft ob empfohlene Hooks fehlen

Ausführen: `/deepwork-env-setup` (vollständig) oder `/deepwork-quick` → Auto-Discovery

---

## Zentrale Konfiguration

Alle Pfade und Limits: `DEEPWORK-CONFIG.md`

- `DEEPWORK_VAULT_PATH` = `D:\Claude\ObsidianVault\`
- `DEEPWORK_SWARM_MAX_WORKERS` = 100
- `DEEPWORK_DEFAULT_COST_CAP_USD` = $5.00

---

## Qualitäts-Prinzipien (gelten in allen Modi und Typen)

- **Projekttyp-Awareness:** Jeder Skill liest `project_type` aus PROJECT.md und adaptiert Protokolle, MCPs, Verification-Kriterien
- **Vertical Slicing:** Jede Section = vollständiges Ergebnis (kein "Zuarbeit ohne Output")
- **Recap nach jeder Section:** Agent erklärt was gebaut/erstellt wurde — User behält Überblick
- **Context Budget:** /clear nach jeder Section (Modus 1) = Qualitätssicherung, kein Formalismus
- **Self-Verification:** Debug/Verification-Protocol beginnt mit "wie prüfe ich selbst?" — nicht nach jedem Versuch fragen
- **Refactor ist Pflicht:** Kein Section-Abschluss ohne kurzes Aufräumen
- **Auto-Discovery:** Suite sucht aktiv nach besseren Tools — nicht passiv warten bis User fragt

*Zuletzt aktualisiert: 2026-05-19 (v3 — 12 Projekttypen, Auto-Discovery, Co-Planning, Typ-adaptive Struktur)*

# Deepwork-Suite — Übersicht

Diese Suite bringt Claude Code in die bestmögliche Arbeitsumgebung — für jedes Projekt, in jedem Stadium.

---

## Welchen Modus brauchst du?

### Modus 1 — Vollständig (Neues Projekt von Null)
Beste Qualität. Geführter Prozess. Alles kontrolliert und dokumentiert.

```
deepwork-env-setup       ← einmalig pro Maschine (Umgebung einrichten)
deepwork-00-bootstrap    ← Projekt starten
deepwork-01-discovery    ← Recherche + Plan + GO/NO-GO
deepwork-02-refine       ← Plan in Schritte aufteilen
deepwork-03-execute      ← Umsetzen (eine Section, dann /clear)
deepwork-end-report      ← Abschluss + Next Steps
```

---

### Modus 2 — Quick-Use (Einzelne Aufgabe, ohne Pipeline)
Für wenn du nur eine konkrete Aufgabe erledigst — kein handoff.md nötig, kein Discovery.

```
deepwork-quick           ← Einstieg: wählt das passende Protokoll
```

**Welches Protokoll für welche Aufgabe:**
| Ich brauche... | Protokoll in native-protocols.md |
|---|---|
| Code Review | Code Review Protocol |
| Bug fixen | Debug Protocol (Self-Verification-first) |
| Technische Frage klären | Spike Protocol |
| Code aufräumen | Refactor Protocol |
| Ideen entwickeln | Brainstorm Protocol |
| Docs einlesen | Document Ingest Protocol |
| Ergebnis prüfen | Verification Protocol |

Alle Protokolle sind in `references/native-protocols.md` vollständig beschrieben und funktionieren standalone.

**Brücke zurück in Modus 1:** Nach dem Quick-Use → `/deepwork-entry-analyze` oder `/deepwork-00-bootstrap`.

---

### Modus 3 — Autopilot (Hands-Off / Alles auf einmal)
Für wenn du nicht Schritt für Schritt dabei sein willst. Ein Mega-Interview am Anfang, dann läuft alles durch.

```
deepwork-alt-autopilot   ← führt 00→01→02→03 autonom durch
```

Einzige Pausen: NO-GO-Verdikt, Killer-Risiken, Cost-Cap, oder Web-Safety. Alles andere entscheidet der Contract.

---

### Modus 4 — Transfer (Bestehendes Projekt einbinden)
Für Projekte die nicht mit deepwork erstellt wurden. Analysiert, bringt auf Standard, ermöglicht dann Modus 1.

```
deepwork-entry-analyze   ← erkennt automatisch den richtigen Sub-Modus:
                            • Kein deepwork vorhanden → Vollanalyse
                            • Alte/unvollständige Struktur → Migrate + Gap-Check
```

---

## Alle Skills im Überblick

| Skill | Modus | Beschreibung |
|---|---|---|
| `deepwork-env-setup` | Voraussetzung | Einmalig pro Maschine: MCPs, Plugins, Vault, Hooks prüfen + einrichten |
| `deepwork-00-bootstrap` | 1 | Projekt starten: Triage, Routing, Ordnerstruktur, Foundation-Dokumente |
| `deepwork-01-discovery` | 1 | Recherche + Plan + GO/NO-GO Verdikt |
| `deepwork-02-refine` | 1 | Plan → konkrete, ausführbare Sections mit Erfolgskriterien |
| `deepwork-03-execute` | 1 | Eine Section umsetzen (Vertical Slice), dann /clear |
| `deepwork-end-report` | 1 | Abschlussbericht + Next Steps |
| `deepwork-quick` | 2 | Einzelne Protokolle ohne Pipeline: Review, Debug, Spike, Refactor, Brainstorm |
| `deepwork-alt-autopilot` | 3 | Autonome Durchführung ohne /clear, kein manueller Input außer am Anfang |
| `deepwork-entry-analyze` | 4 | Bestehendes Projekt: analysieren, Struktur aufbauen, in Modus 1 überführen |

---

## Wann welcher Einstieg?

```
Erste Einrichtung (einmalig)?
  → deepwork-env-setup

Neues Projekt?
  → deepwork-00-bootstrap (dann 01 → 02 → 03 → end-report)

Neues Projekt, aber hands-off?
  → deepwork-alt-autopilot

Bestehendes Projekt einbinden?
  → deepwork-entry-analyze (erkennt auch veraltete deepwork-Strukturen)

Einzelne Aufgabe ohne Pipeline?
  → deepwork-quick
```

---

## Shared References (in allen Skills verfügbar)

Alle Skills teilen gemeinsame Referenz-Dateien im `references/`-Ordner:

| Datei | Inhalt |
|---|---|
| `native-protocols.md` | 8 vollständige Protokolle: Brainstorm, Spike, Verification, Debug, TDD, DocIngest, CodeReview, Refactor, ContextBudget, QualityGate |
| `tool-awareness.md` | Welches Tool für welche Aufgabe + Web-Research-Safety-Regel + MCP-Routing |
| `plain-language.md` | Klartext-Pflicht: wie mit dem User kommuniziert wird |
| `swarm-sizing.md` | Wie viele parallele Helfer für welche Aufgabe |
| `user-profile.md` | Umbrella-Prinzip: aktive Advocacy, nicht stille Ausführung |
| `handoff-protocol.md` | Format und Schema von handoff.md |
| `memory-persistence.md` | Drei-Schicht-Persistenz (Dateisystem / Ruflo / MCP) |
| `model-selection.md` | Wann Opus, wann Sonnet |
| `self-reflection.md` | Internes Controlling: Goal ← Plan ← Execution |
| `research-verification.md` | ≥2 unabhängige Quellen für plan-relevante Fakten |
| `documentation-standard.md` | Zwei-Schicht-Output (Raw + Synthese) |
| `token-log-protocol.md` | Kosten-Tracking-Format |
| `routing.md` | Section-Typ → Tool-Routing-Entscheidung |
| `verdict-rubric.md` | GO/GO-WITH-CUTS/NO-GO Kriterien |
| `research-substeps.md` | 4-Schritt Tellerrand-Recherche |
| `interview-rounds.md` | Fragen-Bank für Discovery-Interview |
| `decision-levels.md` | 5-Stufen-Empfehlung für alle User-Entscheidungen |

---

## Zentrale Konfiguration

Alle Pfade und Limits in einer Datei: `DEEPWORK-CONFIG.md`

Wichtige Werte: `DEEPWORK_VAULT_PATH` (Standard: `D:\Claude\ObsidianVault\`), `DEEPWORK_SWARM_MAX_WORKERS` (Standard: 100), `DEEPWORK_DEFAULT_COST_CAP_USD` (Standard: $5.00)

---

## Qualitäts-Prinzipien (gelten in allen Modi)

- **Vertical Slicing:** Jede Section = vollständiger Feature-Slice (UI + Logik + Daten), kein horizontales Layer
- **Recap nach jeder Section:** Agent erklärt was gebaut wurde — User behält Überblick
- **Context Budget:** /clear nach jeder Section (Modus 1) = Qualitätssicherung, nicht Formalismus
- **Self-Verification:** Debug-Protocol beginnt mit "wie prüfe ich ohne den User?" — nicht nach jedem Versuch fragen
- **Refactor ist Pflicht:** Kein Section-Abschluss ohne kurzes Aufräumen

*Zuletzt aktualisiert: 2026-05-19*

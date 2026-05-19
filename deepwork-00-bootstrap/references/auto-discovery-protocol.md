→ Vollständiges Auto-Discovery-Protokoll: siehe `deepwork-env-setup/references/auto-discovery-protocol.md`

# Auto-Discovery — Schnell-Referenz (deepwork-00-bootstrap)

In `deepwork-00-bootstrap` wird Auto-Discovery nach der Projekttyp-Wahl als Schnell-Scan ausgeführt.

## Wann ausführen

Nach Step 1 (Quick Triage) wenn der Projekttyp feststeht: typ-spezifischen Scan starten.

## Ablauf (kompakt)

1. Aktive MCPs aus System-Reminder oder `~/.claude.json` lesen
2. Aktive Plugins aus `~/.claude/settings.json` lesen
3. Gegen Typ-spezifische Anforderungen aus `project-profiles.md` abgleichen
4. Lücken-Block ausgeben (nur SOFORT + EMPFOHLEN, kein vollständiger GitHub-Scan)
5. Auf Bestätigung warten, dann installieren

## Typ-spezifische MCPs (Mindestanforderung)

| Typ | Mindest-MCPs |
|---|---|
| coding | context7, filesystem, github |
| research | exa, firecrawl, context7, memory |
| content | firecrawl, exa |
| design | Figma MCP, playwright |
| media | higgsfield, filesystem |
| marketing | exa, firecrawl |
| analysis | exa, context7, filesystem |
| concept | exa, sequential-thinking |
| education | context7, firecrawl |
| automation | context7, filesystem, github |
| legal | exa, firecrawl |
| finance | exa, firecrawl, context7 |

Sicherheits-Regeln: siehe vollständiges Dokument in `deepwork-env-setup/references/auto-discovery-protocol.md`

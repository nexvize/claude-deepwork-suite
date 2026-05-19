→ Vollständiges Auto-Discovery-Protokoll: siehe `deepwork-env-setup/references/auto-discovery-protocol.md`

# Auto-Discovery — Schnell-Referenz (deepwork-alt-autopilot)

Im Autopilot-Modus läuft Auto-Discovery automatisch wenn `auto_discovery_enabled: true` im Contract gesetzt ist.

## Autopilot-Verhalten

Wenn `allow_auto_mcp_install: true` im Contract:
- Schritt 1–3 automatisch ausführen
- Fehlende Pflicht-MCPs (context7, filesystem, exa, firecrawl) auto-installieren ohne Pause
- Alle anderen MCPs: trotzdem Pause + User-Bestätigung
- Alle Auto-Installationen ins Journal schreiben

Wenn `allow_auto_mcp_install: false` im Contract:
- Discovery ausführen, aber keinen Install ohne Bestätigung
- Empfehlungs-Block in Autopilot-Pause ausgeben

Always-Pause Triggers gelten auch hier (Web-Safety, externe Schreibzugriffe).

Vollständiges Dokument: `deepwork-env-setup/references/auto-discovery-protocol.md`

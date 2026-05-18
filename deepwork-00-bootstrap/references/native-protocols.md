# Native Deepwork Protocols

Alle häufig benötigten Prozesse — vollständig eigenständig, kein externer Skill-Aufruf nötig.
Jedes Protokoll hat klare Inputs, einen definierten Ablauf, und einen verifizierbaren Output.

---

## Brainstorm Protocol

**Verwenden wenn:** Idee noch vage, Richtung noch offen, Möglichkeiten müssen erst gefunden werden.

**Ablauf (15–20 Minuten, kein Tool nötig):**
1. **Ideen-Sprint:** 20 Ideen ohne Bewertung generieren — Tempo über Qualität, keine Selbstzensur
2. **Cluster:** Ideen nach Thema/Ansatz gruppieren → 3–5 Cluster entstehen
3. **Top 3 identifizieren** (nach Potenzial, nicht nach Einfachheit)
4. **Jede Top-Option auswerten:**
   - Was müsste stimmen damit es funktioniert? (Voraussetzungen)
   - Was würde es zum Scheitern bringen? (Kill-Conditions)
   - Welche Ressourcen braucht es? (Zeit, Geld, Skills)
5. **User entscheidet** via `AskUserQuestion` — alle 3 Optionen ehrlich präsentieren

**Output:** `.deepwork/research/brainstorm.md`

---

## Spike Protocol

**Verwenden wenn:** Konkrete technische oder strategische Frage vor dem Plan beantwortet werden muss.

**Ablauf:**
1. **Frage formulieren:** "Beweist oder widerlegt: [konkrete Aussage in einem Satz]"
2. **Timebox:** max 30 Minuten — dann Ergebnis, auch wenn unklar
3. **Minimal-Test:** kleinstes Experiment das die Frage direkt beantwortet
4. **Research** — MCP-Routing aus `tool-awareness.md` beachten
5. **Ergebnis:** BESTÄTIGT / WIDERLEGT / UNKLAR + Begründung + Auswirkung auf Plan

**Output:** `.deepwork/research/spike-<thema>.md`

---

## Verification Protocol

**Verwenden in deepwork-03** vor jedem "Section done" — nicht optional.

**Schritt 1:** Binary Criterion aus handoff.md lesen.
**Schritt 2:** Passenden Check ausführen (Tests → Bash; API → curl; Datei → Read; UI → Playwright)
**Schritt 3:** PASS → Section done; FAIL → Debug Protocol (max 3 Zyklen)
**Schritt 4:** Nach 3 Fehlschlägen → User-Block mit was probiert wurde und was gebraucht wird.

---

## Debug Protocol

**Verwenden wenn:** Verifikation schlägt fehl.

**Schritt 0:** Self-Verification Method festlegen ZUERST — reproduzierbarer Test der jetzt fehlschlägt.
**Zyklus (max 3):** Reproduzieren → Hypothesen bilden → Wahrscheinlichste testen → Auswerten.
**Nach 3 Zyklen:** User-Block mit Hypothesen, Tests und was gebraucht wird.

---

## Refactor Protocol

**Verwenden nach jeder Section** — nicht überspringen.
**Timebox:** max 15% der Section-Zeit.
1. Minimaler-Fix-Scan
2. Verständlichkeits-Check
3. Behavior-preserving Cleanup
4. Duplikat-Scan

---

## Context Budget Protocol

**Smart Zone:** ~0–100k Tokens. Nach ~100k Tokens → Qualität sinkt messbar.
**/clear zwischen Sections** in deepwork-03 ist aktive Qualitätssicherung.
**Warnsignale:** Agent wiederholt sich, diskutiert Entschiedenes neu, ignoriert handoff.md-Inhalte.

---

## TDD Protocol

**Reihenfolge nicht verhandelbar:** Test schreiben (Red) → Minimaler Code (Green) → Refactor → Repeat.
**Fehler:** Erst Code schreiben, dann Tests — das ist kein TDD.

---

## Document Ingest Protocol

**Verwenden wenn:** User hat existierende Research/Docs.
1. Alle Dateien lesen
2. Entscheidungen, Constraints, Lösungen, Fragen, Risiken extrahieren
3. Widersprüche markieren
4. Konsolidieren → `.deepwork/research/existing-context.md`
5. Widersprüche via AskUserQuestion klären

---

## Code Review Protocol

**Pro Datei prüfen:** Bugs → Sicherheit → Performance → Anforderungen → Lesbarkeit.
**Kritikalitäts-Stufen:** HIGH (blockiert Deploy) / MEDIUM (technische Schulden) / LOW (optional).
**Output:** `.deepwork/journal/code-review-<date>.md`

---

## Quality Gate Checklist

**Nach deepwork-00:** PROJECT.md, REQUIREMENTS.md, tool-inventory.md, decisions.md vorhanden + User hat Routing bestätigt.
**Nach deepwork-01:** SUMMARY.md, PLAN.md, VERDICT.md, handoff.md vorhanden + Kreuzverhoer durchgelaufen.
**Nach deepwork-02:** Jede Section hat binary Kriterium + Tool-Routing + ist ready-to-execute.
**Nach deepwork-03 (pro Section):** Kriterium geprüft, Journal geschrieben, handoff.md updated.
**Nach deepwork-end-report:** PROJECT-COMPLETE.md, NEXT-STEPS.md, Kreuzverhoer + Obsidian-Sync.

# Swarm-Sizing — Entscheidungs-Guide

Lies zuerst `DEEPWORK-CONFIG.md` — der dort definierte Wert `DEEPWORK_SWARM_MAX_WORKERS` ist das harte Maximum (aktuell: 100).

## Wann Swarm nutzen

Swarms sind parallele Arbeiter (Agents), die gleichzeitig an verschiedenen Teilaufgaben arbeiten. Je mehr unabhängige Teilaufgaben es gibt, desto mehr Worker machen Sinn.

Kein Swarm nötig wenn: nur 1–2 Dateien geändert werden, oder die Aufgabe schneller inline erledigt ist als ein Swarm aufgesetzt werden kann.

---

## Die 5 Stufen — dem User immer diese Auswahl zeigen

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SWARM-GRÖSSE — wie viele Helfer soll ich starten?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Direkt (inline, kein Swarm): Einzelne Datei, triviale Änderung — kein Overhead, sofort fertig
2. Schnell (2–5 Worker): Wenige unabhängige Teile, einfache Section — niedrige Kosten, schnell
⭐ 3. Standard (5–15 Worker) (empfohlen): Normale Section, gutes Preis-Leistungs-Verhältnis — moderat
4. Gründlich (15–50 Worker): Reviews, komplexe Features, Qualität hat Vorrang — höhere Kosten, bessere Tiefe
5. Maximum (50–100 Worker): Mega-Prototyp, vollständige Codebase-Überarbeitung — maximale Kosten, maximale Parallele

Mein Tipp für diese Situation: Option <N> — <konkreter Grund warum>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Stufen im Detail

**1. Direkt (inline, kein Swarm)**
- **Worker-Anzahl:** 0 (kein Swarm — inline ausführen)
- **Wann:** Einzelne Datei, triviale Änderung — Swarm-Overhead lohnt sich nicht
- **Kosten:** Minimal
- **Dauer:** Sofort

**2. Schnell (2–5 Worker)**
- **Worker-Anzahl:** `min(unabhängige Subtasks, 5)`
- **Wann:** Wenige unabhängige Teile, einfache Section, Budget-begrenzte Runs, schnelle Iterationen
- **Kosten:** Niedrig
- **Dauer:** Kurz

**⭐ 3. Standard (5–15 Worker) — Empfehlung für die meisten Aufgaben**
- **Worker-Anzahl:** `min(unabhängige Subtasks, 15)`
- **Wann:** Normale Projekt-Sections, 1–3 Dateien pro Subtask
- **Kosten:** Moderat — gutes Preis-Leistungs-Verhältnis
- **Dauer:** Mittel

**4. Gründlich (15–50 Worker)**
- **Worker-Anzahl:** `min(unabhängige Subtasks, 50)`
- **Wann:** Vollständige Codebase-Reviews, komplexe Refactorings, Sicherheits-Audits, Qualität hat Vorrang
- **Kosten:** Höher — mehr Tiefe pro Subtask
- **Dauer:** Länger — aber bessere Ergebnisse

**5. Maximum (50–100 Worker)**
- **Worker-Anzahl:** `min(unabhängige Subtasks, 100)`
- **Wann:** Mega-Prototypen, vollständige Codebase-Überarbeitungen, Enterprise-Rewrites
- **Kosten:** Hoch — maximale Parallelität
- **Dauer:** Je nach Aufgabe — maximale Abdeckung

---

## Sizing-Tabelle (Orientierung)

| Aufgabentyp | Direkt | Schnell | Standard | Gründlich | Maximum |
|---|---|---|---|---|---|
| Einzelne Datei / triviale Änderung | ✓ | — | — | — | — |
| Einfache Section (1–2 Dateien) | — | ✓ | — | — | — |
| Standard-Section (1–3 Dateien) | — | — | ✓ | — | — |
| Audit / Review ganzer Codebase | — | — | — | ✓ | — |
| Mega-Prototyp (viele Module) | — | — | — | — | ✓ |

**Absolutes Maximum:** 100 Worker (`DEEPWORK_SWARM_MAX_WORKERS`)

---

## Hard-Caps (immer einhalten)

- **80%-Warnung:** Wenn 80% des Cost-Caps erreicht → User benachrichtigen, weitermachen
- **100%-Stop:** Bei 100% Cost-Cap → sofort pausieren, User fragen
- **Default Cost-Cap:** Wenn kein Cost-Cap im Contract → `DEEPWORK_DEFAULT_COST_CAP_USD` aus DEEPWORK-CONFIG.md (aktuell: $5.00)

---

## User-Bestätigung

Im interaktiven Modus:
- Swarms mit **≥ 20 Workern** → immer 5-Stufen-Format oben zeigen, Stufe wählen lassen
- Swarms mit **< 20 Workern** → kurz ankündigen ("Ich starte X Helfer für Y"), kein Bestätigungs-Block nötig

Im Autopilot-Modus:
- `allow_large_swarms: true` im Contract → direkt starten, ins Journal schreiben
- `allow_large_swarms: false` → erst nach User fragen

---

## Worktree-Isolation

Für Swarms mit schreibenden Workern (Code-Änderungen, File-Erstellung) immer Worktree-Isolation nutzen (`ruflo-swarm:swarm` mit `isolation: worktree`). Verhindert Merge-Konflikte zwischen parallelen Workern.

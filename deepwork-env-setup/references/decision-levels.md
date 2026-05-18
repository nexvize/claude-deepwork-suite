# 5-Stufen-Entscheidungs-Empfehlung — Master-Template

Dieses Dokument definiert das Standard-Format für alle User-Entscheidungen in der deepwork-Suite. Jede Entscheidung wird immer als 5 nummerierte Optionen präsentiert, mit einer klaren ⭐-Empfehlung.

---

## Das Format

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
<ENTSCHEIDUNGS-TITEL>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. <Stufe 1 Name>: <was das bedeutet> — <Kosten/Zeit-Indikator>
2. <Stufe 2 Name>: <was das bedeutet> — <Kosten/Zeit-Indikator>
⭐ 3. <Stufe 3 Name> (empfohlen): <was das bedeutet> — <Kosten/Zeit-Indikator>
4. <Stufe 4 Name>: <was das bedeutet> — <Kosten/Zeit-Indikator>
5. <Stufe 5 Name>: <was das bedeutet> — <Kosten/Zeit-Indikator>

Mein Tipp für diese Situation: Option <N> — <konkreter Grund warum>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Regeln:**
- Immer genau 5 Optionen, nummeriert 1–5
- Das ⭐ wandert je nach Kontext — es ist nicht immer Option 3
- „Mein Tipp" gibt einen konkreten situationsabhängigen Grund, nicht eine generische Empfehlung
- Kategorienamen sind kontextabhängig — bei Bedarf anpassen (siehe „How to use" unten)

---

## Kategorie A — Swarm-Sizing

**Wann:** Bei allen Entscheidungen über Swarm-Größe und Worker-Anzahl.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SWARM-GRÖSSE — wie viele Helfer soll ich starten?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Direkt (inline, kein Swarm): Einzelne Datei, triviale Änderung — kein Overhead, sofort fertig
2. Schnell (2–5 Worker): Wenige unabhängige Teile, einfache Section — niedrige Kosten, schnell
⭐ 3. Standard (5–15 Worker) (empfohlen): Normale Section, gutes Preis-Leistungs-Verhältnis — moderat
4. Gründlich (15–50 Worker): Reviews, komplexe Features, Qualität hat Vorrang — höhere Kosten, bessere Tiefe
5. Maximum (50–100 Worker): Mega-Prototyp, vollständige Codebase-Überarbeitung — maximale Kosten, maximale Parallele

Mein Tipp für diese Situation: Option <N> — <konkreter Grund>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Stufen im Detail:**

| Stufe | Name | Worker | Wann |
|-------|------|--------|------|
| 1 | Direkt | 0 (inline) | Einzelne Datei, triviale Änderung — Swarm-Overhead nicht lohnenswert |
| 2 | Schnell | 2–5 | Wenige unabhängige Teile, einfache Section |
| 3 ⭐ | Standard | 5–15 | Normale Section — Standard-Default für die meisten Aufgaben |
| 4 | Gründlich | 15–50 | Reviews, komplexe Features, Security-Audits |
| 5 | Maximum | 50–100 | Mega-Prototyp, vollständige Codebase-Überarbeitung |

---

## Kategorie B — Recherche-Tiefe

**Wann:** In deepwork-01-discovery und deepwork-alt-autopilot bei Entscheidungen über Recherche-Tiefe.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RECHERCHE-TIEFE — wie gründlich soll ich recherchieren?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Überblick: Nur offensichtliche Quellen, 1–2 Agents — sehr schnell, minimale Kosten
2. Basis: Bekannte Alternativen prüfen, 3–5 Agents — schnell, niedrige Kosten
⭐ 3. Standard (empfohlen): Vollständige Tellerrand-Recherche, 6–10 Agents — moderat, gute Abdeckung
4. Tiefgehend: Contrary research intensiv, alle Optionen durchleuchtet, 10–20 Agents — höhere Kosten, maximale Abdeckung
5. Exhaustiv: Alles + Expert-Level Quellen, keine Abkürzungen, 20+ Agents — maximale Kosten, vollständiges Bild

Mein Tipp für diese Situation: Option <N> — <konkreter Grund>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Kategorie C — Verifikations-Rigor

**Wann:** In deepwork-03-execute bei der Section-Verifikation.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
VERIFIKATIONS-RIGOR — wie gründlich soll ich prüfen?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Minimal: Nur das binäre Kriterium prüfen — läuft es oder nicht — sehr schnell
2. Basis: Hauptfunktionen + offensichtliche Edge Cases — schnell, gute Grundabsicherung
⭐ 3. Standard (empfohlen): Alle definierten Kriterien + wichtige Edge Cases — moderat, solide Absicherung
4. Intensiv: + Performance-Check + Sicherheits-Basics + Grenzwerte — höherer Aufwand, höhere Sicherheit
5. Formal: + vollständige Test-Suite + Dokumentations-Check + Peer-Review-Level — maximaler Aufwand, production-ready

Mein Tipp für diese Situation: Option <N> — <konkreter Grund>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Kategorie D — Plan-Scope / Ambition

**Wann:** In deepwork-01-discovery, wenn entschieden wird, wie ambitioniert der Plan sein soll.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PLAN-AMBITION — wie weit soll der Plan gehen?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Kern: Nur das absolute Must-have — funktioniert, fertig — minimale Zeit und Kosten
2. Solide: Kern + wichtigste Nice-to-haves — guter Kompromiss, schnell lieferbar
⭐ 3. Vollständig (empfohlen): Kern + Nice-to-haves + polished — moderat, vollständiges Produkt
4. Erweitert: + zukünftige Skalierbarkeit + Edge Cases berücksichtigt — höherer Aufwand, zukunftssicher
5. Maximal: Alles — vollständige Vision, keine Abkürzungen, enterprise-ready — maximaler Aufwand

Mein Tipp für diese Situation: Option <N> — <konkreter Grund>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Kategorie E — Kreuzverhoer-Intensität

**Wann:** Bei allen `kreuzverhoer`-Aufrufen — wie hart der Plan stress-getestet wird.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
KREUZVERHOER-INTENSITÄT — wie schonungslos soll ich challengen?
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. Kurz: 2–3 kritische Fragen, ca. 5 Minuten — für schnelle Sanity-Checks
2. Fokussiert: Wichtigste Annahmen challengen, ca. 10 Minuten — für klare Kernrisiken
⭐ 3. Standard (empfohlen): Vollständiges Kreuzverhoer aller Kernentscheidungen — ausgewogen, gründlich
4. Intensiv: Jede Annahme, jedes Risiko, jede Alternative — für kritische Projekte
5. Schonungslos: Alles + externe Perspektive spawnen, devil's advocate maximal — für hochriskante Entscheidungen

Mein Tipp für diese Situation: Option <N> — <konkreter Grund>
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## How to Use

**Schritt 1 — Kontext erkennen:**
Welche Art von Entscheidung steht an?

| Entscheidungstyp | Kategorie |
|-----------------|-----------|
| Swarm-Größe, Worker-Anzahl | A — Swarm-Sizing |
| Recherche-Tiefe, Quellen-Breite | B — Recherche-Tiefe |
| Verifikation, Testing-Gründlichkeit | C — Verifikations-Rigor |
| Plan-Scope, Ambitionen, Was ist enthalten | D — Plan-Scope / Ambition |
| Kreuzverhoer, Stress-Test, Challenge | E — Kreuzverhoer-Intensität |
| Andere | Eigene Kategorie erstellen (siehe unten) |

**Schritt 2 — Passende Kategorie wählen:**
Nutze die Kategorienamen aus A–E wenn sie passen. Wenn keine passt: eigene 5 Stufen mit passenden Namen für den Kontext entwickeln. Das Format bleibt identisch.

**Schritt 3 — ⭐ situationsabhängig setzen:**
Die Empfehlung ist nicht immer Option 3. Wähle die Stufe, die zum aktuellen Kontext passt:
- Enge Deadlines oder Budget-Druck → Empfehlung nach unten (1 oder 2)
- Kritische Sicherheits-Features oder hochriskante Entscheidungen → Empfehlung nach oben (4 oder 5)
- Normale Situation → Empfehlung auf 3

**Schritt 4 — „Mein Tipp" konkret machen:**
Kein generischer Text. Konkreter Grund warum diese Option für *diese* Situation passt.

**Schritt 5 — User-Antwort verarbeiten:**
User antwortet mit einer Zahl (1–5) oder dem Namen der Stufe. Beide akzeptieren.

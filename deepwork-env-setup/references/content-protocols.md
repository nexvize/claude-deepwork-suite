# Content Protocols — Deepwork Suite v3

Für Projekttypen: `content`, `marketing`, `concept`, `education`

Jedes Protokoll ist eigenständig ausführbar. Empfohlene Reihenfolge: Outline → Draft → Edit → Proofread.

---

## Outline Protocol

**Zweck:** Struktur klären bevor geschrieben wird.
**Wann:** Vor jedem Schreib-Sprint.

**Ablauf:**
1. Ziel klären: Was soll der Leser denken/fühlen/tun?
2. Bestehende Quellen sichten (Read + Glob)
3. 3 alternative Strukturen generieren (A: Problem→Lösung→CTA, B: Story-first, C: Frage-getrieben)
4. Beste Struktur wählen
5. Outline ausarbeiten: Titel + H2 + 2–3 Bullets pro Abschnitt

**Output:** `.deepwork/content/outline.md`

```markdown
# Outline: <Arbeitstitel>
Datum: <ISO> | Format: <Blogartikel/Whitepaper/...>
Zielgruppe: <wer> | Kern-Botschaft: <ein Satz>

## <Abschnittstitel 1> (~<N> Wörter)
- <Was behandelt wird>
- <Welche Aussage>
- <Welches Beispiel>

## Offene Fragen (klären vor Draft)
- <Frage>: <warum unklar>
```

---

## Draft Protocol

**Zweck:** Ersten Entwurf erstellen — schnell, vollständig, ohne Perfektion.
**Wann:** Nach finalem Outline.

**Ablauf:**
1. Tone & Voice festlegen (formell/informell, Distanz/Nähe, Autorität/Peer)
2. Eröffnung schreiben: 3 alternative erste Absätze (Hook A: Statement, B: Geschichte, C: Frage)
3. Abschnitt-für-Abschnitt: fließender Text, Platzhalter für Lücken
4. Übergänge prüfen
5. Platzhalter auflösen via exa/firecrawl
6. Abschluss / CTA schreiben

**Platzhalter-Syntax:**
- `[PLACEHOLDER: <was fehlt>]`
- `[FAKT-CHECK: <Aussage die verifiziert werden muss>]`

**Output:** `.deepwork/content/draft.md`

---

## Edit Protocol

**Zweck:** Entwurf überarbeiten — Klarheit, Fluss, Konsistenz.
**Wann:** Nach Draft, vor Proofread.

**4-Pass-Edit (immer in dieser Reihenfolge):**

### Pass 1 — Struktur-Edit
- Erfüllt jeder Abschnitt genau eine Funktion?
- Gehört er an diese Stelle?
- Ist er notwendig?
- Erlaubt: Abschnitte verschieben, streichen, zusammenführen, aufteilen
- Nicht in Pass 1: Satz-Ebene, Wortwahl, Grammatik

### Pass 2 — Fluss-Edit
- Satzlängen-Variation vorhanden?
- Abschnittsübergänge logisch (kausal, nicht nur thematisch)?
- Passiv-Konstruktionen → Aktiv wo möglich
- Füllwörter streichen: "sehr", "eigentlich", "sozusagen", "quasi"

### Pass 3 — Klarheits-Edit
- Jargon erklärt?
- Abstrakte Aussagen → konkretes Beispiel ergänzen
- Pronomen-Referenzen eindeutig?
- Doppeldeutigkeiten?

### Pass 4 — Konsistenz-Edit
- Tonalität konsistent?
- Du/Sie konsistent?
- Terminologie konsistent?
- Tempus konsistent?

**Output:** `.deepwork/content/draft-edited.md`

---

## Proofread Protocol

**Zweck:** Letzte Qualitätsprüfung vor Veröffentlichung.
**Wann:** Nach Edit, vor Veröffentlichung. Keine Ausnahme.

**Schritte:**
1. Rechtschreibung & Grammatik (Tippfehler, Komma-Fehler, Subject-Verb-Agreement)
2. Fakten-Check: alle `[FAKT-CHECK]`-Marker aufgelöst? Zahlen, Daten, Namen korrekt?
3. Formatierungs-Konsistenz: Überschriften-Hierarchie, Listen-Format, Fett/Kursiv
4. CTA-Check: vorhanden, konkret, handlungsorientiert?
5. Längen-Check: Gesamt-Wortanzahl im Zielbereich? (>20% Abweichung → User entscheiden lassen)

**Output:** `.deepwork/content/final.md`

---

## Translation Protocol

**Zweck:** Inhalte äquivalent übertragen — nicht Wort-für-Wort, sondern kontextuell.
**Wann:** Für mehrsprachige Projekte nach Proofread.

**Ablauf:**
1. Quelltext analysieren: Kern-Botschaft, Stilmittel, kulturelle Referenzen, Ton
2. Zielsprachen-Kontext klären (Region/Variante, Formalitätsnorm, etablierte Fachterminologie)
3. Übersetzen (nicht Transkribieren): Abschnitt für Abschnitt, natürlich wie Muttersprachler
4. Rück-Übersetzungs-Check
5. Terminologie-Abgleich

Kulturelle Anpassungen markieren: `[KULTURELL ANGEPASST: Original war "<X>", ersetzt durch "<Y>"]`

**Output:** `.deepwork/content/translation-<sprache>.md`

---

## SEO-Optimize Protocol

**Zweck:** Text für Suchmaschinen optimieren ohne inhaltliche Qualität zu opfern.
**Wann:** Bei Web-Inhalten mit Traffic-Ziel.

**Ablauf:**
1. Keyword-Recherche (primäres + 3–5 sekundäre + Long-Tail-Keywords)
2. Keyword-Platzierung prüfen: H1, erster Absatz, mind. eine H2, Meta-Description
3. Title Tag schreiben (50–60 Zeichen, Keyword, klickwürdig)
4. Meta-Description schreiben (150–160 Zeichen, Keyword, Handlungsaufruf)
5. H1/H2/H3-Struktur: H1 einmal, Keywords in H2s, keine Hierarchie-Sprünge
6. Lesbarkeit: max. 20 Wörter Satzlänge, max. 3–4 Sätze pro Absatz
7. Interne Verlinkung: 2–5 Stellen identifizieren

**Keyword-Dichte:** 1–2%, nie erzwungen.

**Output:** `.deepwork/content/seo-meta.md`

```markdown
# SEO-Optimierung: <Titel>
Primäres Keyword: <keyword>
Title Tag (<60 Zeichen): <title>
Meta-Description (<160 Zeichen): <description>
Keyword-Dichte: <N>%
SEO-Status: OPTIMIERT / TEILWEISE / NICHT OPTIMIERT
```

---

## Review-Pass Checkliste

### Inhalt & Botschaft
- [ ] Kern-Botschaft klar: ein Satz
- [ ] Zielgruppe passend: richtiges Vorwissen
- [ ] Fakten geprüft: keine unbelegten Behauptungen
- [ ] Keine Widersprüche
- [ ] Keine ungeklärten Platzhalter

### Ton & Stil
- [ ] Ton konsistent
- [ ] Ansprache konsistent (Du/Sie)
- [ ] Terminologie konsistent
- [ ] Füllwörter entfernt
- [ ] Passiv minimiert

### Struktur & Format
- [ ] Überschriften-Hierarchie korrekt
- [ ] Absatz-Längen ok (max 5 Sätze)
- [ ] Listen-Format konsistent
- [ ] Fett/Kursiv sinnvoll

### Call-to-Action
- [ ] CTA vorhanden (wenn Format verlangt)
- [ ] CTA konkret und handlungsorientiert
- [ ] CTA auffindbar

### Länge
- [ ] Wortanzahl im Zielbereich (±20%)
- [ ] Kein wichtiges Thema fehlt
- [ ] Kein Abschnitt unnötig

### Technisch (Web-Content)
- [ ] Title-Tag (<60 Zeichen)
- [ ] Meta-Description (<160 Zeichen)
- [ ] Keyword in H1 und erstem Absatz
- [ ] Alle Links geprüft

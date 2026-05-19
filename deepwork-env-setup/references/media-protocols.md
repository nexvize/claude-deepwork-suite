# Media Protocols — Deepwork Suite v3

Für Projekttypen: `media`, `marketing`

---

## PromptEngineering Protocol

**Zweck:** Iterative Verbesserung von Bild- und Video-Prompts für generative AI-Tools
**Wann:** Vor dem ersten Generierungslauf, bei unbefriedigenden Ergebnissen, bei Stil-Entwicklung

**Ablauf:**
1. Ziel klären: Was erzeugen? Wofür verwendet?
2. Basis-Prompt strukturieren: `[Subjekt] + [Aktion] + [Setting] + [Stil] + [Licht] + [Technik]`
3. Stil-Referenzen einbauen: Künstlernamen, Epochen, Kamera-Referenzen
4. Negative Prompts: was vermeiden? (`blurry, watermark, text, extra limbs`)
5. Technische Parameter: Aspect Ratio, Style Strength, Seed, Steps
6. Variation-Matrix: 3–5 Varianten mit gezielt geänderten Parametern
7. Quality Scoring: Komposition / Stilkonsistenz / Technische Qualität / Zielerreichung (je 1–5)
8. Iteration: besten Prompt als neue Basis
9. Finalen Prompt dokumentieren

**Output-Format:**
```
## PromptEngineering: [Projektname]
Tool: [Midjourney / DALL-E / Higgsfield / SD]

### Prompt-Iterationen
Version N: Prompt | Negative | Parameter | Score | Problem

### Finaler Prompt + Stil-Tokens (für Wiederverwendung)
```

---

## StoryboardPlanning Protocol

**Zweck:** Visuelle Sequenzplanung: Shots, Übergänge, Stimmung, Pacing
**Wann:** Vor Video-Produktion, vor KI-Video-Generierung

**Ablauf:**
1. Konzept-Brief lesen: Kernbotschaft, Zielgruppe, Kanal
2. Gesamtlänge und Pacing: langsam/atmosphärisch vs. schnell/energetisch
3. Akt-Struktur: Intro/Hook, Hauptteil, Abschluss/CTA
4. Shots planen: Nummer, Beschreibung, Kameraeinstellung, Bewegung, Dauer
5. Übergänge: Cut, Dissolve, Wipe, Match Cut, Smash Cut, L-Cut/J-Cut
6. Stimmungs-Arc: emotionale Kurve über das Video
7. Audio-Notizen: Musik-Energie, Voice-Over, Sound-Effekte
8. B-Roll-Liste
9. Review: laut vorlesen, Timing messen

**Output-Format:**
```
## Storyboard: [Projektname]
Format / Länge / Pacing

### Struktur: Hook | Hauptteil | CTA

### Shot-Liste
| # | Beschreibung | Einstellung | Bewegung | Dauer | Übergang | Audio |

### Stimmungs-Arc
### B-Roll-Liste
### Musik-Referenz
```

---

## AssetInventory Protocol

**Zweck:** Bestehende Assets mit Metadaten katalogisieren, Wiederverwendungspotenzial identifizieren
**Wann:** Zu Projektbeginn, vor Produktion neuer Assets, bei Rebranding

**Ablauf:**
1. Asset-Quellen identifizieren: Figma, Google Drive, lokaler Ordner, DAM
2. Assets sammeln + sichten, Duplikate identifizieren
3. Metadaten: Dateiname, Format, Auflösung, Datum, Lizenz, Inhalt
4. Qualitätsbewertung: Auflösung ausreichend? Markenkonfom? Rechte klar?
5. Kategorisieren: Typ (Photo/Illustration/Icon/Video), Theme, Kanal-Eignung
6. Wiederverwendungspotenzial: direkt nutzbar / braucht Anpassung / neu erstellen
7. Lückenanalyse: fehlende Assets
8. Empfehlungen: Priorisierung

**Output-Format:**
```
## AssetInventory: [Projektname]

### Asset-Katalog
| ID | Dateiname | Typ | Format | Qualität | Lizenz | Status | Tags |

### Kategorie-Übersicht / Qualitätsprobleme / Wiederverwendungs-Highlights
### Fehlende Assets (Priorität)
```

---

## ConceptArt-Brief Protocol

**Zweck:** Art-Direction-Brief erstellen: Stimmung, Stil-Referenzen, Farbpalette, visuelle Sprache
**Wann:** Zu Beginn eines kreativen Projekts, vor KI-Bildgenerierung

**Ablauf:**
1. Projektkontext: Produkt/Brand, Zielgruppe, Kernbotschaft
2. Stimmung: 5–8 Adjektive (z.B. "warm, geerdet, mutig, zeitlos")
3. Visuelle Referenzen: mind. 5 mit Begründung was übernommen werden soll
4. Stilsprache: Fotografie/Illustration/3D? Realismus/Abstraktion?
5. Farbpalette: Primär/Sekundär/Akzent mit Hex-Werten + emotionaler Begründung
6. Typografie-Richtung: Serif/Serifenlos, Referenz-Schriften
7. Kompositionsprinzipien: Zentralperspektive, Whitespace, Nahaufnahmen?
8. Verbote: Anti-Patterns für dieses Projekt

**Output-Format:**
```
## ConceptArt Brief: [Projektname]

### Essence / Stimmungs-Adjektive / Visuelle Referenzen / Stilsprache
### Farbpalette: | Rolle | Name | Hex | Emotion |
### Typografie / Kompositionsprinzipien / Anti-Patterns
```

---

## VideoScript Protocol

**Zweck:** Video strukturieren: Hook, Body, CTA, Speaker Notes, B-Roll-Callouts
**Wann:** Vor Video-Aufnahme, vor KI-Video-Generierung

**Ablauf:**
1. Format + Länge klären: YouTube (8–15min), Short/Reel (15–60s), Ad (6/15/30s)
2. Ziel + Kernbotschaft: was soll Zuschauer wissen/fühlen/tun?
3. Hook schreiben (erste 3–15s): Frage / Statement / visueller Hook / Problem
4. Body: max. 3 Hauptpunkte. Pro Punkt: Aussage → Beweis → Takeaway
5. Übergänge: Bridge-Sätze zwischen Punkten
6. CTA: eine konkrete Aktion, klar und direkt
7. Speaker Notes: Tonfall, Energie, Pausen, Betonungen
8. B-Roll-Callouts: wo Sprecher durch B-Roll ergänzt wird
9. Script laut vorlesen, Timing messen

**Output-Format:**
```
## VideoScript: [Titel]
Format | Länge | Ziel

### HOOK (0–Xs)
[VISUAL] [B-ROLL]
SPRECHER: "..."
[Speaker Note]

### BODY: Punkt 1/2/3
### CTA
### B-Roll Shotlist / Timing-Check
```

---

## BrandConsistency Protocol

**Zweck:** Media-Assets gegen Brand Guidelines prüfen
**Wann:** Vor Veröffentlichung, bei Review externer Assets

**Ablauf:**
1. Brand Guidelines referenzieren (oder aus bestehendem Material ableiten)
2. Logo-Verwendung: korrekte Version, Mindestabstände, keine Verzerrung
3. Farbpalette: verwendete Farben gegen Brand-Farben abgleichen
4. Typografie: korrekte Schriften und Gewichtungen
5. Tonalität: Brand Voice eingehalten?
6. Bildsprache: Stil, Farb-Grading, Komposition konsistent?
7. Kanal-Spezifika: korrektes Format/Ratio, Schriften für Mobile groß genug?
8. Issues: Blocker (nicht publizieren) vs. Minor (nachbessern)

**Output-Format:**
```
## BrandConsistency Review: [Asset / Kampagne]

### Ergebnisse
| Bereich | Status | Details |

### Blocker / Minor / Freigabe
```

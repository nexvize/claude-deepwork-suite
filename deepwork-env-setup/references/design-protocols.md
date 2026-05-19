# Design Protocols — Deepwork Suite v3

Für Projekttypen: `design`, `marketing`

---

## WireframeReview Protocol

**Zweck:** UI-Struktur gegen Nutzerziele und Navigationslogik evaluieren
**Wann:** Nach Erstellung erster Wireframes, vor visueller Ausarbeitung

**Ablauf:**
1. Ziele klären: Nutzerziel je Screen, primäre + sekundäre Aktion, erwartetes Ergebnis
2. Navigationspfade tracen: Einstiegspunkte, Flows von Anfang bis Ziel, Dead-ends markieren
3. Informationshierarchie: Wichtigstes visuell prominent? F-Pattern / Z-Pattern?
4. CTA-Platzierung: Primäre Aktionen erkennbar + erreichbar (Thumb Zone Mobile)?
5. Konsistenzcheck: Gleiche Aktionen = gleiche Platzierung auf allen Screens?
6. Lückenanalyse: Fehlende User Stories, Edge-Cases (leere States, Fehler, Loading)?
7. Priorisierung: Blocker / Major / Minor

**Output-Format:**
```
## WireframeReview: [Projektname]

### Screen-Übersicht
| Screen | Primäres Ziel | Status | Issues |

### Navigationspfade
- [Flow]: Screen A → B → C ✓ / ✗ (Problem)

### Issues: Blocker / Major / Minor

### Fehlende Screens / States
```

---

## DesignAudit Protocol

**Zweck:** Konsistenzcheck über alle Komponenten — Farben, Abstände, Typografie, Zustände
**Wann:** Vor Entwicklungsübergabe, nach größeren Design-Iterationen

**Ablauf:**
1. Inventar: alle Screens/Frames + Komponenten auflisten
2. Farb-Audit: verwendete Farben gegen Design-Token prüfen
3. Typografie-Audit: Textstile erfassen, mit System vergleichen
4. Spacing-Audit: Abstände prüfen (4px/8px-Grid?)
5. Komponenten-Audit: Duplikate, detached instances, Overrides
6. Zustands-Audit: Default, Hover, Active, Disabled, Focus, Error, Loading vorhanden?
7. Responsive Audit: Verhalten auf Breakpoints
8. Bericht strukturieren: Findings nach Kategorie, Severity

**Output-Format:**
```
## DesignAudit: [Projektname]

### Farben / Typografie / Spacing / Komponenten / Zustände / Responsive
[Findings pro Kategorie]

### Summary: Kritisch X / Wichtig Y / Minor Z
```

---

## UX-Heuristics Protocol

**Zweck:** Design gegen Nielsens 10 Usability-Heuristiken evaluieren
**Wann:** Bei Design-Reviews, vor Usability-Tests

**Ablauf:**
1. Scope definieren
2. Jeden Screen systematisch durchgehen — alle 10 Heuristiken
3. Severity Rating: 0 (kein Problem) bis 4 (Usability-Katastrophe)
4. Evidence dokumentieren
5. Empfehlungen formulieren
6. Priorisierung: Severity × Aufwand

**Die 10 Heuristiken:**
1. Sichtbarkeit des Systemstatus
2. Übereinstimmung System/reale Welt
3. Nutzerkontrolle & Freiheit
4. Konsistenz & Standards
5. Fehlervermeidung
6. Wiedererkennung statt Erinnerung
7. Flexibilität & Effizienz
8. Ästhetisches & minimalistisches Design
9. Fehlererkennung & -behebung
10. Hilfe & Dokumentation

**Output-Format:**
```
## UX-Heuristics: [Projektname]

| # | Heuristik | Screen | Beschreibung | Severity | Empfehlung |

### Top-Prioritäten / Gesamtbewertung
```

---

## FigmaSpec Protocol

**Zweck:** Figma-Design in entwicklerfertige Spezifikation übersetzen
**Wann:** Vor Übergabe an Entwicklung, bei Komponenten-Implementierung

**Ablauf:**
1. Komponenten-Scope klären
2. Maße und Abstände dokumentieren (exakte Pixel oder Token-Referenzen)
3. Farben und Typografie als Tokens (nicht Hex, sondern `$color-primary-500`)
4. Asset-Export definieren: Format, Auflösung, Pfad, Namenskonvention
5. Interaktionen: Hover/Focus/Active-States, Transition (Duration, Easing)
6. Responsive Verhalten: Breakpoints, Flex/Grid-Logik
7. Sonderfälle: Empty/Loading/Error States, Max/Min Content-Längen

**Output-Format:**
```
## FigmaSpec: [Komponentenname]

### Maße / Farben / Typografie / States / Assets / Responsive / Edge Cases
```

---

## ComponentInventory Protocol

**Zweck:** Alle UI-Komponenten mit Varianten, Zuständen und Verwendungsregeln katalogisieren
**Wann:** Beim Aufbau eines Design Systems, vor Refactoring

**Ablauf:**
1. Alle Komponenten sammeln (Figma + Code-Repo)
2. Kategorisieren: Atoms / Molecules / Organisms / Templates
3. Varianten je Komponente dokumentieren
4. Zustände je Variante: Default/Hover/Focus/Active/Disabled/Loading/Error/Success
5. Verwendungsregeln: wann welche Variante, Anti-Patterns
6. Abhängigkeiten
7. Status: Fertig / In Progress / Deprecated / Fehlend

**Output-Format:**
```
## ComponentInventory: [Projektname] | Stand: YYYY-MM-DD

#### Atoms / Molecules / Organisms
[Komponente: Varianten, States, Verwendung, Status, Figma+Code-Links]

### Fehlende / Deprecated
### Zusammenfassung: Total X / Fertig Y / In Progress Z
```

---

## AccessibilityReview Protocol

**Zweck:** WCAG 2.1 AA Compliance-Check für Design und Implementierung
**Wann:** Vor Entwicklungsübergabe, bei Audit bestehender Interfaces

**Ablauf:**
1. Scope festlegen
2. Farbkontrast prüfen: Text 4.5:1 (normal), 3:1 (groß/bold); UI-Komponenten 3:1
3. Tastaturbedienbarkeit: Tab-Reihenfolge, Focus-Indicator sichtbar?
4. Screenreader: Alt-Texte, Aria-Labels für Icon-Buttons, Formular-Labels
5. Touch-Target-Größen: min. 44×44px
6. Fehler-Identifikation: nicht nur durch Farbe (auch Icon + Text)
7. Formulare: Labels sichtbar, Fehler klar beschrieben?
8. Animation: `prefers-reduced-motion` berücksichtigt?
9. Automatisierte Tests empfehlen: axe-core, Lighthouse, NVDA/VoiceOver

**Output-Format:**
```
## AccessibilityReview: [Projektname] | WCAG 2.1 AA

### Kontrast-Tabelle / Tastatur / Screenreader / Touch Targets / Formulare
### WCAG-Issues: Kriterium | Issue | Severity | Komponente
### Empfehlungen / Test-Tools
### Freigabe: [ ] Freigegeben [ ] Änderungen nötig
```

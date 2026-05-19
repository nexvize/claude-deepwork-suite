# Analysis Protocols - Deepwork Suite v3

Fuer Projekttypen: analysis, research, finance

---

## DataIngest Protocol

**Zweck:** Rohdaten / CSVs / Reports lesen, strukturieren, Datenqualitaetsprobleme identifizieren, Datenmodell aufbauen
**Wann einsetzen:** Zu Beginn jeder Analyse, bevor Insights extrahiert werden, bei Uebernahme fremder Datensaetze

### Ablauf

1. **Datenquellen inventarisieren** - Welche Dateien/Quellen liegen vor? Format (CSV, XLSX, JSON, SQL-Dump, API, PDF)? Groesse? Zeitraum?
2. **Erste Sichtung** - Erste und letzte Zeilen anschauen. Spalten/Felder identifizieren. Grobe Struktur verstehen.
3. **Schema dokumentieren** - Fuer jede Spalte: Name, Datentyp (String/Numeric/Date/Boolean), Beschreibung, Wertebereich.
4. **Datenqualitaet pruefen:**
   - Fehlende Werte: Welche Spalten? Wie viel Prozent fehlt? Zufaellig oder systematisch?
   - Duplikate: Gibt es doppelte Zeilen oder IDs?
   - Inkonsistente Formate: Datumsformate gemischt? Zahlen mit/ohne Komma? Schreibweise inkonsistent?
   - Ausreisser: Extrem hohe/niedrige Werte - Datenfehler oder real?
   - Encoding-Probleme: Sonderzeichen korrekt dargestellt?
5. **Datenmodell aufbauen** - Beziehungen zwischen Tabellen/Entitaeten. Primaer- und Fremdschluessel. ER-Skizze.
6. **Vollstaendigkeit bewerten** - Reichen die Daten um die Analysefragen zu beantworten? Was fehlt?
7. **Preprocessing-Plan** - Welche Bereinigungen / Transformationen sind noetig bevor die Analyse beginnt?

### Output-Format

    ## DataIngest: [Projektname / Datensatz]
    Datum: YYYY-MM-DD | Datenstand: [Zeitraum]

    Datenquellen:
    Datei            | Format | Groesse       | Zeitraum     | Beschreibung
    sales_2024.csv   | CSV    | 45.000 Zeilen | Jan-Dez 2024 | Verkaufsdaten
    customers.xlsx   | XLSX   | 3.200 Zeilen  | aktuell      | Kundenstamm

    Schema (sales_2024.csv):
    Spalte       | Typ     | Beispiel   | Beschreibung
    order_id     | Integer | 100234     | Eindeutige Bestell-ID
    date         | Date    | 2024-03-15 | Bestelldatum
    revenue      | Float   | 249.90     | Nettoumsatz EUR
    customer_id  | Integer | 5521       | FK -> customers

    Datenqualitaet:
    Problem         | Spalte      | Ausmass   | Schwere | Handlung
    Fehlende Werte  | customer_id | 3.2%      | Mittel  | Imputation / Ausschluss
    Duplikate       | order_id    | 12 Zeilen | Hoch    | Deduplizieren
    Format-Mix      | date        | ca. 8%    | Mittel  | ISO 8601 normalisieren
    Ausreisser      | revenue     | 3 Zeilen  | Pruefen | Manuell verifizieren

    Datenmodell:
    customers (customer_id PK)
      -> orders (order_id PK, customer_id FK)
           -> order_items (item_id PK, order_id FK, product_id FK)

    Vollstaendigkeit:
    - "Umsatz nach Region": FEHLT - region-Spalte nicht vorhanden (via PLZ ableitbar)
    - "Churn-Rate": OK - alle benoetigten Felder vorhanden

    Preprocessing-Schritte:
    1. Duplikate in order_id entfernen
    2. Datumsformat normalisieren auf ISO 8601
    3. PLZ -> Region Mapping ergaenzen
    4. Ausreisser >10.000 EUR manuell verifizieren

---

## InsightExtraction Protocol

**Zweck:** Muster, Anomalien und Key-Driver aus strukturierten Daten herausarbeiten
**Wann einsetzen:** Nach DataIngest, bei explorativer Datenanalyse, bevor ein Report oder Dashboard erstellt wird

### Ablauf

1. **Analysefragen priorisieren** - Welche Fragen sollen beantwortet werden? Reihenfolge nach Business-Prioritaet.
2. **Deskriptive Statistik** - Min, Max, Mean, Median, Std. Dev. fuer alle numerischen Spalten. Verteilungen pruefen.
3. **Zeitliche Trends** - Entwicklung ueber Zeit: Wachstum, Saisonalitaet, Wendepunkte, Beschleunigung/Verlangsamung.
4. **Segmentvergleiche** - Metriken nach Kategorien aufteilen (Region, Produkt, Kundentyp). Wer performed besser/schlechter?
5. **Korrelationen suchen** - Welche Variablen bewegen sich zusammen? Wichtig: Korrelation ist keine Kausalitaet.
6. **Anomalien identifizieren** - Datenpunkte die vom Trend abweichen. Zeitraeume mit unerwarteten Spruengen.
7. **Key-Driver analysieren** - Was erklaert den groessten Teil der Variation in der Zielmetrik? Pareto-Analyse anwenden.
8. **Insights formulieren** - Jeder Insight: Beobachtung + Quantifizierung + Implikation + Konfidenz.
9. **Visualisierungs-Empfehlung** - Welcher Chart-Typ eignet sich fuer welchen Insight?

### Output-Format

    ## InsightExtraction: [Projektname]
    Analysiert: YYYY-MM-DD | Datenbasis: [Quelle + Zeitraum]

    Key Insights:

    Insight 1: [Kurztitel]
      Beobachtung:    Umsatz Q4 2024 lag 34% ueber Q4 2023
      Quantifizierung: 2,1M EUR vs. 1,57M EUR
      Treiber:        Produkt X macht 61% des Zuwachses aus
      Implikation:    Wachstum stark produktabhaengig - Klumpenrisiko beachten
      Konfidenz:      Hoch (vollstaendige Daten, klarer Trend)
      Chart:          Gruppiertes Balkendiagramm Q4 YoY

    Anomalien:
    Datum      | Metrik       | Wert | Erwartet    | Moegliche Erklaerung
    2024-07-15 | Bestellungen | -82% | ca. 500/Tag | Systemausfall? Feiertag?

    Segment-Analyse (Umsatz nach Region):
    Region | Umsatz   | Anteil | YoY
    DE     | 1,8M EUR | 62%    | +41%
    AT     | 0,6M EUR | 21%    | +12%
    CH     | 0,5M EUR | 17%    | +28%

    Korrelationen:
    - Marketing-Spend <-> Neukunden: r=0.78 (stark positiv)
    - Preis <-> Conversion: r=-0.62 (erwartet, negativ)

    Offene Fragen:
    - Warum sinkt Retention in AT trotz Umsatzwachstum?
    - Ist Q4-Boost reproduzierbar oder einmaliger Effekt?

---

## Hypothesis-Test Protocol

**Zweck:** Hypothese formulieren, Test definieren, ausfuehren, Schluss ziehen, Konfidenz-Level dokumentieren
**Wann einsetzen:** Bei datengetriebenen Entscheidungen, bei A/B-Test-Auswertung, bei Kausalitaetsfragen in Analysen

### Ablauf

1. **Hypothese klar formulieren** - Null-Hypothese (H0): kein Effekt. Alternativ-Hypothese (H1): vermuteter Effekt. So praezise und messbar wie moeglich.
2. **Test-Design festlegen** - Welche Daten werden genutzt? Welcher statistische Test ist geeignet? (t-Test, Chi-Quadrat, ANOVA, Mann-Whitney, etc.)
3. **Signifikanz-Level festlegen** - Standard: alpha = 0.05. Bei business-kritischen Entscheidungen: alpha = 0.01.
4. **Stichprobengroesse pruefen** - Ist die Stichprobe gross genug fuer statistisch valide Aussagen? Power-Analyse wenn noetig.
5. **Test ausfuehren** - Test-Statistik und p-Wert berechnen. Effektgroesse berechnen (Cohen's d, r, eta-squared).
6. **Ergebnis interpretieren** - p < alpha: H0 ablehnen. p >= alpha: H0 nicht ablehnen (ungleich H0 bestaetigen). Praktische Signifikanz separat bewerten.
7. **Konfidenzintervall berechnen** - Bandbreite des wahren Effekts angeben.
8. **Limitationen dokumentieren** - Annahmen, Confounder, Stichproben-Bias.
9. **Business-Empfehlung ableiten** - Was bedeutet das Ergebnis fuer die konkrete Entscheidung?

### Output-Format

    ## Hypothesis-Test: [Fragestellung]
    Datum: YYYY-MM-DD

    Hypothesen:
      H0: [Kein Effekt / kein Unterschied - praezise formuliert]
      H1: [Vermuteter Effekt / Richtung - praezise formuliert]

    Test-Design:
      Typ:          [t-Test / Chi-Quadrat / Mann-Whitney / ...]
      Datenbasis:   [Beschreibung]
      Stichprobe:   n1=X, n2=Y
      Signifikanz:  alpha = 0.05
      Power (Ziel): 0.80

    Ergebnis:
      Test-Statistik: t = 2.34
      p-Wert:         0.021
      Effektgroesse:  Cohens d = 0.41 (mittlerer Effekt)
      95%-KI:         [0.8%, 12.4%]

    Interpretation:
      p (0.021) < alpha (0.05) -> H0 wird abgelehnt.
      Statistisch signifikante Evidenz fuer H1 vorhanden.
      Effektgroesse: mittel - praktisch relevant.

    Limitationen:
      - Stichprobe nicht vollstaendig randomisiert
      - Saisonale Effekte nicht kontrolliert
      - Confounder: Marketing-Kampagne lief parallel

    Business-Empfehlung:
      [Konkrete Entscheidungsempfehlung basierend auf Ergebnis und Kontext]
      Konfidenz-Level: Hoch / Mittel / Niedrig

---

## ReportDraft Protocol

**Zweck:** Strukturierten Bericht schreiben - Executive Summary, Findings, Empfehlungen, Appendix
**Wann einsetzen:** Nach abgeschlossener Analyse, bei Ergebnispraesentation an Stakeholder, bei regelmaessigen Berichten (Monthly/Quarterly)

### Ablauf

1. **Zielgruppe und Zweck klaeren** - Wer liest den Report? CEO will Executive Summary, Analyst will Details, Board will Empfehlungen. Welche Entscheidung soll der Report ermoeglichen?
2. **Executive Summary zuerst schreiben** - 3-5 Saetze: Kontext, wichtigste Erkenntnis, wichtigste Empfehlung. Kein Fachjargon. Auch ohne den Rest des Reports verstaendlich.
3. **Findings strukturieren** - Jedes Finding hat eine Headline als vollstaendige Aussage (nicht nur das Thema), Evidenz, Kontext/Vergleich und eine visuelle Unterstuetzung.
4. **Recommendations formulieren** - Jede Empfehlung beantwortet: Was tun? Warum? Bis wann? Wer ist verantwortlich? Erwarteter Impact?
5. **Visualisierungen einplanen** - Richtigen Chart-Typ waehlen: Vergleich = Bar; Trend = Line; Anteil = Donut; Verteilung = Histogram.
6. **Appendix anlegen** - Methodologie, Datenquellen-Uebersicht, Glossar, weiterfuehrende Tabellen.
7. **Sprache pruefen** - Aktive Verben statt Passiv. Keine Floskeln. Zahlen immer konkret nennen.
8. **Review-Runde** - Ist jede Empfehlung durch ein Finding belegt? Fehlt Kontext fuer Nicht-Experten?

### Output-Format

    ## Report: [Titel]
    Erstellt: YYYY-MM-DD | Fuer: [Zielgruppe]
    Analysezeitraum: [Von - Bis]

    ---

    Executive Summary
    [3-5 Saetze: Kontext + wichtigste Erkenntnis + wichtigste Empfehlung.
    Kein Jargon. Auch ohne den Rest verstaendlich.]

    ---

    Findings

    1. [Vollstaendige Aussage als Headline - nicht nur Thema]
       [Erlaeuterung. Quantifizierung. Kontext/Vergleich.]
       Visualisierung: [Chart-Typ und Datenbeschreibung]

    2. [...]

    ---

    Empfehlungen:
    Prioritaet | Empfehlung | Begruendung  | Owner | Deadline | Impact
    1          | ...        | Finding #1   | CEO   | Q1 2025  | Hoch
    2          | ...        |              |       |          | Mittel

    ---

    Appendix

    A: Methodik
       [Wie wurde die Analyse durchgefuehrt? Tools, Datenquellen, Annahmen]

    B: Datenquellen
       Quelle | Format | Zeitraum | Qualitaetsbewertung

    C: Glossar
       [Fachbegriffe verstaendlich erklaert]

    D: Detailtabellen
       [Ergaenzende Daten die im Hauptteil zu viel Platz beanspruchen]

---

## DashboardSpec Protocol

**Zweck:** Daten-Dashboard spezifizieren - Metriken, Charts, Filter, Zielgruppe, Refresh-Rate
**Wann einsetzen:** Vor Dashboard-Entwicklung, bei Anforderungserhebung fuer BI-Tools (Metabase, Looker, Power BI, Grafana), bei Redesign bestehender Dashboards

### Ablauf

1. **Zielgruppe und Use Case** - Wer nutzt das Dashboard? Wie oft? Welche konkreten Entscheidungen werden damit getroffen?
2. **Key Metrics definieren** - Welche 5-7 Metriken sind die wichtigsten? North Star Metric festlegen. Lagging vs. Leading Indicators trennen.
3. **Visualisierungen planen** - Pro Metrik: Welcher Chart-Typ? Welcher Zeitraum? Vergleich zu was (Vormonat, Ziel, Vorjahr, Benchmark)?
4. **Filter und Drill-downs** - Welche Filterdimensionen braucht die Zielgruppe? Welche Drill-down-Pfade sind sinnvoll?
5. **Layout strukturieren** - KPI-Tiles oben (Ueberblick), Details unten (Kontext). Logische Gruppierung nach Fragestellungen.
6. **Datenquellen verknuepfen** - Woher kommen die Daten? Aggregationslogik definieren. Notwendige Joins beschreiben.
7. **Refresh-Rate festlegen** - Real-time / Stuendlich / Taeglich / Woechentlich - abhaengig von Use Case und Kosten.
8. **Alerts definieren** - Bei welchen Schwellenwerten werden Benachrichtigungen ausgeloest? An wen? Ueber welchen Kanal?

### Output-Format

    ## DashboardSpec: [Dashboard-Name]
    Zielgruppe: [Rolle / Team]
    Use Case:   [Welche Entscheidungen werden damit getroffen]
    Tool:       [Metabase / Looker / Power BI / Grafana]

    Key Metrics:
    # | Metrik     | Definition                  | Quelle  | Aggregation   | Ziel     | Alert
    1 | MRR        | Monthly Recurring Revenue   | Stripe  | Summe monatl  | >50k EUR | <40k EUR
    2 | Churn Rate | Cancelled / Start-of-Month  | CRM     | %, monatlich  | <3%      | >5%
    3 | CAC        | Ads-Kosten / Neukunden      | Ads+CRM | EUR pro Kunde | <200 EUR | >350 EUR

    Layout:

      Sektion 1: Performance-Ueberblick (oben, immer sichtbar)
        - KPI-Tile: MRR - aktueller Monat + Delta zu Vormonat + Delta zu Ziel
        - KPI-Tile: Churn Rate - aktuell + Trend-Pfeil
        - KPI-Tile: Neue Kunden - aktueller Monat

      Sektion 2: Trends (Mitte)
        - Line Chart: MRR letzte 12 Monate mit Ziel-Linie
        - Grouped Bar: Neue vs. Verlorene Kunden pro Monat

      Sektion 3: Breakdown (unten)
        - Donut: MRR nach Produktkategorie
        - Tabelle: Top-10 Kunden nach Umsatz (sortierbar)

    Filter:
      - Zeitraum: 30 / 90 / 365 Tage, benutzerdefiniert
      - Region: DE / AT / CH / Alle (Multiselect)
      - Produktlinie: Multiselect
      - Segment: SMB / Mid-Market / Enterprise

    Datenquellen:
      - Stripe API       -> MRR, Churn, Neue Kunden
      - PostgreSQL (CRM) -> Kundendaten, Segmentierung
      - Join: stripe_customer_id = crm.stripe_id

    Technisch:
      - Refresh: Taeglich 06:00 Uhr (Batch)
      - Cache:   1 Stunde fuer interaktive Filter
      - Alerts:  MRR <40k EUR -> Slack #finance | Churn >5% -> E-Mail CEO+CFO

    Zugriff:
      - Lesen:      Sales, Finance, Management
      - Bearbeiten: Data-Team
      - Sensibel:   Nur Finance + Management

---

## CompetitiveAnalysis Protocol

**Zweck:** Strukturierte Wettbewerbsanalyse und Positionierungsmatrix erstellen
**Wann einsetzen:** Bei Markteintritt, vor Produkt-Repositionierung, bei Strategie-Reviews, bei Pitch-Vorbereitung

### Ablauf

1. **Wettbewerber identifizieren** - Direkte (gleiches Produkt, gleiche Zielgruppe), indirekte (Alternativloesung), potenzielle (neue Marktteilnehmer). Mind. 5-8 Wettbewerber.
2. **Analyse-Dimensionen festlegen** - Welche Kriterien sind fuer die Positionierung entscheidend? (Preis, Features, Zielgruppe, Vertriebskanal, Markenwahrnehmung, Technologie)
3. **Daten erheben** - Websites, Pricing-Seiten, G2/Capterra-Reviews, LinkedIn (Teamgroesse), Crunchbase (Funding), App Stores, Stellenanzeigen als Strategie-Indikator.
4. **Feature-Matrix erstellen** - Alle Wettbewerber vs. alle Schluessel-Features. Wer hat was, wer nicht?
5. **Pricing-Analyse** - Preismodelle vergleichen (Subscription / Usage-based / One-time / Freemium). Preis-Leistungs-Positionierung einordnen.
6. **Staerken und Schwaechen** - Mindestens 3 Staerken und 3 Schwaechen je Anbieter, aus Kundenperspektive formuliert.
7. **Positionierungsmatrix** - 2 wichtigste Differenzierungsdimensionen als Achsen. Jeden Wettbewerber einordnen. Weissen Fleck identifizieren.
8. **Eigene Position ableiten** - Wo stehen wir heute? Wo in 12 Monaten? Was ist die Differenzierungsstrategie?
9. **Strategische Implikationen formulieren** - Konkrete Handlungsempfehlungen aus der Analyse.

### Output-Format

    ## CompetitiveAnalysis: [Markt / Produktkategorie]
    Datum: YYYY-MM-DD | Scope: [Geografie / Segment]

    Wettbewerber-Ueberblick:
    Unternehmen  | Gegr. | HQ     | Funding  | Kunden   | Pricing
    Competitor A | 2018  | Berlin | 12M EUR  | ca. 500  | 49-299 EUR/mo
    Competitor B | 2020  | Remote | Bootstrap| ca. 200  | 79 USD/mo flat
    Wir          | 2021  | Wien   | 2M EUR   | 87       | 99-249 EUR/mo

    Feature-Matrix:
    Feature               | Wir | Comp A    | Comp B | Comp C
    API-Zugang            | Ja  | Ja        | Nein   | Ja
    DSGVO-konform         | Ja  | Teilweise | Ja     | Nein
    Mobile App            | Nein| Ja        | Ja     | Nein
    Deutsch lokalisiert   | Ja  | Nein      | Nein   | Ja
    SSO / SAML            | Nein| Ja        | Nein   | Ja

    Staerken und Schwaechen:
      Competitor A:
        Staerken:  Enterprise-Sales-Team, Markenbekanntheit, Feature-Tiefe
        Schwaechen: Hoher Preis, komplexes Onboarding, schwacher Support

      Competitor B:
        Staerken:  Einfache Bedienung, guenstiger Preis, schnelles Setup
        Schwaechen: Kein API, keine DSGVO, keine Skalierung fuer Teams

    Positionierungsmatrix:
      Achse X: Preis (Guenstig -> Teuer)
      Achse Y: Zielgruppe (SMB/Einfach -> Enterprise/Komplex)

      Einordnung:
        Comp A: Teuer + Enterprise
        Comp B: Guenstig + SMB
        Comp C: Teuer + Enterprise
        Wir:    Mittelpreis + Mid-Market  [freier Raum - differenzierbar]

    Unsere Differenzierung:
      Staerker als alle: DSGVO + vollstaendige Deutsche Lokalisierung
      Aufzuholen:        Mobile App (Comp A + B haben es)
      Zu vermeiden:      Enterprise-Komplexitaets-Falle

    Strategische Implikationen:
      1. DACH-Markt als defensiven Moat ausbauen - DSGVO als Kaufargument kommunizieren
      2. Mobile App in H2-Roadmap - Wettbewerbsparitaet herstellen
      3. Pricing auf 99-249 EUR/mo halten - klar zwischen Comp B und Comp A positioniert
      4. Mid-Market (20-200 MA) als Fokus - Comp A zu teuer, Comp B zu simpel

    Monitoring:
      - Quartalsweise aktualisieren
      - Quellen: G2, Crunchbase, LinkedIn, Pricing-Seiten, Stellenanzeigen

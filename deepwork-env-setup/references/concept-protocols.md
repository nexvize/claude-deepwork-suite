# Concept Protocols - Deepwork Suite v3

Fuer Projekttypen: concept, research, marketing

---

## StructuredPlanning Protocol

**Zweck:** Grobe Idee in strukturierten Plan umwandeln: Problemstellung, Optionen, Empfehlung, Umsetzungspfad
**Wann einsetzen:** Zu Beginn jedes neuen Projekts oder Initiatives, bei strategischen Entscheidungen, wenn aus einer vagen Idee ein konkreter Plan werden soll

### Ablauf

1. **Problemstellung scharfstellen** - Was ist das eigentliche Problem? Was ist das Symptom, was die Ursache? Wer hat das Problem? Wie oft? Welche Konsequenzen hat es wenn es ungloest bleibt?
2. **Erfolgskriterien definieren** - Woran erkennen wir, dass das Problem geloest ist? Messbare Kriterien formulieren. Was ist "gut genug", was ist "exzellent"?
3. **Rahmenbedingungen erfassen** - Zeit, Budget, Team, Technologie-Constraints. Was ist nicht verhandelbar?
4. **Optionen generieren** - Mindestens 3 echte Alternativen, keine Scheinalternativen. Fuer jede Option: Kurzbeschreibung, Pros, Cons, Aufwand, Risiko.
5. **Optionen bewerten** - Bewertungsmatrix mit gewichteten Kriterien. Welche Option erfuellt Erfolgskriterien am besten bei vertretbarem Risiko?
6. **Empfehlung begruenden** - Warum diese Option? Was ist der entscheidende Trade-off? Welche Risiken werden bewusst akzeptiert?
7. **Umsetzungspfad skizzieren** - Grobe Phasen, kritische Abhaengigkeiten, erste Schritte. Was passiert als naechstes?
8. **Annahmen dokumentieren** - Was muss wahr sein damit der Plan funktioniert? Wo liegt das groesste Risiko?

### Output-Format

    ## StructuredPlan: [Projektname / Initiative]
    Erstellt: YYYY-MM-DD

    Problem
    [2-3 Saetze: Was ist das Problem, wer hat es, was passiert wenn ungloest]

    Erfolgskriterien
    - [Messbar, zeitgebunden]
    - [...]

    Rahmenbedingungen
    - Zeit: [Deadline / Zeitraum]
    - Budget: [EUR oder Personentage]
    - Constraints: [Was ist nicht verhandelbar]

    Optionen

    Option A: [Name]
    Beschreibung: [...]
    Pros:  [Liste]
    Cons:  [Liste]
    Aufwand: [gering / mittel / hoch]
    Risiko:  [gering / mittel / hoch]

    Option B: [Name]
    [...]

    Bewertungsmatrix:
    Kriterium         | Gewicht | Option A | Option B | Option C
    Erfuellung Ziel   | 40%     | 4/5      | 3/5      | 5/5
    Aufwand           | 30%     | 5/5      | 4/5      | 2/5
    Risiko            | 30%     | 4/5      | 5/5      | 3/5
    Gewichteter Score |         | 4.3      | 3.9      | 3.3

    Empfehlung: Option A
    Begruendung: [Warum diese Option? Welche Trade-offs werden bewusst akzeptiert?]

    Umsetzungspfad
    Phase 1 (Woche 1-2): [...]
    Phase 2 (Woche 3-6): [...]
    Phase 3 (ab Woche 7): [...]
    Erste Schritte (sofort): [...]

    Kritische Annahmen
    - [Was muss wahr sein damit der Plan funktioniert]
    - [Wo liegt das groesste Risiko]

---

## StakeholderMap Protocol

**Zweck:** Stakeholder identifizieren - wer betroffen ist, was sie wollen, wie stark ihr Einfluss ist
**Wann einsetzen:** Zu Beginn jedes Projekts mit mehreren Beteiligten, vor wichtigen Praesentationen oder Entscheidungen, bei Widerstand oder Konflikten

### Ablauf

1. **Stakeholder brainstormen** - Wer ist direkt betroffen? Wer trifft Entscheidungen? Wer finanziert? Wer nutzt das Ergebnis? Wer koennte blockieren? Wer wird vergessen aber wichtig sein?
2. **Einfluss und Interesse einschaetzen** - Fuer jeden Stakeholder: Einfluss (niedrig/mittel/hoch) und Interesse (niedrig/mittel/hoch). Ergibt 4-Felder-Matrix.
3. **Erwartungen und Bedenken erfassen** - Was will jeder Stakeholder? Was befuerchtet er? Was sind seine roten Linien?
4. **Interessen-Konflikte identifizieren** - Wo widersprechen sich Stakeholder-Interessen? Wer ist mit wem im Widerstreit?
5. **Engagement-Strategie ableiten** - Pro Stakeholder-Quadrant: Wie stark einbinden? Wie kommunizieren? Wie oft?
6. **Kommunikationsplan skizzieren** - Wer bekommt welche Informationen, wann, ueber welchen Kanal?

### Output-Format

    ## StakeholderMap: [Projektname]
    Erstellt: YYYY-MM-DD

    Stakeholder-Liste:
    Name / Rolle       | Einfluss | Interesse | Quadrant
    CEO (Maria M.)     | Hoch     | Mittel    | Keep Satisfied
    Product Lead (Tom) | Hoch     | Hoch      | Manage Closely
    End-User-Team      | Niedrig  | Hoch      | Keep Informed
    IT-Security        | Mittel   | Niedrig   | Monitor

    Quadranten:
    - Manage Closely (Hoch/Hoch): Aktiv einbinden, regelmaessige Updates, Entscheidungen gemeinsam
    - Keep Satisfied (Hoch/Niedrig): Regelmaessig informieren, Bedenken fruehzeitig adressieren
    - Keep Informed (Niedrig/Hoch): Newsletter, Demo-Einladungen, Feedback einholen
    - Monitor (Niedrig/Niedrig): Passiv auf dem Laufenden halten

    Stakeholder-Details:

    CEO (Maria M.)
    Erwartungen: ROI-Nachweis, keine operativen Unterbrechungen
    Bedenken:    Zu hohe Kosten, zu langsame Umsetzung
    Rote Linien: Budget-Ueberschreitung >20%
    Strategie:   Monatliches Executive-Update, Fokus auf Zahlen

    Product Lead (Tom)
    Erwartungen: Klar definierte Requirements, schnelle Entscheidungen
    Bedenken:    Scope Creep, Ressourcen-Konflikte
    Strategie:   Woechentliche Sync, fruehzeitig bei Trade-offs einbeziehen

    Interessen-Konflikte:
    - CEO will schnell, IT-Security braucht Zeit fuer Pruefung -> Eskalationspfad definieren
    - [...]

    Kommunikationsplan:
    Stakeholder     | Format         | Frequenz   | Naechstes Datum
    CEO             | Executive 1-Pager | Monatlich | 2025-02-01
    Product Lead    | Sync-Meeting   | Woechtentlich | 2025-01-27
    End-User-Team   | Demo + Q&A     | Quartalsweise | 2025-03-01

---

## ScenarioAnalysis Protocol

**Zweck:** 3-Szenario-Planung (optimistisch / realistisch / pessimistisch) mit Eintrittsbedingungen
**Wann einsetzen:** Bei Entscheidungen unter Unsicherheit, bei strategischer Planung, bei Budgetplanung, vor Investitionen oder groesseren Verpflichtungen

### Ablauf

1. **Schluessel-Unsicherheiten identifizieren** - Welche 2-3 Faktoren sind entscheidend fuer den Ausgang? Was kann sich stark veraendern und liegt ausserhalb unserer Kontrolle?
2. **Szenarien konstruieren** - Optimistisch: alles laeuft besser als erwartet. Realistisch: wahrscheinlichster Verlauf. Pessimistisch: vieles laeuft schlechter als erwartet. Kein "Katastrophen"-Szenario noetig.
3. **Eintrittsbedingungen definieren** - Welche Signale / Ereignisse zeigen an, dass wir in welchem Szenario sind? Was muss eintreten, was ausbleiben?
4. **Auswirkungen pro Szenario** - Fuer jedes Szenario: Impact auf Umsatz, Kosten, Timeline, Team, Kunden.
5. **Fruehindikatoren festlegen** - Welche Metriken ueberwachen wir, um fruehzeitig zu erkennen in welches Szenario wir gleiten?
6. **Massnahmen je Szenario planen** - Was tun wir wenn Szenario X eintritt? Wer entscheidet? In welchem Zeitfenster?
7. **Review-Intervall festlegen** - Wann schauen wir die Szenarien neu an?

### Output-Format

    ## ScenarioAnalysis: [Fragestellung / Projekt]
    Erstellt: YYYY-MM-DD | Review: [Datum]

    Schluessel-Unsicherheiten:
    1. [Faktor A, z.B. Markt-Wachstum]
    2. [Faktor B, z.B. Regulierung]

    Szenarien:

    Szenario A: Optimistisch (Eintrittswahrscheinlichkeit: 25%)
    Beschreibung: [Was passiert, was anders ist als erwartet]
    Eintrittsbedingungen: [Welche Signale zeigen dieses Szenario an]
    Impact:
      - Umsatz: +X%
      - Kosten: -Y%
      - Timeline: X Wochen frueher
    Massnahmen: [Was tun wir in diesem Fall]

    Szenario B: Realistisch (Eintrittswahrscheinlichkeit: 55%)
    Beschreibung: [Wahrscheinlichster Verlauf]
    Eintrittsbedingungen: [Standard-Annahmen halten]
    Impact:
      - Umsatz: Basis
      - Kosten: Basis
      - Timeline: Basis
    Massnahmen: [Planmaessig vorgehen]

    Szenario C: Pessimistisch (Eintrittswahrscheinlichkeit: 20%)
    Beschreibung: [Was schief laeuft]
    Eintrittsbedingungen: [Welche Warnsignale beobachten]
    Impact:
      - Umsatz: -X%
      - Kosten: +Y%
      - Timeline: X Wochen verspaetet
    Massnahmen: [Contingency-Plan, Entscheidungsbaum]

    Fruehindikatoren (Monitoring):
    Metrik            | Optimistisch | Realistisch | Pessimistisch | Frequenz
    Conversion Rate   | >5%          | 3-5%        | <3%           | Woechentlich
    Support-Tickets   | <20/Woche    | 20-50/Woche | >50/Woche     | Taeglich

    Review-Termin: [Datum]

---

## PitchDeck Protocol

**Zweck:** Pitch strukturieren: Problem, Loesung, Markt, Traktion, Team, Ask. Pro Slide: Inhalt und Anti-Patterns.
**Wann einsetzen:** Vor Investor-Praesentation, bei internem Business-Case, bei Partnerschaftsgespraechen, bei Foerderantraegen

### Ablauf

1. **Zielgruppe und Kontext klaeren** - Wer sieht den Pitch? Was wissen sie bereits? Was ist ihre Hauptfrage? Was wollen sie am Ende tun?
2. **Kernbotschaft formulieren** - Einen Satz: Was ist das Unternehmen/Projekt und warum ist es relevant? (Elevator Pitch)
3. **Narrativ-Bogen festlegen** - Jeder Slide baut auf dem vorigen auf. Problem -> Schmerz -> Loesung -> Beweis -> Markt -> Warum wir.
4. **Jeden Slide einzeln strukturieren** - Was ist die eine Aussage dieses Slides? Welche Evidenz stuetzt sie? Was wird gezeigt (Grafik/Zahl/Zitat)?
5. **Anti-Patterns pro Slide pruefen** - Typische Fehler vermeiden (zu viel Text, schwache Marktgroesse-Argumentation, etc.)
6. **Zahlen verifizieren** - Alle Metriken und Marktgroessen-Zahlen auf Plausibilitaet pruefen.
7. **Storytelling-Test** - Pitch laut vorlesen. Ergibt sich ein roter Faden? Ist jeder Slide notwendig?

### Output-Format

    ## PitchDeck: [Projektname]
    Zielgruppe: [Investoren / Partner / Intern] | Anlass: [...]
    Gesamtlaenge: [X Slides, Y Minuten]

    Elevator Pitch (1 Satz):
    "[Unternehmen] hilft [Zielgruppe] dabei [Problem] zu loesen, indem [Loesung] - anders als [Alternative]."

    Slide-Struktur:

    Slide 1: Cover
    Inhalt: Unternehmensname, Tagline, Datum, Praesentator
    Anti-Pattern: Kein generisches Logo-Slide ohne Tagline

    Slide 2: Problem
    Inhalt: Das Problem in einer Zahl oder Situation greifbar machen. Wer leidet? Wie oft? Welche Kosten?
    Anti-Pattern: Problem zu abstrakt - muss der Zuschauer spueren koennen
    Beispiel: "Kleine Unternehmen verlieren 8 Stunden pro Woche an manuelle Buchhaltung"

    Slide 3: Loesung
    Inhalt: Wie losen wir das Problem? Demo oder Produkt-Screenshot. Kernfunktionalitaet in 3 Punkten.
    Anti-Pattern: Feature-Liste statt Nutzen-Beschreibung

    Slide 4: Markt
    Inhalt: TAM / SAM / SOM. Wie wurde berechnet? Wachstumsrate?
    Anti-Pattern: "1% von einem Riesenmarkt" - kein Investor kauft das. Bottom-up-Rechnung zeigen.

    Slide 5: Geschaeftsmodell
    Inhalt: Wie verdienen wir Geld? Pricing. Unit Economics (LTV, CAC, Payback).
    Anti-Pattern: Zu viele Monetarisierungsideen - focus on what drives revenue today

    Slide 6: Traktion
    Inhalt: Was haben wir bisher bewiesen? Kunden, ARR, Wachstum, Retention, Key Milestones.
    Anti-Pattern: "Wir haben X Interessenten" - nur zahlende Kunden oder echte Metriken

    Slide 7: Wettbewerb
    Inhalt: Positionierungsmatrix oder klare Differenzierung. Warum gewinnen wir?
    Anti-Pattern: "Wir haben keinen Wettbewerb" - sofort Glaubwuerdigkeit verloren

    Slide 8: Team
    Inhalt: Warum dieses Team fuer dieses Problem? Relevante Erfahrung, Komplementaritaet.
    Anti-Pattern: Lange CV-Liste - nur das Relevante

    Slide 9: Ask und Use of Funds
    Inhalt: Wie viel wird gesucht? Fuer was wird es verwendet? Was wird damit erreicht (Milestones)?
    Anti-Pattern: "Wir brauchen Geld fuer Marketing" - keine Milestones

    Slide 10: Vision
    Inhalt: Wo sind wir in 3-5 Jahren? Warum ist das gross?
    Anti-Pattern: Zu vage ("wir werden Marktfuehrer") - konkrete Vision mit Zahlen

---

## RoadmapBuild Protocol

**Zweck:** Ziele in phasierte Roadmap umwandeln mit Milestones, Abhaengigkeiten, Ressourcenschaetzungen
**Wann einsetzen:** Bei Produktplanung, bei Projektplanung, bei OKR-Umsetzung, bevor ein Team loslegt

### Ablauf

1. **Ziele klaeren** - Was soll die Roadmap erreichen? Welche OKRs / Strategieziele werden dadurch adressiert?
2. **Backlog zusammenstellen** - Alle bekannten Vorhaben, Features, Initiativen sammeln. Noch nicht priorisieren.
3. **Priorisieren** - Nach Impact/Effort oder ICE Score (Impact, Confidence, Ease). Was bringt am meisten zum Ziel bei vertretbarem Aufwand?
4. **Phasen definieren** - Sinnvolle Zeitraeume (Quartale, Monate, Sprints). Was ist Phase 0 (Now), Phase 1 (Next), Phase 2 (Later)?
5. **Milestones festlegen** - Was ist das lieferbare Ergebnis am Ende jeder Phase? Wie messen wir Erfolg?
6. **Abhaengigkeiten kartieren** - Welche Vorhaben muessen vor anderen abgeschlossen sein? Wo sind externe Abhaengigkeiten (andere Teams, Zulieferer)?
7. **Ressourcen einschaetzen** - Personentage oder Story Points pro Vorhaben. Kapazitaet des Teams gegenueberstellen. Realistisch?
8. **Risiken und Puffer einplanen** - Wo sind die groessten Unsicherheiten? Pufferzeit einbauen.
9. **Kommunikationsformat waehlen** - Timeline-View, Now/Next/Later-Board, oder Quartals-Grid - je nach Publikum.

### Output-Format

    ## Roadmap: [Produkt / Projekt]
    Erstellt: YYYY-MM-DD | Zeitraum: [Q1-Q4 2025]
    Ziel: [Was soll erreicht werden - messbar]

    Priorisierter Backlog (ICE-Score):
    Vorhaben           | Impact | Confidence | Ease | Score | Phase
    Login via SSO      | 8      | 9          | 7    | 8.0   | Q1
    Mobile App         | 9      | 6          | 4    | 6.3   | Q2
    API v2             | 7      | 8          | 6    | 7.0   | Q1
    KI-Empfehlungen    | 8      | 5          | 3    | 5.3   | Q3

    Phasen:

    Phase 0 - Now (Jan-Feb 2025)
    Milestone: [Lieferbares Ergebnis]
    Vorhaben:
    - [ ] SSO Login (8 PT) [keine Abhaengigkeiten]
    - [ ] API v2 Grundgeruest (12 PT) [keine Abhaengigkeiten]
    Kapazitaet: 3 Devs x 40 PT = 120 PT verfuegbar | geplant: 80 PT

    Phase 1 - Next (Mrz-Mai 2025)
    Milestone: [Lieferbares Ergebnis]
    Vorhaben:
    - [ ] Mobile App MVP (35 PT) [benoetigt API v2]
    Abhaengigkeit: API v2 muss in Phase 0 abgeschlossen sein
    Kapazitaet: 120 PT | geplant: 95 PT

    Phase 2 - Later (Jun-Sep 2025)
    Milestone: [Lieferbares Ergebnis]
    Vorhaben:
    - [ ] KI-Empfehlungen (50 PT) [benoetigt Mobile App + Nutzerdaten]
    Puffer: 20 PT fuer unvorhergesehenes

    Abhaengigkeits-Diagramm:
    SSO Login -> (independent)
    API v2 Grundgeruest -> Mobile App MVP -> KI-Empfehlungen

    Risiken:
    - Mobile App: kein Mobile-Dev im Team -> Hiring oder Freelancer in Q1
    - KI: Datenmenge unklar -> Review nach 3 Monaten Mobile-Daten

---

## RiskMatrix Protocol

**Zweck:** Risiken identifizieren, kategorisieren (Wahrscheinlichkeit x Impact) und Gegenmassnahmen definieren
**Wann einsetzen:** Zu Beginn eines Projekts, vor wichtigen Entscheidungen, bei Budgetfreigaben, bei Risiko-Reviews mit Stakeholdern

### Ablauf

1. **Risiken brainstormen** - Alle moeglichen Risiken auflisten ohne Bewertung. Kategorien: Technisch, Markt, Team/Personal, Regulierung, Finanziell, Abhaengigkeiten.
2. **Wahrscheinlichkeit einschaetzen** - Fuer jedes Risiko: Wie wahrscheinlich ist es? (1=selten, 2=moeglich, 3=wahrscheinlich, 4=fast sicher)
3. **Impact einschaetzen** - Wenn das Risiko eintritt: Wie schlimm? (1=vernachlaessigbar, 2=gering, 3=erheblich, 4=kritisch)
4. **Risiko-Score berechnen** - Wahrscheinlichkeit x Impact = Score (1-16). Ab Score 9: Kritisch. 5-8: Hoch. 3-4: Mittel. 1-2: Niedrig.
5. **Top-Risiken priorisieren** - Auf die Top 5 konzentrieren.
6. **Gegenmassnahmen definieren** - Fuer jedes Top-Risiko: Vermeidung (Risiko eliminieren), Verminderung (Wahrscheinlichkeit senken), Uebertragung (Versicherung, Vertrag), Akzeptanz (bewusst tragen).
7. **Owner und Fruehwarnsystem** - Wer ist verantwortlich? Welche Signale zeigen an dass das Risiko eintritt?
8. **Review-Rhythmus** - Wann wird die Matrix aktualisiert?

### Output-Format

    ## RiskMatrix: [Projektname]
    Erstellt: YYYY-MM-DD | Review: [Datum]

    Alle Risiken:
    ID | Risiko                        | Kategorie | W | I | Score | Prioritaet
    R1 | Schluessel-Dev kuendigt        | Team      | 2 | 4 | 8     | Hoch
    R2 | Datenschutz-Regulierung aendert| Regulierung| 1| 4 | 4     | Mittel
    R3 | Hauptlieferant faellt aus      | Abhaengig. | 2| 3 | 6     | Hoch
    R4 | Wettbewerber kopiert Feature   | Markt     | 3 | 2 | 6     | Hoch
    R5 | Budget wird gekuerzt           | Finanziell| 2 | 4 | 8     | Hoch

    (W = Wahrscheinlichkeit 1-4, I = Impact 1-4)

    Top Risiken - Massnahmenplan:

    R1: Schluessel-Dev kuendigt (Score 8)
    Gegenmassnahme: Verminderung
    Massnahmen:
    - Dokumentation und Code-Reviews priorisieren (Wissenstransfer)
    - Retention-Gespraech fuehren (Gehalt, Entwicklung)
    - Backup-Kandidaten in Pipeline halten
    Owner: CTO
    Fruehwarnsignal: Motivationsabfall, haeufige Fehltage, LinkedIn-Aktivitaet steigt
    Fallback: Freelancer-Pool vorbereiten

    R3: Hauptlieferant faellt aus (Score 6)
    Gegenmassnahme: Uebertragung + Verminderung
    Massnahmen:
    - SLA mit Poenale im Vertrag verankern
    - Zweitlieferant qualifizieren (bis Q2)
    Owner: COO
    Fruehwarnsignal: Lieferverzoegerungen >3x in 30 Tagen

    Risiko-Heatmap (schematisch):
    Impact 4 |  R2   | R1, R5 |       |
    Impact 3 |       | R3     |       |
    Impact 2 |       |        | R4    |
    Impact 1 |       |        |       |
             | W=1   | W=2    | W=3   | W=4

    Review-Termin: [Datum]
    Verantwortlich: [Name]

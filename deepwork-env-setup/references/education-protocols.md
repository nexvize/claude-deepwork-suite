# Education Protocols - Deepwork Suite v3

Fuer Projekttypen: education, concept, content

---

## LearningOutcomes Protocol

**Zweck:** Messbare Lernziele formulieren (Blooms Taxonomie), sicherstellen dass sie erreichbar und pruefbar sind
**Wann einsetzen:** Zu Beginn jedes Bildungsvorhabens (Kurs, Tutorial, Workshop, Onboarding), vor Curriculum-Entwicklung, bei Review bestehender Kurse

### Ablauf

1. **Zielgruppe klaeren** - Wer sind die Lernenden? Welches Vorwissen haben sie? Was koennen sie nach dem Kurs anders machen als vorher?
2. **Blooms Taxonomie-Level bestimmen** - Fuer jedes Lernziel: Auf welchem Niveau soll gelernt werden?
   - Erinnern (remember): Fakten abrufen koennen
   - Verstehen (understand): Erklaeren und in eigene Worte fassen
   - Anwenden (apply): In bekannten Situationen einsetzen
   - Analysieren (analyze): Zerlegen, Zusammenhaenge erkennen
   - Evaluieren (evaluate): Beurteilen, kritisch bewerten
   - Erschaffen (create): Neues erzeugen, eigene Loesungen entwickeln
3. **Lernziel-Formulierung** - Template: "Nach dem Abschluss koennen die Lernenden [Verb auf Blooms-Level] [Inhalt] [Kontext/Bedingung]."
4. **Pruefbarkeit verifizieren** - Kann man beobachten/messen ob das Ziel erreicht wurde? Wenn nicht: umformulieren.
5. **Erreichbarkeit pruefen** - Ist das Ziel mit dem vorhandenen Vorwissen und der verfuegbaren Zeit realistisch?
6. **Ausrichtung pruefen (Constructive Alignment)** - Stimmen Lernziele, Lernaktivitaeten und Pruefung ueberein?
7. **Lernziel-Set finalisieren** - Maximal 5-7 Hauptziele. Hierarchisch strukturieren wenn noetig.

### Output-Format

    ## LearningOutcomes: [Kurs / Workshop / Tutorial]
    Zielgruppe: [Wer lernt]
    Vorwissen: [Was Lernende bereits koennen/wissen muessen]
    Dauer: [X Stunden / Tage]

    Lernziele:

    LZ1 (Verstehen): Nach dem Abschluss koennen die Lernenden erklaeren,
    was [Konzept X] ist und warum es in [Kontext Y] eingesetzt wird.
    Blooms-Level: 2 - Verstehen
    Pruefbar durch: Muendliche Erklaerung oder schriftliche Zusammenfassung
    Erreichbar: Ja, nach Modul 1 (2h)

    LZ2 (Anwenden): Die Lernenden koennen [Technik Z] auf ein neues Problem
    anwenden und dabei [Kriterium A] und [Kriterium B] einhalten.
    Blooms-Level: 3 - Anwenden
    Pruefbar durch: Praktische Uebung mit Bewertungsrubrik
    Erreichbar: Ja, nach Modul 3 (nach 6h Gesamtzeit)

    LZ3 (Analysieren): Die Lernenden koennen zwei Loesungsansaetze fuer [Problem]
    hinsichtlich [Kriterien] vergleichen und die bessere Option begruenden.
    Blooms-Level: 4 - Analysieren
    Pruefbar durch: Case-Study-Aufgabe
    Erreichbar: Ja, als Abschlussaufgabe nach 8h

    Constructive Alignment Check:
    LZ1 -> Lernaktivitaet: Video + Lesematerial -> Pruefung: Erklaer-Aufgabe [OK]
    LZ2 -> Lernaktivitaet: Geleitete Uebung + Feedback -> Pruefung: Eigen-Uebung [OK]
    LZ3 -> Lernaktivitaet: Case Discussion -> Pruefung: Case Study [OK]

---

## CurriculumOutline Protocol

**Zweck:** Kurs oder Tutorial strukturieren: Voraussetzungs-Mapping, Modul-Reihenfolge, Zeitschaetzungen, Wissensabhaengigkeiten
**Wann einsetzen:** Bei Kursentwicklung, bei Tutorial-Erstellung, bei Onboarding-Programm-Design, bei Review bestehender Curricula

### Ablauf

1. **Lernziele als Ausgangspunkt** - Alle Lernziele aus LearningOutcomes Protocol verwenden.
2. **Wissens-Graph aufbauen** - Welche Konzepte setzen welche anderen voraus? Topologische Sortierung: Was muss zuerst gelernt werden?
3. **Module definieren** - Sinnvolle thematische Einheiten. Jedes Modul hat: Titel, Lernziel(e), Inhaltsliste, Zeitschaetzung.
4. **Sequenz optimieren** - Vom Einfachen zum Komplexen. Spiralcurriculum: Konzepte auf hoeherem Niveau wiederholt aufgreifen.
5. **Zeitschaetzungen** - Pro Inhaltselement: Lesen/Video (x min), Uebung (x min), Reflection (x min). Gesamt pro Modul. Gesamtzeit des Kurses.
6. **Voraussetzungen dokumentieren** - Was muss der Lernende VOR dem Kurs koennen? Empfohlene Vorkurse oder Ressourcen angeben.
7. **Luecken identifizieren** - Gibt es Spruenge im Curriculum die zu gross sind? Bruecken-Inhalte einplanen.
8. **Variationen einplanen** - Optional-Inhalte fuer Fortgeschrittene markieren. Kernpfad vs. erweiterter Pfad.

### Output-Format

    ## CurriculumOutline: [Kursname]
    Zielgruppe: [Wer]
    Gesamtdauer: [X Stunden / X Wochen]
    Format: [Selbstlernkurs / Praesenz / Hybrid]

    Voraussetzungen:
    - Muss vorher koennen: [Liste]
    - Empfohlene Vorkurse: [Liste]
    - Technisches Setup: [Tools, Software]

    Wissens-Graph (vereinfacht):
    Grundlagen -> Konzept A -> Konzept B -> Anwendung
                           -> Konzept C -> [optional: Vertiefung]

    Modul-Uebersicht:
    # | Modul             | Lernziele | Dauer | Typ
    1 | Grundlagen [X]    | LZ1       | 2h    | Video + Lesen
    2 | Konzept A         | LZ2       | 3h    | Video + Uebung
    3 | Konzept B + C     | LZ3       | 4h    | Uebung + Diskussion
    4 | Praxisprojekt     | LZ2+LZ3   | 5h    | Projekt
    5 | Review und Pruefung| alle     | 1h    | Quiz + Reflexion

    Modul-Details:

    Modul 1: Grundlagen [X]
    Lernziel: LZ1 - Erklaeren was [X] ist
    Inhalt:
    - [Thema 1.1] (Video, 15 min)
    - [Thema 1.2] (Lesen, 20 min)
    - Wissenscheck (Quiz, 5 min)
    Gesamtdauer: 40 min
    Abhaengigkeiten: keine
    Vorwissen noetig: [...]

    Kernpfad: Module 1, 2, 3, 5 (10h)
    Erweiterter Pfad: + Modul 4 Praxisprojekt (15h gesamt)

---

## ExerciseDesign Protocol

**Zweck:** Uebungen erstellen mit Ziel, Anleitung, Musterloesung, typischen Fehlern und Bewertungskriterien
**Wann einsetzen:** Bei Kursentwicklung, bei Workshop-Vorbereitung, bei der Erstellung von Praxisaufgaben

### Ablauf

1. **Lernziel der Uebung klaeren** - Welches Lernziel wird adressiert? Welches Blooms-Level?
2. **Uebungstyp waehlen** - Anwendungsuebung (bekanntes Problem), Transfer-Uebung (neues Problem), kreative Uebung, Debugging-Uebung, Diskussionsaufgabe.
3. **Scaffolding entscheiden** - Wie viel Unterstuetzung bekommt der Lernende? Viel (geleitete Uebung), mittel (Hinweise verfuegbar), wenig (offene Aufgabe).
4. **Aufgabenstellung schreiben** - Klar, eindeutig, ohne versteckte Anforderungen. Kontext, Aufgabe, Anforderungen separat formulieren.
5. **Musterloesung erstellen** - Vollstaendige Loesung. Erklaerungen warum dieser Weg. Alternativen erwaehnen wenn relevant.
6. **Haeufige Fehler antizipieren** - Welche typischen Missverstaendnisse werden in dieser Aufgabe sichtbar? Feedback-Hinweise fuer jeden Fehler.
7. **Bewertungsrubrik erstellen** - Wenn bewertet wird: Kriterien, Gewichtung, Beschreibung fuer "vollstaendig / teilweise / nicht erfuellt".
8. **Test-Run** - Uebung selbst oder mit Testperson durchgehen. Zeitbedarf messen. Unklarheiten identifizieren.

### Output-Format

    ## Exercise: [Titel]
    Lernziel: [LZ-Referenz]
    Blooms-Level: [Anwenden / Analysieren / ...]
    Typ: [Anwendung / Transfer / Debugging / ...]
    Zeitbedarf: [X Minuten]
    Scaffolding: [Hoch / Mittel / Niedrig]
    Voraussetzungen: [Was muss vorher bekannt sein]

    Aufgabenstellung:
    Kontext:
    [Situation beschreiben - warum ist diese Aufgabe relevant]

    Aufgabe:
    [Was soll der Lernende konkret tun - so klar wie moeglich]

    Anforderungen:
    - [Spezifisches Kriterium 1]
    - [Spezifisches Kriterium 2]
    - [Spezifisches Kriterium 3]

    Hinweise (optional, Scaffolding):
    - [Tipp 1]
    - [Tipp 2]

    Musterloesung:
    [Vollstaendige Loesung mit Erklaerungen]

    Alternative Loesungsansaetze:
    [Wenn relevant: andere gueltiger Wege]

    Haeufige Fehler:
    Fehler 1: [Was oft falsch gemacht wird]
    Ursache: [Warum passiert das]
    Feedback: [Hinweis der zur richtigen Loesung fuehrt, ohne sie zu verraten]

    Bewertungsrubrik:
    Kriterium           | Gewicht | Vollstaendig           | Teilweise             | Nicht erfuellt
    Korrektheit Ergebnis| 50%     | Ergebnis korrekt       | Kleiner Fehler        | Falscher Ansatz
    Code-Qualitaet      | 30%     | Lesbar, kommentiert    | Lesbar, unkommentiert | Unlesbar
    Anforderungen       | 20%     | Alle erfuellt          | 2 von 3               | <2 erfuellt

---

## AssessmentDesign Protocol

**Zweck:** Pruefungen / Tests entwerfen: Fragetypen, Schwierigkeitsverteilung, Antwortschlussel, Feedback-Nachrichten
**Wann einsetzen:** Nach Curriculum-Erstellung, bei Quiz-Design fuer E-Learning, bei Workshop-Evaluierung, bei Zertifizierungs-Pruefungen

### Ablauf

1. **Pruefungszweck klaeren** - Formativ (Lernfortschritt pruefen, Feedback geben) oder summativ (Bestehen/Nicht-Bestehen entscheiden)?
2. **Zu pruefende Lernziele auflisten** - Jedes Lernziel sollte durch mind. eine Frage abgedeckt sein.
3. **Fragetypen waehlen** - Multiple Choice (schnell, eindeutig), Multiple Select, True/False, Lueckentext, Kurzantwort, Essay, Praktische Aufgabe.
4. **Schwierigkeitsverteilung planen** - Typisch: 30% einfach (Erinnern), 50% mittel (Verstehen/Anwenden), 20% schwer (Analysieren/Evaluieren).
5. **Fragen formulieren** - Jede Frage: eindeutig, keine Doppelnegationen, kein Wissens-Trivia das nichts mit Lernzielen zu tun hat.
6. **Antwortoptionen bei MC gestalten** - 4 Optionen, alle plausibel. Haeufige Fehler als Distraktoren nutzen. Kein "Alle oben genannten".
7. **Antwortschlussel und Erklaerungen** - Fuer jede Antwort: richtig/falsch + Erklaerung warum. Fuer falsche Antworten: Lernhinweis.
8. **Feedback-Nachrichten schreiben** - Positives Feedback bei richtiger Antwort kurz. Erklaerung bei falscher Antwort lehrreich, nicht beschaemend.
9. **Bestehensgrenze festlegen** - Standard: 70-80%. Begruendung dokumentieren.
10. **Review** - Test selbst durchgehen. Sind alle Fragen fair? Gibt es Doppeldeutigkeiten?

### Output-Format

    ## Assessment: [Test-/Quizname]
    Zugehoerig zu: [Kurs / Modul]
    Zweck: Formativ / Summativ
    Gesamtfragen: X
    Zeitlimit: Y Minuten
    Bestehensgrenze: Z%

    Abgedeckte Lernziele:
    LZ1: Fragen 1, 3, 5
    LZ2: Fragen 2, 4, 7
    LZ3: Fragen 6, 8

    Schwierigkeitsverteilung:
    Einfach (Erinnern/Verstehen): 3 Fragen (30%)
    Mittel (Anwenden): 5 Fragen (50%)
    Schwer (Analysieren): 2 Fragen (20%)

    Fragen:

    Frage 1 (MC, Einfach, LZ1):
    Was ist [Konzept X]?
    A) [Richtige Antwort]
    B) [Falsche Antwort - haeufiger Irrtum]
    C) [Falsche Antwort - verwandtes Konzept]
    D) [Falsche Antwort - klingt aehnlich]
    Antwort: A
    Erklaerung richtig: [Warum A korrekt ist]
    Erklaerung B: [Warum B falsch ist + Lernhinweis]
    Feedback richtig: "Genau! [Kurzbestaetigung]"
    Feedback falsch: "[Erklaerung ohne Blosstellen] Schau nochmal in [Modul X] nach."

    Auswertungshinweise:
    - 90-100%: Ausgezeichnet - bereit fuer Modul X
    - 70-89%:  Bestanden - ggf. [Bereich] wiederholen
    - <70%:    Nicht bestanden - [Modul] nochmals durcharbeiten

---

## ConceptExplanation Protocol

**Zweck:** Komplexes Konzept erklaeren: Analogie zuerst, dann Detail, dann Anwendung, dann Selbsttest
**Wann einsetzen:** Bei der Erstellung von Lernmaterialien, bei Erklaervideos, bei Dokumentation, bei technischen Blog-Posts, bei Live-Unterricht

### Ablauf

1. **Konzept und Lernziel klaeren** - Was soll erklaert werden? Auf welchem Niveau? Fuer wen?
2. **Analogie finden** - Was kennt die Zielgruppe bereits, das aehnlich funktioniert? Die Analogie muss das Kernprinzip treffen, nicht alle Details.
3. **Analogie erklaeren** - Vertrautheit aufbauen. Dann: "Das ist aehnlich wie [Konzept], weil..."
4. **Konzept im Detail erklaeren** - Jetzt das eigentliche Konzept. Schritt fuer Schritt. Fachbegriffe einfuehren und sofort erklaeren.
5. **Wo die Analogie versagt** - Jede Analogie hat Grenzen. Explizit sagen, wo sie aufhoert zu passen. Vermeidet spaetere Missverstaendnisse.
6. **Anwendung zeigen** - Konkrete Beispiele. Wenn moeglich: interaktiv (Lernende machen etwas selbst).
7. **Zusammenfassung** - Kernaussagen in 3-5 Bulletpoints. Was muss haengen bleiben?
8. **Selbsttest-Fragen** - 3-5 Fragen die der Lernende sich selbst stellen kann um zu pruefen ob er es verstanden hat.

### Output-Format

    ## ConceptExplanation: [Konzeptname]
    Zielgruppe: [Wer]
    Vorwissen: [Was sie bereits kennen]
    Lernziel: [Was sie danach koennen]
    Format: [Text / Video-Script / Unterricht]

    Analogie:
    "[Konzept X] funktioniert wie [bekanntes Ding Y].
    Stell dir vor: [lebendige, konkrete Beschreibung der Analogie]."

    Verbindung zum Konzept:
    "Aehnlich funktioniert [Konzept X]: [Verbindung erklaeren]."

    Detail-Erklaerung:

    1. [Erster Aspekt]
    [Erklaerung. Fachbegriff in Klammern beim ersten Vorkommen.]

    2. [Zweiter Aspekt]
    [Erklaerung]

    Wo die Analogie aufhoert:
    "[Y] und [X] unterscheiden sich darin, dass [wichtiger Unterschied].
    Das musst du wissen, um [Fehler] zu vermeiden."

    Anwendungsbeispiel:
    [Konkretes, realistisches Beispiel das die Zielgruppe kennt]
    [Schritt-fuer-Schritt Durchfuehrung]

    Zusammenfassung:
    - [Kernaussage 1]
    - [Kernaussage 2]
    - [Kernaussage 3]

    Selbsttest-Fragen:
    1. [Frage die Verstaendnis prueft - keine Faktenfrage]
    2. [Frage die Transfer prueft]
    3. [Frage die Abgrenzung zu aehnlichem Konzept prueft]
    4. [Anwendungsfrage]

    Weiterfuehrende Ressourcen:
    - [Ressource fuer Vertiefung]
    - [Ressource fuer Praxis]

---

## LearnerPersona Protocol

**Zweck:** Ziel-Lernende beschreiben: Vorwissen, Ziele, Constraints, Lernstil-Praeferenzen
**Wann einsetzen:** Vor der Kursentwicklung, bei der Anpassung bestehender Kurse an neue Zielgruppen, bei der Erstellung von Lernmaterialien

### Ablauf

1. **Daten sammeln** - Interviews mit typischen Lernenden, Umfragen, Analyse von Support-Fragen, Review von Kurs-Feedback.
2. **Demographische Basisdaten** - Beruf, Erfahrungslevel im Bereich, Alter/Generation (beeinflusst Lerngewohnheiten), geografischer Kontext.
3. **Vorwissen kartieren** - Was wissen sie sicher? Was wissen sie vielleicht? Was wissen sie nicht? Was denken sie zu wissen, stimmt aber nicht?
4. **Ziele und Motivation erfassen** - Warum nehmen sie den Kurs? Intrinsisch (Interesse) oder extrinsisch (Job, Zertifikat)? Was wollen sie konkret danach koennen?
5. **Constraints dokumentieren** - Wie viel Zeit haben sie pro Woche? Lernen sie allein oder in Gruppen? Welche Geraete nutzen sie? Welche Sprachen?
6. **Lernstil-Praeferenzen** - Video oder Text? Beispiele vor Theorie oder umgekehrt? Hands-on oder konzeptuell? Einzel- oder Gruppenarbeit?
7. **Typische Hindernisse** - Was hielt diese Lernenden bisher davon ab, das zu lernen? Angst vor Technik? Zeitmangel? Falsches Vorwissen?
8. **Persona-Karte erstellen** - Kompaktes Profil mit Name (fiktiv), Foto (optional), Zitat, allen obigen Aspekten.

### Output-Format

    ## LearnerPersona: [Persona-Name]
    (Fuer Kurs: [Kursname])

    Persona: [fiktiver Name, z.B. "Anna, die Quereinsteigerin"]
    Rolle: [Beruf / Position]
    Erfahrungslevel: [Einsteiger / Fortgeschritten / Experte]
    Charakteristisches Zitat: "[Was sie ueber das Thema sagen wuerden]"

    Demographie:
    Beruf: [...]
    Erfahrung im Bereich: [X Jahre / kein Vorwissen]
    Typisches Lernumfeld: [Buero / zuhause / unterwegs / alle]

    Vorwissen:
    Sicher bekannt:   [Liste]
    Vielleicht bekannt: [Liste]
    Nicht bekannt:    [Liste]
    Missverstaendnisse (bekannte falsche Annahmen): [Liste]

    Ziele und Motivation:
    Warum dieser Kurs: [Konkreter Grund]
    Was sie danach koennen wollen: [Spezifisch]
    Motivation: [Intrinsisch / Extrinsisch / Gemischt]

    Constraints:
    Verfuegbare Zeit: [X Stunden / Woche]
    Lernformat:       [Selbstlernkurs / Praesenz / hybrid]
    Geraete:          [Desktop / Mobile / beide]

    Lernstil-Praeferenzen:
    - Bevorzugt:   [Video mit Untertiteln / kurze Texte / Beispiele zuerst]
    - Vermeidet:   [Lange Theorie-Bloecke / rein textbasiert]
    - Lernrythmus: [kurze Sessions taeglich / laengere Einheiten am Wochenende]

    Typische Hindernisse:
    - [Hindernis 1: z.B. "Schreckt vor Fachbegriffen zurueck"]
    - [Hindernis 2: z.B. "Hat wenig Zeit fuer Hausaufgaben"]

    Implikationen fuer das Curriculum:
    - [Was muss im Kurs beruecksichtigt werden]
    - [Was sollte vermieden werden]
    - [Welche Beispiele resonieren mit dieser Persona]

# Plain-Language Mandate — deepwork-03-execute

**Canonical:** `deepwork-env-setup/references/plain-language.md` — alle 5 Regeln vollständig dort.

---

## Für diesen Skill besonders relevant

**Regel 2 — Pre-Permission-Block** vor jeder Code-/Datei-Änderung:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Was ich gleich tue: Ich schreibe die Login-Funktion.
Warum: Das ist der nächste Schritt laut Plan.
Auswirkung: Neue Datei "src/auth/login.ts" wird erstellt.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Regel 3 — Verification-Pause:**

```
Ich habe den Abschnitt fertiggestellt und möchte prüfen ob alles funktioniert.
Ich pausiere, weil du die Ergebnisse sehen und bestätigen sollst.

Was ich getestet habe:
1. [Test in Klartext]
2. ...
Ergebnis: [BESTANDEN / FEHLGESCHLAGEN — was genau]
```

**Regel 1 — Status in Klartext:**

FALSCH: "Executing TDD cycle: red→green→refactor on auth module"
RICHTIG: "Ich schreibe jetzt den Login-Code und teste ob er funktioniert."

FALSCH: "Running self-verification against section acceptance criteria"
RICHTIG: "Ich prüfe ob das was ich gebaut habe auch wirklich das tut was geplant war."

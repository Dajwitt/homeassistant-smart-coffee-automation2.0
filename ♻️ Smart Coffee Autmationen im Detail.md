# ♻️ **Smart Coffee Autmationen im Detail**

Diese Seite erklärt im Detail alle Automationen, die das Herzstück dieses Projekts bilden. Jede Automation ist über Blueprints realisiert und basiert auf klar definierten Helfern, Sensoren und Zustandsabfragen. Ziel ist eine vollautomatische Steuerung und Auswertung der Kaffeemaschinenaktivität. Alle Blueprints sind miteinander verzahnt und greifen über Hilfsentitäten (Booleans, Zahlen, Timer) ineinander – für ein stabiles und zuverlässiges System.

---

## 🌐 Übersicht

**Folgende Automationen sind im Projekt enthalten:**

1. 😀 Spülvorgang erkennen
2. ☕️ Zubereitung erkennen
3. 🍵 Tassengröße erkennen nach Zubereitung
4. 💧 Wassertank-Zähler zurücksetzen
5. ⏱️ Timer & Abschaltung

---

## 😀 1. Spülvorgang erkennen

### Funktion

Diese Automation erkennt automatisch, wenn die Kaffeemaschine nach dem Einschalten einen Spülvorgang durchführt (typisch bei vielen Vollautomaten). Dadurch wird vermieden, dass diese Phase fälschlich als "Zubereitung" erkannt und gezählt wird.

### Ablauf

- Startet, wenn der Stromverbrauch **über 500 W** liegt.
- Bedingung: Beide Timer (Standby-Vorwarnung und Idle) müssen `idle` sein (d. h. keine laufende Zubereitung).
- Setzt den Boolean `spuelvorgang_aktiv` auf **true**.
- Nach **55 Sekunden** wird dieser Boolean automatisch wieder auf **false** gesetzt.
- Gleichzeitig wird der Abschalt-Timer erneut gestartet, um den Energiesparzyklus aufrechtzuerhalten.

### Hintergrund

Wird diese Phase nicht korrekt erkannt, kann es zu fehlerhaften Auswertungen in der Statistik kommen.

---

## ☕️ 2. Zubereitung erkennen

### Funktion

Zählt jede tatsächliche Kaffeezubereitung – basierend auf Stromverbrauch – und unterscheidet später zwischen einer oder zwei Tassen.

### Ablauf

- Trigger: **Leistung > 1000 W**.
- Bedingung: `spuelvorgang_aktiv` ist **aus** (mindestens 5 Sekunden lang).
- Innerhalb eines Loops wird **jede Sekunde die Zubereitungsdauer** gezählt.
- Nach dem Brühvorgang wird diese Dauer gespeichert.
- Sicherheitsabfrage (erneut): Nur wenn `spuelvorgang_aktiv` **nicht aktiv** ist, erfolgt die Auswertung:
  - **15–59 Sek.** → 1 Tasse
  - **60–90 Sek.** → 2 Tassen
- Ergebnis: Zubereitungszähler wird erhöht und der Boolean `zubereitung_erkannt_statistik` auf `on` gesetzt (für statistische Anzeige im Dashboard).
- Nach 10 Sekunden: Zurücksetzen aller Zwischenspeicher.

### Besonderheit

Zwei Sicherheitsabfragen stellen sicher, dass Spülvorgänge **niemals** als Zubereitung gezählt werden.

---

## 🍵 3. Tassengröße erkennen nach Zubereitung

### Funktion

Analysiert die in der vorherigen Automation gespeicherte Zubereitungsdauer und bestimmt automatisch, ob **eine oder zwei Tassen** zubereitet wurden.

### Ablauf

- Trigger: Neue Zubereitungsdauer wurde gespeichert.
- Wenn `spuelvorgang_aktiv` ist → **Abbruch**.
- Daueranalyse:
  - **15–59 Sek.** → Counter `counter.tasse_1x` wird erhöht, Anzeige: "1 Tasse"
  - **60+ Sek.** → Counter `counter.tasse_2x` wird erhöht, Anzeige: "2 Tassen"
- Ergebnis wird im Dashboard dargestellt (inkl. Farbcode, Text, Zähler).

---

## 💧 4. Wassertank-Zähler zurücksetzen

### Funktion

Zählt den geschätzten Wasserverbrauch basierend auf den Brühvorgängen. Wenn der Wasserstandssensor meldet, dass der Tank leer ist, wird der Zähler automatisch zurückgesetzt.

### Ablauf

- Trigger: Wassersensor schaltet auf `off` (leer).
- Aktion:
  - Sprachbenachrichtigung wird abgespielt.
  - Wasserzähler wird auf **0** gesetzt.
  - Der Boolean `reset_erkannt` wird für das Dashboard aktiviert und nach kurzer Zeit wieder deaktiviert.

### Ziel

Ein realistisches Tracking des Wasserverbrauchs, ohne manuelles Zählerzurücksetzen. Nur ein **Sensorkontakt am Wassertank** ist notwendig.

---

## ⏱️ 5. Timer & Abschaltung

### Funktion

Schaltet die Kaffeemaschine automatisch ab, wenn **längere Zeit keine Nutzung** erfolgt. Dabei wird bewusst der Spülvorgang vermieden, der beim normalen Ausschalten auftritt.

### Ablauf

- **Timer 1: Abschalt-Timer (z. B. 40 Minuten)**
  - Wird nach jeder Zubereitung gestartet
- **Timer 2: Vorwarn-Timer (z. B. 15 Minuten)**
  - Wird nach Ablauf von Timer 1 gestartet
- Wenn Timer 2 ebenfalls abläuft:
  - Kaffeemaschine wird **kurz aus- und wieder eingeschaltet**
  - Dadurch wird KEIN Spülvorgang ausgelöst

### Ziel

Automatische Abschaltung **ohne Spülen** zur Schonung der Maschine und Reduktion unnötiger Laufzeiten.

---

## 🔗 Hinweise zur Nutzung

- Alle Automationen sind als **Blueprints** verfügbar.
- Das Zusammenspiel funktioniert nur, wenn **alle Helfer, Sensoren und Timer exakt übernommen werden** (siehe Projektanleitung).
- Besonders wichtig:
  - `input_boolean.kaffeemaschine_spuelvorgang_aktiv`
  - `input_number.kaffeemaschine_zubereitungsdauer`
  - `counter.kaffeemaschine_zubereitungen`
  - `sensor.kaffeemaschine_power` (Power-Messung)

**Bitte folge exakt der Anleitung, damit alle Verknüpfungen zwischen den Automationen korrekt greifen.**

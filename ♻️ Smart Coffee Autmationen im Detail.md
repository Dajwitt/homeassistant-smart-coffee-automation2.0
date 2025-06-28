# ♻️ **Smart Coffee Autmationen im Detail**

Diese Seite erklärt im Detail alle Automationen, die das Herzstück dieses Projekts bilden. Jede Automation ist über Blueprints realisiert und basiert auf klar definierten Helfern, Sensoren und Zustandsabfragen. Ziel ist eine vollautomatische Steuerung und Auswertung der Kaffeemaschinenaktivität. Alle Blueprints sind miteinander verzahnt und greifen über Hilfsentitäten (Booleans, Zahlen, Timer) ineinander – für ein stabiles und zuverlässiges System.

> 📌 Hinweis: Alle Einstellungen sind voreingestellt und können auf deine Maschine angepasst werden!
---

## 🌐 Übersicht

**Folgende Automationen sind im Projekt enthalten:**

1. 🌀 Spülvorgang erkennen
2. ☕️ Zubereitung erkennen
3. 🍵 Tassengröße erkennen nach Zubereitung
4. 💧 Wassertank-Zähler zurücksetzen
5. ⏱️ Timer & Abschaltung

---

## 🌀 1. Spülvorgang erkennen

### Funktion

Diese Automation erkennt automatisch, wenn die Kaffeemaschine nach dem Einschalten einen Spülvorgang durchführt (typisch bei vielen Vollautomaten). Dadurch wird vermieden, dass diese Phase fälschlich als "Zubereitung" erkannt und gezählt wird.

### Ablauf

- Startet, wenn der Stromverbrauch **über 500 W** liegt.
- Bedingung: Beide Timer (Standby-Vorwarnung und Idle) müssen `idle` sein 
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
  - **15–59 Sek.** → Counter `Normale Tasse` wird erhöht
  - **60+ Sek.** → Counter `Große Tasse` wird erhöht
- Ergebnis wird im Dashboard dargestellt
---

## 💧 4. Wassertank-Zähler zurücksetzen

### Funktion

Diese Automation überwacht den Kaffezubereitungs Zähler und wertet seinen Status aus. Sobald der Zähler über 5 steigt, löst die Automation eine Benachrichtigung aus, dass der Wasertank leer ist und startet einen 5 Minuten Timmer. In diesen 5 Minuten hast du genügend Zeit den Wassertank neu zu befüllen. Setzt du den Wassertank wieder ein, wird der Zubereitungszähler auf Null zurückgesetzt und im Dashboard wird 100 % angezeigt.

Solltest du den Wassertank nicht innerhalb der 5 Minuten Nachfüllen, schaltet sich die Maschine aus. Das ist eine weiter indirekte erinnerung, dass der Wassertank leer ist. Schaltest du die Maschine wieder ein und der Zubereitungszähler ist immer noch über 5 bekommst du eine weitere Benachrichtiging.

Du kannst jetzt trotzdem einen Kaffee zubereiten, aber deine Tasse wird vielleicht nicht ganz voll.

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
- **Wenn Timer 2 ebenfalls abläuft**
  - Kaffeemaschine wird **kurz aus- und wieder eingeschaltet**
  - Dadurch wird KEIN Spülvorgang ausgelöst

### Ziel

Automatische Abschaltung **ohne Spülen** Die Maschiene kann auch nach dem Spülen und auomatischen Ausschalten vom Strom getrennt werden.

---

## 🔗 Hinweise zur Nutzung

- Alle Automationen sind als **Blueprints** verfügbar.
- Das Zusammenspiel funktioniert nur, wenn **alle Helfer, Sensoren und Timer exakt übernommen werden**

**Bitte folge exakt der Anleitung, damit alle Verknüpfungen zwischen den Automationen korrekt greifen.**

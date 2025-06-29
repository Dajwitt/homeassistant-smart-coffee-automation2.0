# ♻️ Smart Coffee Automationen im Detail

Diese Seite erklärt detailliert die Automationen, die das Herzstück des **Smart Coffee Automation**-Projekts bilden. Jede Automation ist als Blueprint verfügbar und basiert auf klar definierten Helfern, Sensoren und Zustandsabfragen. Das Ziel ist eine vollautomatische Steuerung und detaillierte Auswertung der Kaffeemaschinenaktivität. Alle Blueprints sind miteinander verzahnt und greifen über Hilfsentitäten (Booleans, Zahlen, Timer) ineinander, um ein stabiles und zuverlässiges System zu gewährleisten.

> 📌 **Wichtiger Hinweis:** Alle Einstellungen sind voreingestellt, können aber auf die spezifischen Gegebenheiten deiner Kaffeemaschine angepasst werden!

---

## 🌐 Übersicht der Automationen

**Das Projekt umfasst die folgenden Kern-Automationen:**

1.  🌀 Spülvorgang erkennen
2.  ☕️ Zubereitung erkennen
3.  🍵 Tassengröße nach Zubereitung erkennen
4.  💧 Wassertank-Zähler zurücksetzen & überwachen
5.  ⏱️ Timer-gesteuerte Abschaltung

---

## 🌀 1. Spülvorgang erkennen

### Funktion

Diese Automation ist entscheidend, um zu vermeiden, dass die automatischen Spülvorgänge deiner Kaffeemaschine beim Einschalten fälschlicherweise als Kaffeezubereitung erkannt und gezählt werden.

### Ablauf

* **Auslöser:** Die Automation startet, wenn der Stromverbrauch der Kaffeemaschine **über 500 W** liegt.
* **Bedingung:** Beide Abschalt-Timer (`Standby-Vorwarnung` und `Idle-Ausschalt-Timer`) müssen den Status `idle` (inaktiv) haben. Dies stellt sicher, dass der Stromanstieg nicht von einer echten Kaffeezubereitung herrührt.
* **Aktion:** Der Hilfs-Boolean `spuelvorgang_aktiv` wird auf **`on`** gesetzt.
* **Beendigung:** Nach **55 Sekunden** wird dieser Boolean automatisch wieder auf **`off`** zurückgesetzt.
* **Timer-Reset:** Gleichzeitig wird der `Idle-Ausschalt-Timer` erneut gestartet, um den Energiesparzyklus aufrechtzuerhalten und die Maschine nach einer gewissen Inaktivität wieder abzuschalten.

### Hintergrund

Eine korrekte Erkennung des Spülvorgangs ist essenziell, um die Genauigkeit deiner Kaffee-Statistiken zu gewährleisten und fehlerhafte Zählungen zu verhindern.

---

## ☕️ 2. Zubereitung erkennen

### Funktion

Diese Automation zählt jede tatsächliche Kaffeezubereitung basierend auf dem Stromverbrauch deiner Maschine. Sie bereitet zudem die Daten vor, um später zwischen einer oder zwei Tassen zu unterscheiden.

### Ablauf

* **Auslöser:** Die Automation wird ausgelöst, sobald die **Leistungsaufnahme über 1000 W** steigt.
* **Bedingung:** Der Boolean `spuelvorgang_aktiv` muss für mindestens **5 Sekunden `off`** sein. Dies ist eine wichtige Sicherheitsabfrage, um sicherzustellen, dass kein Spülvorgang fälschlicherweise als Zubereitung gezählt wird.
* **Zählung der Brühdauer:** Innerhalb einer Schleife wird **jede Sekunde die Dauer der Kaffeezubereitung** erfasst.
* **Speicherung:** Nach Abschluss des Brühvorgangs wird diese gemessene Dauer im Helfer `kaffeemaschine_letzte_bruehdauer` gespeichert.
* **Zweite Sicherheitsabfrage:** Es erfolgt eine erneute Prüfung, ob `spuelvorgang_aktiv` **nicht aktiv** ist. Nur wenn diese Bedingung erfüllt ist, erfolgt die weitere Auswertung:
    * **15–59 Sekunden Brühdauer:** Wird als 1 Tasse gewertet.
    * **60–90 Sekunden Brühdauer:** Wird als 2 Tassen gewertet.
* **Statistik-Update:** Der Gesamt-Zubereitungszähler wird erhöht, und der Boolean `zubereitung_erkannt_statistik` wird auf `on` gesetzt, um die aktuelle Zubereitung im Dashboard für Statistiken anzuzeigen.
* **Zwischenspeicher-Reset:** Nach 10 Sekunden werden alle temporären Zwischenspeicher zurückgesetzt.

### Besonderheit

Zwei voneinander unabhängige Sicherheitsabfragen stellen sicher, dass Spülvorgänge **niemals** als tatsächliche Kaffeezubereitungen gezählt werden, was die Zuverlässigkeit deiner Statistiken erheblich verbessert.

---

## 🍵 3. Tassengröße nach Zubereitung erkennen

### Funktion

Diese Automation analysiert die von der vorherigen Automation (`Zubereitung erkennen`) gespeicherte Brühdauer und bestimmt automatisch, ob **eine oder zwei Tassen** Kaffee zubereitet wurden.

### Ablauf

* **Auslöser:** Die Automation startet, sobald eine neue Zubereitungsdauer im Helfer `kaffeemaschine_letzte_bruehdauer` gespeichert wurde.
* **Bedingung:** Falls der Boolean `spuelvorgang_aktiv` auf `true` steht, wird die Automation **sofort abgebrochen**, um Fehlzählungen zu vermeiden.
* **Daueranalyse & Zählung:**
    * Wenn die Brühdauer zwischen **15 und 59 Sekunden** liegt, wird der Counter `Normale Tasse` um eins erhöht.
    * Wenn die Brühdauer **60 Sekunden oder länger** ist, wird der Counter `Große Tasse` um eins erhöht.
* **Darstellung:** Das Ergebnis dieser Zählung wird im Dashboard übersichtlich dargestellt.

---

## 💧 4. Wassertank-Zähler zurücksetzen & überwachen

### Funktion

Diese Automation überwacht den Kaffeezubereitungs-Zähler und leitet daraus den Füllstand des Wassertanks ab. Sie ist darauf ausgelegt, dich proaktiv an das Nachfüllen zu erinnern und die Zählung nach dem Befüllen automatisch zurückzusetzen.

### Ablauf

* **Zählerüberwachung & Benachrichtigung:** Sobald der Kaffeezubereitungs-Zähler über einen vordefinierten Schwellenwert (z.B. 5 Tassen, anpassbar an deine Maschine) steigt, wird ein 5-Minuten-Timer (`kaffeemaschine_wasser_nachfuell_prompt`) gestartet. Gleichzeitig wird ein Trigger (`sprachbenachrichtigung_ausloeser_wassertank`) für Benachrichtigungen aktiviert, der signalisiert, dass der Wassertank wahrscheinlich leer ist.
    * Du hast nun **5 Minuten Zeit**, den Wassertank zu befüllen.
* **Wassertank befüllt:** Sobald du den Wassertank wieder einsetzt (erkannt durch den Türkontakt am Wassertank), wird der Zubereitungszähler (`counter.kaffeemaschine_zubereitungen`) auf Null zurückgesetzt. Im Dashboard wird dann wieder 100 % Füllstand angezeigt.
* **Automatische Abschaltung bei Nicht-Befüllen:** Solltest du den Wassertank nicht innerhalb der 5 Minuten nachfüllen, schaltet sich die Kaffeemaschine automatisch aus. Dies dient als weitere, indirekte Erinnerung, dass der Wassertank leer ist.
* **Erneute Benachrichtigung:** Wenn du die Maschine wieder einschaltest und der Zubereitungszähler immer noch über dem Schwellenwert liegt, erhältst du eine weitere Benachrichtigung.
* **Trotzdem Kaffee zubereiten:** Auch wenn der Tankzähler anzeigt, dass der Tank leer ist, kannst du weiterhin einen Kaffee zubereiten. Beachte jedoch, dass deine Tasse möglicherweise nicht ganz voll wird, wenn tatsächlich zu wenig Wasser im Tank ist.

### Ziel

Ein realistisches Tracking des Wasserverbrauchs und eine intelligente Erinnerungsfunktion, die ein manuelles Zählerzurücksetzen überflüssig macht. Hierfür ist lediglich ein **Sensorkontakt am Wassertank** notwendig.

---

## ⏱️ 5. Timer-gesteuerte Abschaltung

### Funktion

Diese Automation schaltet die Kaffeemaschine automatisch ab, wenn **längere Zeit keine Nutzung** erfolgt. Dabei wird bewusst der Spülvorgang vermieden, der beim normalen Ausschalten vieler Kaffeemaschinen auftritt.

### Ablauf

* **Timer 1: Abschalt-Timer (z.B. 40 Minuten)**
    * Dieser Timer wird nach jeder Kaffeezubereitung oder jedem Spülvorgang gestartet.
    * Läuft dieser Timer ab, wird ein Helfer (Trigger) für 5 Sekunden eingeschaltet, der für Benachrichtigungen genutzt werden kann (z.B. "Die Kaffeemaschine geht bald in den Standby-Modus").
* **Timer 2: Vorwarn-Timer (z.B. 15 Minuten)**
    * Dieser Timer wird gestartet, sobald Timer 1 abgelaufen ist.
* **Ende des Zyklus:** Wenn auch Timer 2 abläuft:
    * Die Kaffeemaschine wird **kurz aus- und sofort wieder eingeschaltet**.
    * Durch dieses schnelle Umschalten wird **KEIN Spülvorgang** ausgelöst.

### Hinweis zur Anpassung

Ich habe mich bewusst dafür entschieden, das Spülen vor der automatischen Abschaltung zu verhindern. Solltest du jedoch wünschen, dass die Maschine *nach* dem Spülen und automatischen Ausschalten vom Strom getrennt wird, kannst du die Gesamtdauer beider Timer so einstellen, dass die Abschaltung nach dem Spülvorgang greift.

### Ziel

Eine effiziente und automatische Abschaltung der Maschine **ohne unnötiges Spülen**.

---

## 🔗 Hinweise zur Nutzung

* Alle Automationen dieses Projekts sind als **Blueprints** verfügbar, was den Import und die Konfiguration in Home Assistant erheblich vereinfacht.
* Das reibungslose Zusammenspiel aller Funktionen ist nur gewährleistet, wenn **alle Helfer, Sensoren und Automationen exakt wie beschrieben übernommen werden**.

**Bitte folge exakt dieser Anleitung, damit alle Verknüpfungen zwischen den Automationen korrekt greifen und dein Smart Coffee System zuverlässig funktioniert.**

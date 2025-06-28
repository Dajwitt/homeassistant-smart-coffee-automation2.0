## **💬 Smart Coffee** FAQ

---

### Warum gibt es zwei Timer und welche Funktion haben sie?

Bevor du die Timer konfigurierst, finde zunächst heraus, **wann sich deine Kaffeemaschine nach der letzten Zubereitung automatisch in den Standby-Modus versetzt**. Diese Zeit teilst du anschließend auf zwei Timer auf – je nachdem, ob du das automatische Spülen **verhindern** oder **zulassen** möchtest.

📌 **Beispiel: Deine Maschine schaltet sich nach 60 Minuten automatisch ab:**

- **Spülen verhindern:**  
   → Timer 1: 40 Minuten + Timer 2: 15 Minuten = 55 Minuten  
   (Die Maschine wird kurz vor dem Spülen abgeschaltet.)
- **Spülen zulassen:**  
   → Timer 1: 50 Minuten + Timer 2: 15 Minuten = 65 Minuten  
   (Die Maschine schaltet nach dem Spülen ab.)

💡 Tipp:  
 Nach Ablauf des ersten Timers (z. B. nach 40 Minuten) kannst du dich zusätzlich **benachrichtigen lassen**, dass die Maschine bald ausgehen wird.

---


### Soll ich das automatische Spülen verhindern?

Das hängt von deinem Nutzerverhalten ab. Ich persönlich **verzichte auf das Spülen vor dem Abschalten**, weil mein Wassertank eher klein ist – so bekomme ich noch eine Tasse mehr, bevor er leer ist.

✅ **Wenn du das Spülen zulassen möchtest**, dann stelle deine Timer so ein, dass die Abschaltung **nach dem Spülvorgang** erfolgt (siehe vorherige Frage).

---


### Warum spült meine Maschine direkt nach dem 3-Sekunden-Reset?


Nicht alle Kaffeevollautomaten verhalten sich gleich. Die Reaktion nach einem kurzen **Ein-/Ausschaltvorgang (z. B. 3 Sekunden)** hängt vom Modell ab:

- ☕ **Manche Maschinen** bleiben nach dem kurzen Ausschalten zuverlässig im Standby-Modus.
- ⚠️ **Andere Modelle** führen beim Wiedereinschalten sofort einen **Spülvorgang** aus – unabhängig davon, ob zuvor bereits gespült wurde.

🔧 **Lösungsmöglichkeiten:**

- **Erhöhe die Dauer**, in der die Maschine ausgeschaltet bleibt (z. B. 5–10 Sekunden).
- **Testen:** Finde heraus, ob dein Modell überhaupt durch kurzes Aus- und Einschalten zuverlässig abgeschaltet bleibt.
- **Alternative:** Du kannst das automatische Wiedereinschalten **ganz weglassen**, sodass du die Maschine manuell einschalten musst, wenn du wieder Kaffee zubereiten möchtest.

💡 Jeder Maschinentyp reagiert etwas anders – passe daher die Automation an das Verhalten deiner Maschine an.

---


### Wie übernehme ich die Kontrolle über die Blueprint-Automation?

Sobald du die Blueprint **importiert, ausgefüllt und gespeichert** hast, gehe wie folgt vor:

1. Öffne **Einstellungen → Automationen & Szenen**
2. Suche die Automation **„Timer & Abschaltung“**
3. Klicke oben rechts auf die **drei Punkte (⋮)**
4. Wähle **„Kontrolle übernehmen“** und bestätige mit **Ja**
5. Danach nochmal **speichern**

Nun kannst du die Automation manuell bearbeiten.

---

### Wo stelle ich die Benachrichtigungen ein?


#### ☕ Automation: **Timer & Abschaltung**

Unter **Option 2 – „Wenn ausgelöst durch 40 Minuten abgelaufen“** kannst du eine Benachrichtigung hinzufügen, die dich informiert, dass sich die Maschine **bald automatisch abschaltet**.

👉 So richtest du sie ein:

1. Öffne die Automation **Timer & Abschaltung**
2. Scrolle zur **Aktionenliste**
3. Klicke auf **„Aktion hinzufügen“**
4. Wähle deine bevorzugte Benachrichtigungsmethode (z. B. **App**, **Sprachausgabe**, **Push-Nachricht**)

#### 💧 Automation: **Wassertank überwachen – Zähler zurücksetzen**

Hier kannst du unter:

- **Option 2 – Wenn ausgelöst durch** `zaehler_ueber_5`
- **Option 6 – z. B. bei erkanntem Verbrauch mit leerem Tank**

eine Benachrichtigung einrichten, die dich warnt, dass der **Wassertank leer** ist.

👉 Auch hier einfach eine Aktion hinzufügen und die gewünschte Methode wählen.

💡 **Hinweis:**  
Benachrichtigungen lassen sich **ganz flexibel auch in anderen Automationen integrieren** – je nach Bedarf. Deiner Kreativität sind dabei keine Grenzen gesetzt.

---

### Wie passe ich den Füllstand an meine Maschine an?

Der Füllstand des Wassertanks wird **automatisch berechnet** – für Prozent und verbleibende Tassen.
Du musst in beiden Sensoren nur **eine einzige Zeile** anpassen:

```jinja2
{% set max_tassen = 5 %}
```

➡️ Ersetze die **5** durch die maximale Anzahl an Kaffeezubereitungen, die deine Maschine mit einer Tankfüllung schafft..

💡 Beispiel: Für eine Maschine mit 7 Tassen:

```jinja2
{% set max_tassen = 7 %}
```

---

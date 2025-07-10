### ⏱ Timer & Abschaltung und 💧 Wassertank überwachen – Zähler zurücksetzen

### 🐞 Problem

Wird in der Automation **💧 Wassertank überwachen – Zähler zurücksetzen** die eingestellte Anzahl an Kaffeezubereitungen überschritten, startet automatisch der **Erinnerungs-Timer zum Wasser nachfüllen**. Gleichzeitig laufen die beiden Timer aus der Automation **⏱ Timer & Abschaltung** (Standby-Vorwarnung und Idle-Ausschaltung) wie gewohnt weiter.

Sobald nun in der **💧 Wassertank**-Automation der **Erinnerungs-Timer abläuft** und die beiden anderen Timer (Standby-Vorwarnung und Idle-Ausschaltung) **abgebrochen werden**, wird **trotzdem** in der Automation **⏱ Timer & Abschaltung** die **Sprachbenachrichtigung** „Die Maschine schaltet bald aus“ ausgelöst.  
  
Dies geschieht, weil der Trigger „**Boolesche Eingabe: Einschalten**“ (Sprachbenachrichtigung Vorwarnung) aktiv ist.

➡️ In diesem Fall ist die Benachrichtigung **nicht sinnvoll** und wird im Alltag schnell als **störend** wahrgenommen.

---

### ✅ Lösung

Ein zusätzlicher Helfer verhindert die unnötige Benachrichtigung zuverlässig.

#### 🧩 Schritt 1 – Helfer erstellen

```
input_boolean:
  helfer_timer_abbrechen:
    name: Helfer Timer abbrechen
```

---

#### 🛠 Schritt 2 – Automation ⏱ Timer & Abschaltung anpassen

- Füge den neuen Helfer als **Bedingung in Option 2** hinzu:

  > Nur wenn `input_boolean.helfer_timer_abbrechen` auf `off` steht, darf die Benachrichtigung gesendet werden.

📸 Beispiel:  
 ![Screenshot 2025-07-10 09.50.05.png](.attachments.3972/Screenshot%202025-07-10%2009.50.05.png)

---

#### 🛠 Schritt 3 – Automation 💧 Wassertank überwachen – Zähler zurücksetzen anpassen

Der schnellste Weg: Nutze die optimierte 📥 **Blueprint**  [🔗 Link zur Blueprint](https://gist.github.com/Dajwitt/24050e09d1b8b191cce9dfcfa0660ccf)

**Bearbeite Option 4 :** 

- Nutze folgenden YAML-Code
- Passe den Schalter der Maschine an dein Setup an.

---

```
      - conditions:
          - condition: trigger
            id: wasser_timer_abgelaufen
        sequence:
          - action: input_boolean.turn_on
            metadata: {}
            data: {}
            target:
              entity_id: input_boolean.helfer_timer_abbrechen
          - delay:
              hours: 0
              minutes: 0
              seconds: 0
              milliseconds: 500
          - action: timer.cancel
            metadata: {}
            data: {}
            target:
              entity_id: timer.kaffeemaschine_standby_vorwarnung
          - delay:
              hours: 0
              minutes: 0
              seconds: 0
              milliseconds: 500
          - action: timer.cancel
            metadata: {}
            data: {}
            target:
              entity_id: timer.kaffeemaschine_idle_ausschalt_timer
          - action: switch.turn_off
            metadata: {}
            data: {}
            target:
              entity_id: switch.kaffeemaschine_led_switch_0
          - delay:
              hours: 0
              minutes: 0
              seconds: 2
              milliseconds: 0
          - action: switch.turn_on
            metadata: {}
            data: {}
            target:
              entity_id: switch.kaffeemaschine_led_switch_0
          - action: input_boolean.turn_off
            metadata: {}
            data: {}
            target:
              entity_id: input_boolean.helfer_timer_abbrechen
```

![image (2).png](.attachments.3972/image%20%282%29.png)
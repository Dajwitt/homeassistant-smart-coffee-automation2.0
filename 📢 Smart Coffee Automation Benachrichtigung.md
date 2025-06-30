# 📢 Benachrichtigungen für Warnungen und Hinweise

  
🧩 **Funktion:** Zentrale Drehscheibe für Benachrichtigungen, ausgelöst durch andere Automationen. 

🎯 Das Ziel ist eine **flexible und minimalistische** Benachrichtigungsstrategie, bei der du entscheidest, ob und wie du informiert wirst.

---

## 🔄 Aktuelle Integration

Die in diesem Projekt vorgesehenen Standard-Benachrichtigungen sind derzeit nur in folgenden Kern-Automationen integriert:

- ⏳ **Timer & Abschaltung** 
  - Vorwarnung, bevor die Kaffeemaschine in den Standby-Modus wechselt.
- 💧 **Wassertank überwachen & Zähler zurücksetzen**
  - Erinnerung zum Nachfüllen des Wassers.

---

## 🧩 Funktionsweise

- **🔔 Auslöser (Trigger):**
  - Bestimmte `input_boolean`-Helfer wie  
    `input_boolean.sprachbenachrichtigung_ausloeser_wassertank`  
    werden von zwei Automationen auf `on` gesetzt → signalisiert, dass eine Benachrichtigung gesendet werden soll.
- **🎬 Reaktion (Aktion):**
  - Die zentrale Benachrichtigungs-Automation sendet je nach aktiviertem `input_boolean` eine Nachricht über den konfigurierten Benachrichtigungsdienst.

---

## 🛠️ Anpassung & Flexibilität

Du hast **volle Kontrolle** über die Benachrichtigungen:

- ✅ **Optional:**
  - Ignoriere die `input_boolean`-Trigger oder deaktiviere die Benachrichtigungs-Automation, wenn du keine Benachrichtigungen erhalten möchtest
- ➕ **Erweiterbar:**
  - Weitere Ereignisse kannst du leicht hinzufügen – einfach neue `input_boolean`-Trigger und Aktionen ergänzen.
- 🧷 **Direkt integrierbar:**
  - Alternativ kannst du Benachrichtigungen **direkt in jede Automation** einbauen (z. B. „Spülvorgang erkennen“, „Kaffeezubereitung erkennen“).
- 📡 **Geräteunabhängig:**  
  Standardmäßig wird Alexa (`notify.alexa_media_echo_wohnzimmer`) genutzt – du kannst aber jeden anderen Dienst wie:
  - 📱 Companion App
  - 📨 E-Mail
  - 💬 Telegram
  - 🖥️ Dashboard (persistente Benachrichtigungen)

  verwenden. Einfach `notify.` und `target` anpassen.

---

## ⬇️ Automation importieren

📥 **So geht's:**

1. Kopiere den YAML-Code unten.
2. In Home Assistant:  
   `Einstellungen` → `Automationen & Szenen` → `Automation hinzufügen`
3. Oben rechts auf die drei Punkte **(⋮)** klicken → **In YAML bearbeiten**
4. YAML-Code einfügen 
5. Benachrichtigungsdienst anpassen und speichern ✅

---

## ✏️ YAML-Code der zentralen Benachrichtigung

```yaml
alias: Benachrichtigung für Vorwarung und Wassertank
description: ""
triggers:
  - trigger: state
    entity_id:
      - input_boolean.sprachbenachrichtigung_ausloeser_vorwarnung
    to: "on"
    id: Vorwarnung
  - trigger: state
    entity_id:
      - input_boolean.sprachbenachrichtigung_ausloeser_wassertank
    to: "on"
    id: Wassertank
conditions: []
actions:
  - choose:
      - conditions:
          - condition: trigger
            id:
              - Vorwarnung
        sequence:
          - action: notify.alexa_media_echo_wohnzimmer
            data:
              message: >-
                Die Kaffeemaschine geht gleich aus. Jetzt wär ein guter Moment
                für ’nen letzten Kaffee!
              target: media_player.echo_wohnzimmer
              data:
                type: announce
                method: all
      - conditions:
          - condition: trigger
            id:
              - Wassertank
        sequence:
          - action: notify.alexa_media_echo_wohnzimmer
            data:
              message: >-
                Oh oh! Das Wasser wird knapp – bitte gleich nachfüllen, sonst
                gibt’s keinen Kaffee mehr!
              target: media_player.echo_wohnzimmer
              data:
                type: announce
                method: all
mode: single
```
## Warum gibt es zwei Timer und welche Funktion haben sie?

Bevor du die Timer konfigurierst, finde zunächst heraus, wann sich deine Kaffeemaschine nach der letzten Zubereitung automatisch in den Standby-Modus versetzt. Diese Zeit teilst du anschließend auf zwei Timer auf – je nachdem, ob du das automatische Spülen verhindern oder zulassen möchtest.

## 📌 Beispiel: Deine Maschine schaltet sich nach 60 Minuten automatisch ab:

**Spülen verhindern:**

→ Timer 1: 40 Minuten + Timer 2: 15 Minuten = 55 Minuten
(Die Maschine wird kurz vor dem Spülen abgeschaltet.)

**Spülen zulassen:**

→ Timer 1: 50 Minuten + Timer 2: 15 Minuten = 65 Minuten
(Die Maschine schaltet nach dem Spülen ab.)

---

Die beiden Helfer **Sprachbenachrichtigung auslösen Wassertank** und **Sprachbenachrichtigung auslösen Vorwarnung** dienen als Auslöser für Benachrichtigungen und sind bereits in die Automationen eingebunden. Du kannst damit **selbst entscheiden**, wie und auf welchem Weg du benachrichtigt werden möchtest – zum Beispiel per App, Sprachausgabe oder Nachricht.

Damit dir die Benachrichtigungen tatsächlich zugestellt werden, musst du **zusätzlich eine eigene Automation erstellen**. 

**Eine Anleitung dazu findest du hier:** 📢  [Smart Coffee Automation Benachrichtigung](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%93%A2%20Smart%20Coffee%20Automation%20Benachrichtigung.md)

---

> ⚠️  Die drei Timer (`standby_vorwarnung`, `idle_shutdown`, `debug_timer`) **müssen in der** `configuration.yaml` **gepflegt werden**, da diese Timer nach der Erstellung **nicht über die UI bearbeitet** werden können. Passe **duration:** der Timer nach deinen Bedürfnissen an. Es wird empfohlen die Timer später über die die UI anzulegen, da diese beim Neustart von Home Assistant nicht abbrechen und weiter laufen!

### 🧾 Anleitung zur Integration der Helfer:

  1. Öffne deine Home Assistant `configuration.yaml`.
  2. Füge den folgenden Block hinzu – entweder am Ende oder unter dem Abschnitt `input_boolean`, `input_number`, `input_text`, `counter`, `timer`, wenn du ihn schon verwendest:

```
# 📦 Smart Coffee Automatisierung: Helfer
input_boolean:

  kaffeemaschine_spuelvorgang_aktiv:
    name: Spülvorgang aktiv
    icon: mdi:water-sync

  zubereitung_erkannt_statistik:
    name: Kaffeezubereitung erkannt statistik
    icon: mdi:coffee-maker-check-outline

  sprachbenachrichtigung_ausloeser_wassertank:
    name: Sprachbenachrichtigung auslösen Wassertank
    icon: mdi:message-bulleted
    
  sprachbenachrichtigung_ausloeser_vorwarnung:
    name: Sprachbenachrichtigung auslösen Vorwarnung
    icon: mdi:message-bulleted

input_number:

  kaffeemaschine_bruehleistung_dauer:
    name: Brühdauer aktuelle Zubereitung
    icon: mdi:clock-outline
    min: 0
    max: 300
    step: 1
    unit_of_measurement: s

  kaffeemaschine_letzte_bruehdauer:
    name: Letzte Brühdauer
    icon: mdi:clock-time-three
    min: 0
    max: 300
    step: 1
    unit_of_measurement: s

input_text:
  kaffeemaschine_letzte_tassengroesse:
    name: Letzte Tassengröße
    icon: mdi:coffee

counter:

  kaffeemaschine_zubereitungen:
    name: Kaffeezubereitungen
    icon: mdi:coffee-maker

  kaffeemaschine_tasse_normal:
    name: Normale Tassen Kaffee
    icon: mdi:coffee

  kaffeemaschine_tasse_gross:
    name: Große Tassen Kaffee
    icon: mdi:coffee-outline

timer:

  kaffeemaschine_idle_ausschalt_timer:
    name: Ausschalt-Timer (Idle)
    duration: '00:40:00'
    icon: mdi:power

  kaffeemaschine_standby_vorwarnung:
    name: Standby-Vorwarnung
    duration: '00:15:00'
    icon: mdi:clock-alert-outline

  kaffeemaschine_wasser_nachfuell_prompt:
    name: Wasser nachfüllen Erinnerung
    duration: '00:05:00'
    icon: mdi:water-alert

```
--- 

**Bereit für den nächsten Schritt? ⚙ [Sensoren & Templates einfügen](https://github.com/Dajwitt/homeassistant-smart-coffee-automation3.0/blob/main/%E2%9A%99%20Smart%20Coffee%20Sensoren%20%26%20Templates.md#anleitung-sensoren--templates-korrekt-einf%C3%BCgen)**


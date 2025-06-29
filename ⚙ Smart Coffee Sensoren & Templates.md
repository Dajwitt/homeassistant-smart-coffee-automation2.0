## Anleitung: Sensoren & Templates korrekt einfügen

Diese Datei enthält alle notwendigen Sensoren und Templates, die für das reibungslose Funktionieren deiner **Home Assistant Smart Coffee Automation** benötigt werden. Es ist entscheidend, dass diese Komponenten **exakt wie beschrieben** in deine `configuration.yaml` Datei eingefügt werden, um die Kompatibilität mit allen Automationen, Blueprints und dem Dashboard sicherzustellen.

---

## ⚠️ Wichtige Hinweise zur Konfiguration

Bitte beachte die folgenden essenziellen Punkte, um Fehler bei der Integration zu vermeiden:  
  
- Verwende ausschließlich **Leerzeichen** für die Einrückung, keine Tabulatoren.  
- Die Einrückung muss präzise sein (genau 2 Leerzeichen pro Hierarchieebene).  
- Die Schlüssel `template:` und `sensor:` dürfen in deiner `configuration.yaml` Datei **jeweils nur einmal** vorkommen. Sollten sie bereits existieren, erweitere die vorhandenen Abschnitte einfach um die hier gezeigten Einträge.

---

## 🧩 Schritt 1: Template-Sensoren einfügen  
  
Füge den folgenden Code-Abschnitt in den `template:`-Bereich deiner `configuration.yaml` ein:  
  
💡 **Hinweis zur Anpassung des Wassertanksensors:** 
Der Füllstand des Wassertanks wird automatisch in Prozent berechnet. Du musst lediglich **eine einzige Zeile** anpassen, um die maximale Kapazität deiner Maschine zu hinterlegen:

```jinja2
{% set max_tassen = 5 %}
```

➡️ Ersetze die **5** durch die maximale Anzahl an Kaffeezubereitungen, die deine Maschine mit einer Tankfüllung schafft.

```yaml
template:
  - sensor:
      - name: "Kaffeetank Füllstand Prozent"
        unique_id: kaffeetank_fuellstand_prozent
        unit_of_measurement: "%"
        device_class: battery
        icon: mdi:eye
        state: >
          {% set max_tassen = 5 %} 
          {% set counter = states('counter.kaffeemaschine_zubereitungen') | int(0) %}
          {% set prozent = 100 - ((counter / max_tassen) * 100) %}
          {{ [prozent, 0] | max | round(0) }}

```
---

## 📊 Schritt 2: Statistik-Sensoren einfügen

Füge diesen Abschnitt in den `sensor:`-Bereich deiner `configuration.yaml` ein:

```yaml
sensor:
  - platform: history_stats
    name: Kaffee heute
    unique_id: sensor.kaffee_heute
    entity_id: input_boolean.zubereitung_erkannt_statistik
    state: "on"
    type: count
    start: "{{ now().replace(hour=0, minute=0, second=0) }}"
    end: "{{ now() }}"

  - platform: history_stats
    name: Kaffee diese Woche
    unique_id: sensor.kaffee_diese_woche
    entity_id: input_boolean.zubereitung_erkannt_statistik
    state: "on"
    type: count
    start: >
      {% set today = now().replace(hour=0, minute=0, second=0) %}
      {% set weekday = today.weekday() %}
      {% set monday = today - timedelta(days=weekday) %}
      {{ monday }}
    end: "{{ now() }}"
```

💡 **Wichtiger Tipp:** Falls du bereits andere `sensor:`-Einträge in deiner `configuration.yaml` hast, **ergänze** diese einfach um die oben genannten Sensoren. Den `sensor:`-Abschnitt benötigst du in der gesamten Datei **nur einmal**.

⚠️ Starte Home Assistant neu!

---

## 💪 Warum ist diese exakte Übernahme so wichtig?

Diese speziellen Sensoren und Templates sind elementar für die Funktionalität deines Smart Coffee Systems, da sie:

- **nicht** verändert oder gekürzt werden dürfen, um die korrekte Funktion zu gewährleisten.
- **exakt** auf alle projektinternen Automationen abgestimmt sind.
- die unverzichtbare Grundlage für alle Statistiken und das gesamte Dashboard bilden.

Dein gesamtes System wird nur dann wie geplant funktionieren, wenn diese Konfigurationen **exakt so übernommen** werden.

---


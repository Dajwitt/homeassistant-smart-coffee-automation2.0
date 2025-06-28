## Anleitung: Sensoren & Templates korrekt einfügen

Damit alle Automationen, Blueprints und das Dashboard reibungslos funktionieren, **müssen die folgenden Sensoren und Templates exakt wie beschrieben in die configuration.yaml eingefügt werden**.

---

## ⚠️ Wichtige Hinweise

- Verwende ausschließlich **Leerzeichen**, keine Tabs!
- Die Einrückung muss exakt stimmen (2 Leerzeichen pro Ebene).
- `template:` und `sensor:` dürfen **nur je einmal** in der Datei vorkommen. Wenn bereits vorhanden, **einfach erweitern**.

---

## 🧩 Schritt 1: Template-Sensoren einfügen

Füge folgenden Abschnitt in den Bereich `template:` deiner `configuration.yaml` ein:
 
 💡 **Hinweis:** Der Füllstand des Wassertanks wird **automatisch berechnet** – für Prozent und verbleibende Tassen.
Du musst in beiden Sensoren nur **eine einzige Zeile** anpassen:

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
        state: >
          {% set max_tassen = 5 %} # Die 5 ersetzen
          {% set counter = states('counter.kaffeemaschine_zubereitungen') | int(0) %}
          {% set prozent = 100 - ((counter / max_tassen) * 100) %}
          {{ [prozent, 0] | max | round(0) }}

      - name: "Kaffeetank Füllstand Tassen"
        unique_id: kaffeetank_fuellstand_tassen
        unit_of_measurement: "Tassen"
        icon: mdi:coffee-outline
        state: >
          {% set max_tassen = 5 %} # Die 5 ersetzen 
          {% set counter = states('counter.kaffeemaschine_zubereitungen') | int(0) %}
          {% set remaining = max_tassen - counter %}
          {{ [remaining, 0] | max }}

```
---

## 📊 Schritt 2: Statistik-Sensoren einfügen

Füge diesen Abschnitt in den Bereich sensor: deiner configuration.yaml ein:

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

💡 Tipp: Wenn du schon andere **sensor:-Einträge** hast, **ergänze** diese einfach – du brauchst den Abschnitt sensor: **nur einmal** in der Datei.

---

### 💪 Warum ist das so wichtig?

Diese Sensoren und Templates …

- ❌ dürfen **nicht** verändert oder gekürzt werden
- ✅ sind exakt auf die Automationen abgestimmt
- ⚖️ sind die Grundlage für Statistiken und das Dashboard

Nur wenn diese exakt so übernommen werden, funktioniert dein gesamtes System wie geplant.

---


## Anleitung: Sensoren & Templates korrekt einfügen

Damit alle Automationen, Blueprints und das Dashboard reibungslos funktionieren, **müssen die folgenden Sensoren und Templates exakt wie beschrieben eingefügt werden**.

---

### ✏️ Schritt 1: Zwei Dateien anlegen

Lege in deinem  Home Assistant Config-Verzeichnis zwei Dateien an:

1. `template_sensors.yaml`  ✨ Enthält *alle* Template- und Binary-Sensoren
2. `history_stats.yaml`     ⚖️ Enthält *alle* Statistik-Sensoren (History Stats)

---

### ✏️ Schritt 2: Verweise in `configuration.yaml` eintragen

In deiner `configuration.yaml` fügst du folgenden Eintrag ein:

```yaml
sensor: !include history_stats.yaml
template: !include template_sensors.yaml
```

> ⚠️ Achte auf Einrückungen! Keine Tabs, nur Leerzeichen verwenden.

---

### 📃 Inhalt `template_sensors.yaml`

```yaml
template:
  - sensor:
      - name: "Kaffeetank Füllstand Prozent"
        unique_id: kaffeetank_fuellstand_prozent
        unit_of_measurement: "%"
        state: >
          {% set counter_value = states('counter.kaffeemaschine_zubereitungen') | int(0) %}
          {% set mapping = {
            0: 100,
            1: 83,
            2: 67,
            3: 50,
            4: 33,
            5: 17,
            6: 0
          } %}
          {{ mapping[counter_value] }}
        icon: mdi:water-percent

      - name: "Kaffeetank Füllstand Tassen"
        unique_id: kaffeetank_fuellstand_tassen
        unit_of_measurement: "Tassen"
        icon: mdi:coffee-outline
        state: >
          {% set counter_value = states('counter.kaffeemaschine_zubereitungen') | int(0) %}
          {% set max_counter = 5 %}
          {% set remaining = max_counter - counter_value %}
          {{ [remaining, 0] | max }}

      - name: Letzte Tassengröße
        unique_id: letzte_kaffeegroeße
        state: >-
          {% set dauer = states('input_number.kaffeemaschine_letzte_bruehdauer') | float(0) %}
          {% if dauer < 1 %}
            Standby
          {% elif dauer < 14 %}
            Zubereitung läuft
          {% elif dauer <= 35 %}
            Espresso klein
          {% elif dauer <= 44 %}
            Espresso groß
          {% elif dauer <= 60 %}
            Normale Tasse
          {% else %}
            Große Tasse
          {% endif %}
        icon: mdi:coffee
```

---

### 📊 Inhalt `history_stats.yaml`

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

---

### 💪 Warum ist das so wichtig?

Diese Sensoren und Templates …

- ❌ dürfen **nicht** verändert oder gekürzt werden
- ✅ sind exakt auf die Automationen abgestimmt
- ⚖️ sind die Grundlage für Statistiken und das Dashboard

Nur wenn diese exakt so übernommen werden, funktioniert dein gesamtes System wie geplant.

---


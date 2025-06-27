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
- sensor:
    - name: "Kaffeetank Füllstand Prozent"
      unique_id: sensor.kaffeetank_prozent
      unit_of_measurement: "%"
      state: >
        {% set voll = states('input_number.kaffeetank_groesse') | int(0) %}
        {% set ist = states('input_number.kaffeetank_aktuell') | int(0) %}
        {{ ((ist / voll) * 100) | round(0) if voll > 0 else 0 }}

    - name: "Kaffeetank Füllstand Tassen"
      unique_id: sensor.kaffeetank_tassen
      unit_of_measurement: "Tassen"
      state: >
        {% set ml_pro_tasse = 180 %}
        {% set ist = states('input_number.kaffeetank_aktuell') | int(0) %}
        {{ (ist / ml_pro_tasse) | round(0) }}

    - name: "Letzte Tassengröße"
      unique_id: sensor.letzte_tassengroesse
      state: "{{ states('input_text.kaffeemaschine_letzte_tassengroesse') }}"

- binary_sensor:
    - name: "Wasser fast leer"
      unique_id: binary_sensor.wasser_fast_leer
      state: >
        {% set prozent = states('sensor.kaffeetank_prozent') | int(0) %}
        {{ prozent < 20 }}
```

---

### 📊 Inhalt `history_stats.yaml`

```yaml
- platform: history_stats
  name: Kaffee heute
  unique_id: sensor.kaffee_heute
  entity_id: input_boolean.zubereitung_erkannt_statistik
  state: "on"
  type: count
  start: "{{ now().replace(hour=4, minute=0, second=0) }}"
  end: "{{ now() }}"

- platform: history_stats
  name: Kaffee diese Woche
  unique_id: sensor.kaffee_diese_woche
  entity_id: input_boolean.zubereitung_erkannt_statistik
  state: "on"
  type: count
  start: "{{ now().replace(hour=4, minute=0, second=0) - timedelta(days=now().weekday()) }}"
  end: "{{ now() }}"

- platform: history_stats
  name: Kaffee diesen Monat
  unique_id: sensor.kaffee_dieser_monat
  entity_id: input_boolean.zubereitung_erkannt_statistik
  state: "on"
  type: count
  start: "{{ now().replace(day=1, hour=4, minute=0, second=0) }}"
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


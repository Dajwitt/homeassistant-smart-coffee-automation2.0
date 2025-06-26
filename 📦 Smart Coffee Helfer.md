### 🧾 Anleitung zur Integration der Helfer:

1. Öffne deine Home Assistant `configuration.yaml`.
2. Füge den folgenden Block hinzu – entweder am Ende oder unter dem Abschnitt `input_boolean`, `input_number`, `input_text`, `counter`, `timer`, wenn du ihn schon verwendest:

```
# 📦 Smart Coffee Automatisierung: Helfer
input_boolean:
  kaffeemaschine_spuelvorgang_aktiv:
    name: Spülvorgang aktiv
  zubereitung_erkannt_statistik:
    name: Zubereitung erkannt Statistik

input_number:
  kaffeemaschine_bruehleistung_dauer:
    name: Brühdauer aktuelle Zubereitung
    min: 0
    max: 300
    step: 1
    unit_of_measurement: 's'
  kaffeemaschine_letzte_bruehdauer:
    name: Letzte Brühdauer
    min: 0
    max: 300
    step: 1
    unit_of_measurement: 's'

input_text:
  kaffeemaschine_letzte_tassengroesse:
    name: Letzte Tassengröße

counter:
  kaffeemaschine_zubereitungen:
    name: Kaffeezubereitungen insgesamt
  kaffeemaschine_tasse_normal:
    name: Normale Tassen
  kaffeemaschine_tasse_gross:
    name: Große Tassen

timer:
  kaffeemaschine_standby_vorwarnung:
    name: Vorwarnung Standby
    duration: "00:01:00"

  kaffeemaschine_idle_shutdown:
    name: Automatische Abschaltung
    duration: "00:05:00"

  kaffeemaschine_debug_timer:
    name: Debug Timer
    duration: "00:00:30"
```

> 💡 **Hinweis:** Die drei Timer (`standby_vorwarnung`, `idle_shutdown`, `debug_timer`) **müssen in der** `configuration.yaml` **gepflegt werden**, da Timer nach der Erstellung **nicht über die UI bearbeitet** werden können.

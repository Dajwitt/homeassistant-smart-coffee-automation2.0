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

  kaffeemaschine_5min_timer_abbrechen:
    name: 5-Minuten-Timer abbrechen
    icon: mdi:timer-off

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

> 💡 **Hinweis:** Die drei Timer (`standby_vorwarnung`, `idle_shutdown`, `debug_timer`) **müssen in der** `configuration.yaml` **gepflegt werden**, da Timer nach der Erstellung **nicht über die UI bearbeitet** werden können.

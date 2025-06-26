## 📲 Anleitung: Dashboard in Home Assistant importieren

### 🧾 Voraussetzung

- Alle **Sensoren**, **Helfer**, **Timer** und **Automation**-Blueprints müssen vorher wie in den Anleitungen beschrieben eingebunden worden sein.
- Dieses Dashboard dient der **Übersicht und Steuerung** der Kaffeemaschine und basiert exakt auf der empfohlenen Struktur.
- Die Datei findest du in diesem Projekt unter: `Dashboard.yaml`

---

### 📁 Schritt-für-Schritt-Anleitung

#### 1. **Öffne Home Assistant**

Gehe in der Seitenleiste zu **Einstellungen → Dashboards → Dashboard hinzufügen**.

#### 2. **Neues Dashboard erstellen**

- Name: z. B. `Kaffeemaschine`
- URL (Pfad): z. B. `tablet`
- Sichtbarkeit: Sichtbar lassen
- Speichern

#### 3. **Dashboard öffnen und in den YAML-Modus wechseln**

- Öffne das neu erstellte Dashboard
- Oben rechts auf die drei Punkte `⋮` klicken → **"Dashboard bearbeiten"**
- Wieder oben rechts auf `⋮` → **"In YAML bearbeiten"**

#### 4. **Inhalte einfügen**

- **Kopiere den gesamten Inhalt** 

```
views:
  - type: sections
    max_columns: 4
    title: Kaffeemaschine
    path: tablet
    sections:
      - type: grid
        cards:
          - type: heading
            icon: mdi:coffee-maker-outline
            heading: Maschine
            heading_style: title
          - type: tile
            entity: switch.kaffeemschine
            features_position: bottom
            vertical: false
            tap_action:
              action: toggle
            hide_state: false
            name: Kaffeemaschine
            grid_options:
              columns: 12
              rows: 1
          - type: tile
            entity: sensor.kaffeemaschine_power
            features_position: bottom
            vertical: false
            name: Kaffeemaschine
            grid_options:
              columns: 12
              rows: 1
          - type: tile
            entity: input_boolean.kaffeemaschine_spuelvorgang_aktiv
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
            icon: mdi:water
          - type: tile
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
            entity: input_boolean.zubereitung_erkannt_statistik
            name: Zubereitung erkannt
            hide_state: true
            color: accent
      - type: grid
        cards:
          - type: heading
            icon: mdi:coffee-maker-outline
            heading: Wasser
            heading_style: title
          - type: custom:button-card
            entity: sensor.kaffeetank_fullstand_prozent
            icon: mdi:water-percent
            layout: vertical
            show_state: true
            show_name: false
            state_display: '[[[ return entity.state + ''%'' ]]]'
            tap_action:
              action: none
            hold_action:
              action: more-info
            styles:
              card:
                - border-radius: 12px
                - padding: 10px
                - box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.15)
                - display: grid
                - grid-template-rows: auto 1fr auto
                - background: |
                    [[[
                      let v = parseInt(entity.state);
                      if (v >= 85) return "linear-gradient(to top, #2e7d32, #66bb6a)";
                      if (v >= 60) return "linear-gradient(to top, #fbc02d, #fff176)";
                      if (v >= 35) return "linear-gradient(to top, #f57c00, #ffb74d)";
                      if (v >= 17) return "linear-gradient(to top, #c62828, #ef5350)";
                      return "linear-gradient(to top, #880000, #b71c1c)";
                    ]]]
              icon:
                - height: 60px
                - width: 40px
                - color: white
                - justify-self: center
                - animation: |
                    [[[
                      return parseInt(entity.state) < 18 ? "blink-slow 1.5s infinite" : "none";
                    ]]]
              state:
                - font-size: 1.4em
                - font-weight: bold
                - color: white
                - justify-self: center
                - animation: |
                    [[[
                      return parseInt(entity.state) < 18 ? "blink-slow 1.5s infinite" : "none";
                    ]]]
            extra_styles: |
              @keyframes blink-slow {
                0%   { opacity: 1; }
                50%  { opacity: 0.4; }
                100% { opacity: 1; }
              }
          - type: tile
            entity: binary_sensor.wassertank_contact
            grid_options:
              columns: 12
              rows: 1
            features_position: bottom
            vertical: false
            name: Wassertank
      - type: grid
        cards:
          - type: heading
            icon: mdi:coffee-maker-outline
            heading: Statistik
            heading_style: title
          - type: tile
            entity: counter.kaffeemaschine_zubereitungen
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
          - type: tile
            entity: sensor.kaffee_heute
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
          - type: tile
            entity: sensor.kaffee_diese_woche
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
          - type: tile
            entity: counter.kaffeemaschine_tasse_normal
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
          - type: tile
            entity: counter.kaffeemaschine_tasse_gross
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
      - type: grid
        cards:
          - type: heading
            icon: mdi:tools
            heading: Timer
            heading_style: title
          - type: tile
            entity: timer.kaffeemaschine_idle_ausschalt_timer
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
          - type: tile
            entity: timer.kaffeemaschine_standby_vorwarnung
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
          - type: tile
            entity: timer.kaffeemaschine_wasser_nachfuell_prompt
            features_position: bottom
            vertical: false
            grid_options:
              columns: 12
              rows: 1
      - type: grid
        cards:
          - type: heading
            icon: ''
            heading: Helfer
            heading_style: title
          - features:
              - type: numeric-input
                style: buttons
            type: tile
            entity: input_number.kaffeemaschine_bruehleistung_dauer
            features_position: inline
            vertical: false
            hide_state: true
          - features:
              - type: numeric-input
                style: buttons
            type: tile
            entity: input_number.kaffeemaschine_letzte_bruehdauer
            features_position: inline
            vertical: false
            hide_state: true
      - type: grid
        cards:
          - type: heading
            icon: mdi:test-tube
            heading: Test
            heading_style: title
          - type: custom:mushroom-chips-card
            chips:
              - type: entity
                entity: input_boolean.dummy_helfer
                content_info: name
                tap_action:
                  action: perform-action
                  perform_action: script.zahler_tassengrose_zurucksetzen
                  target: {}
                name: 'Zähler Reset       '
                icon: mdi:restart
      - type: grid
        cards:
          - type: heading
            heading: Neuer Abschnitt
    cards: []
    badges: []
    header:
      card:
        type: markdown
        text_only: true
        content: '# Kaffeemaschine  ✨'
```

- Ersetze den vorhandenen YAML-Inhalt komplett damit
- **Speichern**

#### 5. **Fertig!**

Du kannst das Dashboard jetzt sofort nutzen. Alle relevanten Karten und Abschnitte wie:

- Maschinenstatus
- Stromverbrauch
- Spülvorgang
- Wassertankanzeige
- Statistik
- Timer-Steuerung
- Testfunktionen

…sind bereits **vollständig eingebunden**.

---

### ℹ️ Hinweise

- Das Dashboard nutzt **Mushroom Cards** und **Custom Button Cards** – diese müssen ggf. über **HACS** installiert werden:
  - `Mushroom Cards`
  - `Button Card`
- Du kannst das Layout jederzeit anpassen – die Logik der Automationen wird dadurch **nicht beeinträchtigt**.
# ☕ Home Assistant Smart Coffee Automation 2.0

Willkommen zur Version 2.0 des Smart-Coffee-Projekts für Home Assistant. Dieses Projekt bietet eine vollständig automatisierte Auswertung, Steuerung und Optimierung deiner Kaffeemaschine – mit Fokus auf einfache Übernahme durch fertige Blueprints, Helfer, Sensoren und einem Dashboard.

---

## 🚀 Funktionen im Überblick

✅ Automatische Erkennung von Kaffeezubereitungen
✅ Differenzierung zwischen 1 und 2 Tassen
✅ Zählung aller Vorgänge (inkl. täglicher & wöchentlicher Statistik)
✅ Spülvorgänge werden korrekt ignoriert
✅ Automatische Abschaltung der Maschine ohne Spülen
✅ Integration eines Wasserstand-Sensors mit Reset-Zähler
✅ Kompaktes Dashboard für Übersicht und Kontrolle

---

## 📥 Schnellstart: Blueprints importieren

Alle Automationen sind als **Blueprints** verfügbar. So einfach funktioniert der Import:

| Automation                   | Blueprint-Import                                                                                                                                                                                                   |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ☕ Kaffeezubereitung erkennen | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F742f2a1b079aafa4c80e378e42038555%2Fraw%2Fkaffeezubereitung_erkennen.yaml) |
| 🍵 Tassengröße erkennen      | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F9e9aa8203902c0265c80f30f64cc5911%2Fraw%2Ftassengroesse_bestimmen.yaml)    |
| 🌀 Spülvorgang erkennen      | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F7b47fb55c00832db02cb799baef7181f%2Fraw%2Fspuelvorgang_erkennen.yaml)      |
| 💧 Wassertank zurücksetzen   | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F70d522b2e358cca27c41e225abe3b458%2Fraw%2Fwassertank_ueberwachen.yaml)     |
| ⏱ Timer & Abschaltung        | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F5382905d489eb4275bd5b57c16ff1849%2Fraw%2Ftimer_und_abschaltung.yaml)      |

👉 Alternativ findest du die Blueprints direkt [hier als Übersicht](./📥%20Smart%20Coffee%20Blueprints.md)

---

## 🧱 Projektstruktur

Das Projekt ist in folgende Komponenten aufgeteilt, die du **eins zu eins übernehmen solltest**:

| Bereich         | Datei                                                                                                                                                                                        |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 📦 Helfer       | [📦 Smart Coffee Helfer.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%93%A6%20Smart%20Coffee%20Helfer.md)                                         |
| ⚙ Sensoren      | [⚙ Smart Coffee Sensoren & Templates.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%9A%99%20Smart%20Coffee%20Sensoren%20%26%20Templates.md)           |
| 💻 Dashboard    | [💻 Smart Coffee Dashboard.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%92%BB%20Smart%20Coffee%20Dashboard.md)                                   |
| ♻️ Automationen | [♻️ Smart Coffee Autmationen im Detail.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%99%BB%EF%B8%8F%20Smart%20Coffee%20Autmationen%20im%20Detail.md) |

---

## 📋 Installation & Konfiguration

Die einzelnen Komponenten müssen exakt übernommen werden, da sie logisch miteinander verknüpft sind. Du findest zu jeder Datei eine Anleitung, wie sie importiert oder eingebunden wird.

Besonders wichtig:

* Power-Sensor (z. B. `sensor.kaffeemaschine_power`)
* Wassertank-Sensor (binary\_sensor)
* Switch für die Maschine

Diese Geräte musst du **selbst einfügen**, alle anderen Helfer und Sensoren werden bereitgestellt.

---

## ℹ️ Hinweise

* Verwende den YAML-Modus, wenn du mit Raw-Dateien arbeitest.
* In der UI kannst du viele Helfer später nicht mehr anpassen (z. B. Timer-Zeiten), daher ist die Konfiguration über die YAML empfehlenswert.
* Vermeide das Umbenennen von Helfern oder Sensoren – die gesamte Logik basiert auf exakt benannten Entitäten.

---

## 💬 Feedback & Community

Wenn dir dieses Projekt gefällt oder du Erweiterungen hast, melde dich gerne auf [community.home-assistant.io](https://community.home-assistant.io/c/blueprints-exchange/53).

---

> Erstellt von [Dajwitt](https://github.com/Dajwitt) · Projektseite: [homeassistant-smart-coffee-automation2.0](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0)

# ☕ Home Assistant Smart Coffee Automation 2.0

Willkommen zur Version 2.0 des Smart-Coffee-Projekts für Home Assistant. Dieses Projekt bietet eine vollständig automatisierte Auswertung, Steuerung und Optimierung deiner Kaffeemaschine – mit Fokus auf einfache Übernahme durch fertige Blueprints, Helfer, Sensoren und einem Dashboard.

---

## 📚 Funktionsübersicht

 ✅ Automatische Erkennung von Kaffeezubereitungen  
 ✅ Differenzierung zwischen 1 und 2 Tassen  
 ✅ Zählung aller Vorgänge (inkl. täglicher & wöchentlicher Statistik)  
 ✅ Spülvorgänge werden korrekt ignoriert  
 ✅ Automatische Abschaltung der Maschine ohne Spülen  
 ✅ Integration eines Wasserstand-Sensors mit Reset-Zähler  
 ✅ Kompaktes Dashboard für Übersicht und Kontrolle

---

## 🔧 Voraussetzungen: Was du brauchst

Damit alle Automationen und Auswertungen korrekt funktionieren, benötigst du folgende Geräte in deinem Home Assistant Setup:

* ✅ **Power Sensor**: z. B. Shelly Plug S zur Leistungsmessung
* ✅ **Switch**: zum Ein-/Ausschalten der Kaffeemaschine (oft im Plug enthalten)
* ✅ **(Optional)** Binary-Sensor am Wassertank (z. B. über Reed-Kontakt)

Diese Geräte musst du **selbst einfügen** – alle anderen Konfigurationen werden vollständig bereitgestellt.

---

## 📦 Schritt 1: Helfer anlegen

Alle benötigten Helfer findest du hier:
📄 [📦 Smart Coffee Helfer.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%93%A6%20Smart%20Coffee%20Helfer.md)

> ⚠️ **Wichtig:** Diese Helfer müssen **exakt so** benannt und übernommen werden, damit die gesamte Logik funktioniert. Bitte **nichts abändern oder kürzen**.

---

## ⚙ Schritt 2: Sensoren & Templates einfügen

Hier werden die Template-Sensoren, Binary-Sensoren und Statistiken angelegt:
📄 [⚙ Smart Coffee Sensoren & Templates.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%9A%99%20Smart%20Coffee%20Sensoren%20%26%20Templates.md)

> ⚠️ Auch hier gilt: Alle Abschnitte bitte **vollständig** übernehmen – sie sind auf die oben genannten Helfer abgestimmt.

---

## 📥 Schritt 3: Automationen per Blueprint importieren

Jede Automation hat eine ganz bestimmte Aufgabe innerhalb der Logik:

* **☕ Kaffeezubereitung erkennen**: Erkennt zuverlässig den Start einer Zubereitung anhand der Leistungsaufnahme.
* **🍵 Tassengröße erkennen**: Unterscheidet zwischen 1-Tassen- und 2-Tassen-Zubereitungen basierend auf der Laufzeit.
* **🌀 Spülvorgang erkennen**: Filtert automatische Spülungen nach dem Einschalten zuverlässig aus.
* **💧 Wassertank zurücksetzen**: Setzt einen Zähler zurück, wenn der Tank aufgefüllt wurde – Voraussetzung ist ein Sensor.
* **⏱ Timer & Abschaltung**: Erkennt, wenn die Maschine im Leerlauf ist, und schaltet sie dann automatisch aus.

Alle Automationen sind als **Blueprints** verfügbar.
👉 **Klicke auf „Importieren“, um den jeweiligen Blueprint direkt in Home Assistant zu laden.**

| Automation                   | Blueprint-Import                                                                                                                                                                                                   |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ☕ Kaffeezubereitung erkennen | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F742f2a1b079aafa4c80e378e42038555%2Fraw%2Fkaffeezubereitung_erkennen.yaml) |
| 🍵 Tassengröße erkennen      | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F9e9aa8203902c0265c80f30f64cc5911%2Fraw%2Ftassengroesse_bestimmen.yaml)    |
| 🌀 Spülvorgang erkennen      | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F7b47fb55c00832db02cb799baef7181f%2Fraw%2Fspuelvorgang_erkennen.yaml)      |
| 💧 Wassertank zurücksetzen   | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F70d522b2e358cca27c41e225abe3b458%2Fraw%2Fwassertank_ueberwachen.yaml)     |
| ⏱ Timer & Abschaltung        | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.githubusercontent.com%2FDajwitt%2F5382905d489eb4275bd5b57c16ff1849%2Fraw%2Ftimer_und_abschaltung.yaml)      |

📑 Details zu allen Automationen findest du hier:
📄 [♻️ Smart Coffee Autmationen im Detail.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%99%BB%EF%B8%8F%20Smart%20Coffee%20Autmationen%20im%20Detail.md)

---

## 💻 Schritt 4: Dashboard importieren

Das kompakte Dashboard gibt dir volle Kontrolle über deine Kaffeemaschine.

📄 [💻 Smart Coffee Dashboard.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%92%BB%20Smart%20Coffee%20Dashboard.md)

> 📌 Hinweis: YAML-Modus muss aktiv sein, um das Dashboard direkt per Datei einzufügen. Alternativ können die Karten manuell hinzugefügt werden.

📷 Beispiel:
![Smart Coffee Dashboard](https://raw.githubusercontent.com/Dajwitt/homeassistant-smart-coffee-automation2.0/main/media/dashboard-overview.png)

---

## 🧪 Ergebnis: Was du bekommst

* Übersicht aller Zubereitungen mit Tages- & Wochenstatistik
* Differenzierung von 1x oder 2x Tassenbezügen
* Automatische Abschaltung mit Wasserkontrolle
* Saubere Integration in Home Assistant UI

---

## ℹ️ Hinweise & Community

* YAML-Modus wird empfohlen für volle Kontrolle
* Entitäten dürfen nicht umbenannt werden
* Änderungen an Templates oder Sensoren stören die Automationslogik

💬 Du hast Feedback oder Fragen?
👉 Besuche den [Blueprints-Bereich der Community](https://community.home-assistant.io/c/blueprints-exchange/53)

---

> Erstellt von [Dajwitt](https://github.com/Dajwitt) · Projektseite: [homeassistant-smart-coffee-automation2.0](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0)

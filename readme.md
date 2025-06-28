# ☕ Home Assistant Smart Coffee Automation 2.0

Willkommen zur Version 2.0 des Smart-Coffee-Projekts für Home Assistant. Dieses Projekt bietet eine vollständig automatisierte Auswertung, Steuerung und Optimierung deiner Kaffeemaschine – mit Fokus auf einfache Übernahme durch fertige Blueprints, Helfer, Sensoren und einem Dashboard.

---

## 📚 Funktionsübersicht

 ✅ Automatische Erkennung von Kaffeezubereitungen  
 
 ✅ Differenzierung zwischen 1 und 2 Tassen  
 
 ✅ Zählung aller Vorgänge (inkl. täglicher & wöchentlicher Statistik)  
 
 ✅ Spülvorgänge ignorieren (Optional)
 
 ✅ Automatische Abschaltung der Maschine mit oder ohne spülen vor dem Standby  
 
 ✅ Integration eines (Wasserstand-Sensors) mit Reset-Zähler  
 
 ✅ Kompaktes Dashboard für Übersicht und Kontrolle

---

## 🔧 **Voraussetzungen: Was du brauchst**

Damit alle Automationen und Auswertungen korrekt funktionieren, benötigst du folgende Komponenten in deinem Home Assistant Setup:

✅ **Smart-Relaisschalter** (z. B. Shelly 1PM Gen 2/3/4) zur Leistungsmessung

✅ **Kontaktsensor** (z. B. Aqara Tür-/Fensterkontakt) am Wassertank

✅ **Erfasste Daten:**
– Zeit bis zum Standby
– Dauer der Zubereitung
– Leistungsaufnahme (Watt) beim Einschalten und während der Zubereitung

## **Optional**

✅ **Sprachassistent** (z. B. Amazon Echo) für akustische Hinweise

✅ **Home Assistant Companion App** für mobile Benachrichtigungen

**Hinweis:** Den Smart-Relaisschalter und den Kontaktsensor musst du selbst in Home Assistant einbinden. Alle übrigen Konfigurationen werden vollständig durch dieses Projekt bereitgestellt.

---

## 📦 **Schritt 1: Welche Daten brauchst du?**

Bevor du startest, solltest du folgende Informationen über deine Kaffeemaschine kennen:

⏱️ **Standby-Zeit:** Wie lange bleibt die Maschine nach dem Einschalten aktiv, bevor sie automatisch abschaltet?

☕ **Zubereitungsdauer:** (Voreingestellt)
– Eine Tasse: unter 60 Sekunden 
– Zwei Tassen: ab 60 Sekunden

⚡ **Leistungsaufnahme (Watt):**
– Beim Einschalten (voreingestellt: 500 W)
– Während der Zubereitung (voreingestellt: 1000 W)

---

## 📦 Schritt 2: Helfer anlegen

Alle benötigten Helfer findest du hier:
📄 [📦 Smart Coffee Helfer.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%93%A6%20Smart%20Coffee%20Helfer.md)

> ⚠️ **Wichtig:** Diese Helfer müssen **exakt so** benannt und übernommen werden, damit die gesamte Logik funktioniert. Bitte **nichts abändern!!!**.

---

## ⚙ Schritt 3: Sensoren & Templates einfügen

Hier werden die Template-Sensoren, Binary-Sensoren und Statistiken angelegt:
📄 [⚙ Smart Coffee Sensoren & Templates.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%9A%99%20Smart%20Coffee%20Sensoren%20%26%20Templates.md)

> ⚠️ Auch hier gilt: Alle Abschnitte bitte **vollständig** übernehmen – sie sind auf die oben genannten Helfer abgestimmt.

---

## 📥 Schritt 4: Automationen per Blueprint importieren

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

## 💻 Schritt 5: Dashboard importieren

Das kompakte Dashboard gibt dir volle Kontrolle über deine Kaffeemaschine.

📄 [💻 Smart Coffee Dashboard.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%92%BB%20Smart%20Coffee%20Dashboard.md)

> 📌 Hinweis: YAML-Modus muss aktiv sein, um das Dashboard direkt per Datei einzufügen. Alternativ können die Karten manuell hinzugefügt werden.

📷 Beispiel:

<img src="https://github.com/user-attachments/assets/7fc665fa-e27d-436f-8962-43ecba983ed7" width="600"/>

---

## 🧪 Ergebnis: Was du bekommst

* Übersicht aller Zubereitungen mit Tages- & Wochenstatistik (Normale & Große Tassen)
* Differenzierung von 1x oder 2x Tassenbezügen
* Automatische Abschaltung mit Wasserkontrolle
* Saubere Integration in Home Assistant UI

---

## 💬 Hinweise & FAQ

* [Warum ich dieses Projekt erstellt habe?](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%9D%94%20Warum%20diese%20Projekt.md)
* [Smart Coffee FAQ](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%92%AC%20Smart%20Coffee%20FAQ.md)


---

> Erstellt von [Dajwitt](https://github.com/Dajwitt) · Projektseite: [homeassistant-smart-coffee-automation2.0](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0)

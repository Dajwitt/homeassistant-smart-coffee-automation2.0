# ☕ Home Assistant Smart Coffee Automation 

Willkommen zu einem etwas anderen Smart-Home-Projekt – hier geht es nicht um Lichtschalter oder Bewegungsmelder, sondern um das wichtigste Gerät in der Küche: **Den Kaffeevollautomaten**

Diese Anleitung zeigt dir, wie du mit einem Stromsensor, einem Türkontakt, ein paar Home Assistant-Helfern und cleverer Logik erkennen kannst, ob dein **nicht smarter Kaffeevollautomat gerade spült, Kaffee zubereitet – oder einfach nur still in der Ecke steht. Ganz ohne Integration oder API. Nur durch Verhaltenserkennung.

### ✅ Vorteile

- Funktioniert mit nahezu jedem Vollautomaten, da das Verhalten analysiert wird, nicht die Technik
- Sehr zuverlässig, wenn Stromaufnahme und Zubereitungsdauer konstant sind
- Extrem vielseitig für Folge-Automationen (z. B. Wassertankwarnung, Abschaltung, Erinnerungen)
- Kein Root, keine Cloud, keine Bastellösung auf der Maschine selbst nötig

 ## 💡 Hinweis zur Übertragbarkeit

Dieses Projekt basiert auf einem **DeLonghi Magnifica S Kaffeevollautomaten**. Doch das Prinzip lässt sich auf nahezu **jeden Vollautomaten übertragen**

---

## 📚 Funktionsübersicht

 ✅ Automatische Erkennung von Kaffeezubereitungen  

 ✅ Wassertanküberwachung  
 
 ✅ Differenzierung zwischen normale und große Tassen  
 
 ✅ Zählung aller Vorgänge (inkl. täglicher & wöchentlicher Statistik)  
 
 ✅ Automatische Abschaltung der Maschine mit oder ohne spülen vor dem Standby  

 ✅ Benachrichtigung - wenn der Tank leer ist oder die Maschine bald abschaltet  
 
 ✅ Kompaktes Dashboard für Übersicht und Kontrolle

---

## 🔧 **Voraussetzungen: Was du brauchst**

Damit alle Automationen und Auswertungen korrekt funktionieren, benötigst du folgende Komponenten in deinem Home Assistant Setup:

✅ **Smart-Relaisschalter** (z. B. Shelly 1PM Gen 2/3/4) zur Leistungsmessung

✅ **Kontaktsensor** (z. B. Aqara Tür-/Fensterkontakt) am Wassertank

## **Optional**

✅ **Sprachassistent** (z. B. Amazon Echo) für akustische Hinweise

✅ **Home Assistant Companion App** für mobile Benachrichtigungen

**Hinweis:** Den Smart-Relaisschalter und den Kontaktsensor musst du selbst in Home Assistant einbinden. Alle übrigen Konfigurationen werden vollständig durch dieses Projekt bereitgestellt.

---

## 📦 **Schritt 1: Welche Daten brauchst du?**

Bevor du startest, solltest du folgende Informationen über deine Kaffeemaschine kennen:

⏱️ **Standby-Zeit:** Wie lange bleibt die Maschine nach dem Einschalten aktiv, bevor sie automatisch abschaltet?

☕ **Zubereitungsdauer:** (Voreingestellt und wird im laufenden Betrieb angepasst!)
– Eine Tasse: unter 60 Sekunden 
– Zwei Tassen: ab 60 Sekunden

⚡ **Leistungsaufnahme (Watt):** (Voreingestellt und wird im laufenden Betrieb angepasst!)
– Beim Einschalten (500 W)
– Während der Zubereitung (1000 W)

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
* **🍵 Tassengröße erkennen**: Unterscheidet zwischen Normale-Tassen- und Große-Tassen-Zubereitungen basierend auf der Laufzeit.
* **🌀 Spülvorgang erkennen**: Filtert automatische Spülungen nach dem Einschalten zuverlässig aus.
* **💧 Wassertank zurücksetzen**: Setzt einen Zähler zurück, wenn der Tank aufgefüllt wurde – Voraussetzung ist ein Sensor.
* **⏱ Timer & Abschaltung**: Erkennt, wenn die Maschine im Leerlauf ist, und schaltet sie dann automatisch aus.

Alle Automationen sind als **Blueprints** verfügbar.
👉 **Klicke auf „Importieren“, um den jeweiligen Blueprint direkt in Home Assistant zu laden.**

| Automation                   | Blueprint-Import                                                                                                                                                                                                   |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ☕ Kaffeezubereitung erkennen | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.github.com%2FDajwitt%2F742f2a1b079aafa4c80e378e42038555) |
| 🍵 Tassengröße erkennen      | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.github.com%2FDajwitt%2F9e9aa8203902c0265c80f30f64cc5911)    |
| 🌀 Spülvorgang erkennen      | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.github.com%2FDajwitt%2F7b47fb55c00832db02cb799baef7181f%2Fedit)      |
| 💧 Wassertank zurücksetzen   | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.github.com%2FDajwitt%2F70d522b2e358cca27c41e225abe3b458)     |
| ⏱ Timer & Abschaltung        | [Importieren](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgist.github.com%2FDajwitt%2F5382905d489eb4275bd5b57c16ff1849)      |

📑 Details zu allen Automationen findest du hier:
📄 [♻️ Smart Coffee Autmationen im Detail.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%99%BB%EF%B8%8F%20Smart%20Coffee%20Autmationen%20im%20Detail.md)

---

## 💻 Schritt 5: Dashboard importieren

Das kompakte Dashboard gibt dir volle Kontrolle über deine Kaffeemaschine. „So sieht dein Dashboard nach einigen Zubereitungen aus“

📑 Details zu Dashboard findest du hier: [💻 Smart Coffee Dashboard.md](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%92%BB%20Smart%20Coffee%20Dashboard.md)


<p align="center">
  <img src="https://github.com/Dajwitt/picture/blob/main/smart_coffee_dashboard_1_1.png?raw=true" width="600"/>
</p>

---

## ✏ Schritt 6: Anpassung im laufenden Betrieb

Hier erfolgt die Nacharbeit und erfordert das Beobachten der Abläufe und kleine Anpassungen. 📑 Details zu Dashboard findest du hier:  [📈 Smart Coffee Anpassung & Feinjustierung](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%93%88%20Smart%20Coffee%20Anpassung%20%26%20Feinjustierung.md)

---

## 🧪 Ergebnis: Was du bekommst

* Übersicht aller Zubereitungen mit Tages- & Wochenstatistik (Normale & Große Tassen)
* Differenzierung von 1x oder 2x Tassenbezügen
* Automatische Abschaltung mit Wasserkontrolle
* Saubere Integration in Home Assistant UI

---

## 💬 Hinweise & FAQ

* [Warum ich dieses Projekt erstellt habe?](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%9D%94%20Warum%20dieses%20Projekt.md)
* [Smart Coffee FAQ](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%F0%9F%92%AC%20Smart%20Coffee%20FAQ.md)


---

> Erstellt von [Dajwitt](https://github.com/Dajwitt) · Projektseite: [homeassistant-smart-coffee-automation2.0](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0)

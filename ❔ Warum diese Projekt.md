## Ein smarter Kaffeevollautomat mit Home Assistant ☕️🤖

Willkommen zu einem etwas anderen Smart-Home-Projekt – hier geht es nicht um Lichtschalter oder Bewegungsmelder, sondern um das wichtigste Gerät in der Küche: den Kaffeevollautomaten.

Diese Anleitung zeigt dir, wie du mit einem Stromsensor, einem Türkontakt, ein paar Home Assistant-Helfern und cleverer Logik erkennen kannst, ob deine Kaffeemaschine gerade spült, Kaffee zubereitet – oder einfach nur still in der Ecke steht. Ganz ohne Integration oder API. Nur durch Verhaltenserkennung.

## Ziel des Projekts ist:

- 🌀 Spülvorgänge zu erkennen (z. B. beim Einschalten)
- ☕ Kaffeezubereitung zu identifizieren (und zu zählen)
- 💧 Den Wassertank zu überwachen (indirekt, über die Anzahl der Zubereitungen)
- ⏲️ Die Maschine gezielt auszuschalten, bevor sie automatisch spült
- 🗣️ Die Daten für weitere Automationen (Benachrichtigungen, Statistiken, Sprachassistenten) verfügbar zu machen

### ✅ Vorteile

- Funktioniert mit nahezu jedem Vollautomaten, da das Verhalten analysiert wird, nicht die Technik
- Sehr zuverlässig, wenn Stromaufnahme und Zubereitungsdauer konstant sind
- Extrem vielseitig für Folge-Automationen (z. B. Wassertankwarnung, Abschaltung, Erinnerungen)
- Kein Root, keine Cloud, keine Bastellösung auf der Maschine selbst nötig

### 🚫 Kein vollautomatischer Barista

So smart die Erkennung auch ist – **die Maschine bleibt manuell**: Du musst weiterhin selbst den Knopf drücken, um einen Kaffee zu starten. Die Automationen begleiten dich dabei intelligent, erkennen Abläufe, überwachen den Zustand und helfen beim Energiesparen. Sie ersetzen aber (noch) nicht den menschlichen Griff zur Taste.  

> 💡 Dafür bekommst du volle Transparenz – und vielleicht ein kleines Stück smarteren Alltag.

---

## 🔧 So baust du dein eigenes Smart-Kaffee-System

Wenn du direkt loslegen willst, folge einfach dieser Schritt-für-Schritt-Anleitung:

1. 🔍 [Benötigte Datenquellen und Messwerte](./Benötigte%20Datenquellen%20und%20Messwerte.md)
2. 🧰 [Geräte & Sensor-Voraussetzungen](./Geräte.md)
3. 🛠️ [Helfer (Helpers)](./Helfer.md)
4. 🧪 [Template Sensoren](./Template%20Sensoren.md)
5. ⚙️ Automationen:

   * [Kaffeezubereitung erkennen](./Kaffeezubereitung%20erkennen.md)
   * [Spülvorgang erkennen](./Delongi%20Spülen%20erkennen.md)
   * [Timer & Abschaltung](./Timer%20%26%20Abschaltung.md)
   * [Wassertank – Zähler zurücksetzen](./Wassertank%20–%20Zähler%20zurücksetzen.md)

---

## 💡 Warum ich diese Automationen gebaut habe

### 1. **Spülen verhindern vorm Ausschalten**

Viele Maschinen spülen automatisch, bevor sie in den Standby gehen – oft völlig unnötig. Diese Automation erkennt das und **verhindert das Spülen**, wenn es nicht gebraucht wird. Das spart Wasser und Nerven. Außerdem ist nichts nerviger, wenn du nicht genau weißt, wann die Maschine sich von selbst ausschaltet.

### 2. **Spülvorgänge und Kaffeezubereitung unterscheiden**

Über den Stromverbrauch wird exakt erkannt, ob die Maschine **spült** oder **Kaffee brüht**. So weiß Home Assistant jederzeit, was gerade passiert – und kann entsprechend reagieren.

### 3. **Kaffeezähler + Wassertanküberwachung**

Ein leerer Wassertank mitten im Brühvorgang ist nicht nur ärgerlich, sondern kann auch dazu führen, dass keine  komplette Tasse Kaffee rauskommt.

Da mein Automat den Wasserstand nicht misst, zählt Home Assistant einfach mit:  
 **5 Kaffee = leerer Tank**  
 So kann eine Erinnerung kommen – bevor’s kritisch wird.

### 4. **Maschinenstatus überwachen**

Die Automationen erfassen auch, **wie lange die Maschine bereits an ist**, wann sie sich **abschaltet**. Wird in der Zeit ein neuer Kaffee zubereitet, startet alle Timer neu. So kannst du z. B. anzeigen lassen:  
 *„Läuft seit 37 Minuten“*, *„geht in Kürze in den Standby“*, *„wurde nach letzter Zubereitung automatisch abgeschaltet“*.

---

## 💡 Hinweis zur Übertragbarkeit

Dieses Projekt basiert auf einem **DeLonghi Magnifica S Kaffeevollautomaten**. Doch das Prinzip lässt sich auf nahezu **jeden Vollautomaten übertragen** – wichtig ist nur, dass du das typische Verhalten deines Geräts **kennst und dokumentierst**.  
Dann kannst du die **Sensoren, Schwellenwerte und Zeitintervalle** einfach anpassen.

---

## 👨‍🔧 Warum du es nachbauen solltest

- Du liebst clevere Automationen, die **ohne Hardware-Hack funktionieren**?
- Du möchtest wissen, wie viele Kaffee du wirklich trinkst?
- Du willst vermeiden, dass du morgens **wegen leerem Tank schlechte Laune hast**?
- Du willst deinem Home Assistant ein echtes Highlight verpassen?

Dann wirst du dieses Projekt lieben.

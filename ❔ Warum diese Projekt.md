## Ein smarter Kaffeevollautomat mit Home Assistant ☕️🤖

## Ziel des Projekts ist:

- 🌀 Spülvorgänge zu erkennen (z. B. beim Einschalten)
- ☕ Kaffeezubereitung zu identifizieren (und zu zählen)
- 💧 Den Wassertank zu überwachen (indirekt, über die Anzahl der Zubereitungen)
- ⏲️ Die Maschine gezielt auszuschalten, bevor sie automatisch spült
- 🗣️ Die Daten für weitere Automationen (Benachrichtigungen, Statistiken, Sprachassistenten) verfügbar zu machen

### 🚫 Kein vollautomatischer Barista

So smart die Erkennung auch ist – **die Maschine bleibt manuell**: Du musst weiterhin selbst den Knopf drücken, um einen Kaffee zu starten. Die Automationen begleiten dich dabei intelligent, erkennen Abläufe, überwachen den Zustand und helfen beim Energiesparen. Sie ersetzen aber (noch) nicht den menschlichen Griff zur Taste.  

> 💡 Dafür bekommst du volle Transparenz – und vielleicht ein kleines Stück smarteren Alltag.

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

## 👨‍🔧 Warum du es nachbauen solltest

- Du liebst clevere Automationen, die **ohne Hardware-Hack funktionieren**?
- Du möchtest wissen, wie viele Kaffee du wirklich trinkst?
- Du willst vermeiden, dass du morgens **wegen leerem Tank schlechte Laune hast**?
- Du willst deinem Home Assistant ein echtes Highlight verpassen?

Dann wirst du dieses Projekt lieben.

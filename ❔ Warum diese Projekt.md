# ☕️🤖 Ein smarter Kaffeevollautomat mit Home Assistant: Die Version 2.0

Dieses Dokument erklärt die Entstehungsgeschichte und die Kernziele des **Smart Coffee Automation**-Projekts. Es beleuchtet, warum diese Automationen entwickelt wurden und welche Vorteile sie dir im täglichen Gebrauch deiner Kaffeemaschine bieten.

---

## 🎯 Die Ziele dieses Projekts

Die **Smart Coffee Automation 2.0** wurde mit klaren Zielen entwickelt, um dein Kaffeeerlebnis zu optimieren und mehr Transparenz in den Betrieb deines Vollautomaten zu bringen:

* **Null-Smart-Maschine smart machen:** Das Kernziel dieses Projekts ist es, einen standardmäßigen, **nicht-smarten Kaffeevollautomaten** – wie beispielsweise einen **DeLonghi Magnifica S** – mittels externer Sensoren (Stromsensor und Türkontakt) vollwertig in Home Assistant zu integrieren. Dies ermöglicht es, alle Funktionen der Maschine zu erweitern und ihren Status sichtbar zu machen, was weit über einfache Komfortfunktionen hinausgeht.

* **🌀 Spülvorgänge erkennen:** Automatische Spülvorgänge (z.B. beim Einschalten) sollen zuverlässig identifiziert werden, um unnötigen Wasserverbrauch zu vermeiden.

* **☕ Kaffeezubereitung identifizieren & zählen:** Erkenne präzise, wann Kaffee gebrüht wird, und führe eine genaue Zählung durch.

* **💧 Wassertank überwachen:** Obwohl viele Maschinen keinen direkten Sensor haben, wird der Wasserstand indirekt über die Anzahl der Zubereitungen überwacht.

* **⏲️ Gezielte Abschaltung:** Die Maschine soll gezielt ausgeschaltet werden können, bevor sie automatisch spült und in den Standby-Modus geht.

* **🗣️ Daten für weitere Automationen:** Alle gesammelten Daten und Statusinformationen werden für weiterführende Automationen wie Benachrichtigungen, Statistiken und die Integration in Sprachassistenten nutzbar gemacht.

### 🚫 Wichtiger Hinweis: Kein vollautomatischer Barista

So intelligent die Erkennung und Steuerung auch sind, dieses System macht deine Kaffeemaschine **nicht zu einem vollautomatischen Barista**. Du drückst weiterhin selbst den Knopf, um deinen Kaffee zuzubereiten. Die Automationen begleiten dich dabei im Hintergrund: Sie erkennen Abläufe, überwachen den Zustand und helfen dir, Energie zu sparen. Sie ersetzen jedoch (noch) nicht den menschlichen Griff zur Taste.

> 💡 Dafür erhältst du volle Transparenz über die Nutzung deiner Maschine und integrierst ein weiteres Stück Smartness in deinen Alltag.

---

## 💡 Warum ich diese Automationen gebaut habe – Die Motivation hinter Version 2.0

Die Idee zu diesem Projekt entstand aus dem Wunsch heraus, die Nutzung von Kaffeevollautomaten smarter und effizienter zu gestalten, insbesondere da viele Modelle keine integrierten Smart-Home-Funktionen bieten. Die Version 2.0 ist das Ergebnis kontinuierlicher Verfeinerung und Optimierung.

### 1. **Unnötiges Spülen vor dem Ausschalten verhindern**

Viele Kaffeemaschinen führen vor dem Übergang in den Standby-Modus einen automatischen Spülvorgang durch, der oft unnötig ist und Wasser verschwendet. Diese Automation wurde entwickelt, um dies zu erkennen und das Spülen gezielt zu verhindern, wenn es nicht erforderlich ist. Das spart nicht nur Wasser, sondern auch Nerven, da man nicht ständig darauf achten muss, wann sich die Maschine von selbst abschaltet.

### 2. **Spülvorgänge und Kaffeezubereitung präzise unterscheiden**

Durch die Analyse des Stromverbrauchs kann das System exakt erkennen, ob die Maschine gerade **spült** oder tatsächlich **Kaffee brüht**. Dies ermöglicht Home Assistant, jederzeit den genauen Status der Maschine zu kennen und entsprechend intelligent darauf zu reagieren.

### 3. **Intelligenter Kaffeezähler & Wassertanküberwachung**

Ein leerer Wassertank mitten im Brühvorgang ist frustrierend und kann dazu führen, dass keine vollständige Tasse Kaffee zubereitet wird. Da mein Automat den Wasserstand nicht direkt misst, zählt Home Assistant einfach die zubereiteten Kaffees mit (z.B. "5 Kaffee = leerer Tank"). So kann rechtzeitig eine Erinnerung gesendet werden, bevor der Tank kritisch leer ist.

### 4. **Umfassende Maschinenstatusüberwachung**

Die Automationen erfassen detailliert, **wie lange die Kaffeemaschine bereits eingeschaltet ist** und wann sie sich **automatisch abschaltet**. Wird in dieser Zeit ein neuer Kaffee zubereitet, starten alle Timer neu. Dies ermöglicht eine dynamische Statusanzeige, beispielsweise: *"Läuft seit 37 Minuten"*, *"geht in Kürze in den Standby"* oder *"wurde nach letzter Zubereitung automatisch abgeschaltet"*.

---

## 👨‍🔧 Warum du dieses Projekt nachbauen solltest

Wenn du:

* clevere Automationen liebst, die **ohne physische Hardware-Modifikationen an der Maschine funktionieren**,
* genau wissen möchtest, wie viele Kaffees du tatsächlich trinkst,
* morgens nicht wegen eines leeren Wassertanks schlechte Laune bekommen möchtest,
* deinem Home Assistant ein echtes Highlight hinzufügen willst,

... dann ist dieses Projekt genau das Richtige für dich!

# 💻 Anpassung im laufenden Betrieb – Zubereitungszeiten kalibrieren

Nachdem du alle Komponenten des Smart Coffee Projekts eingerichtet hast, ist dieser Schritt entscheidend, um die Präzision deiner Kaffeeerkennung zu perfektionieren. Hier geht es darum, die spezifischen Zubereitungsdauern deiner Kaffeemaschine zu ermitteln und die Automationen entsprechend anzupassen.

### ✅ Warum ist das wichtig?

Jede Kaffeemaschine hat leicht unterschiedliche Zubereitungszeiten für normale und große Tassen. Das Projekt verwendet voreingestellte Werte, aber für eine **zuverlässige Erkennung und Zählung** ist es essenziell, diese auf die tatsächlichen Zeiten deiner Maschine abzustimmen. Die Anpassung erfolgt **einfach und zentral über die Variablen in der Home Assistant Benutzeroberfläche**.

### 📝 Ablauf der Kalibrierung

1. **Dashboard beobachten:**
   
   * Öffne dein **Smart Coffee Dashboard** in Home Assistant.
   * Konzentriere dich auf den Helfer `input_number.kaffeemaschine_bruehleistung_dauer` (oder "Zubereitungsdauer aktuelle Zubereitung"). Dieser Wert zählt während eines Zubereitungsvorgangs von 0 aufwärts.
  
   * **Kaffee zubereiten:** Bereite zunächst **eine normale Tasse Kaffee** zu.
   * **Dauer notieren:** Beobachte den Wert von `input_number.kaffeemaschine_bruehleistung_dauer`. Sobald die Zubereitung beendet ist (der Stromverbrauch sinkt und die Zählung stoppt), **notiere dir den finalen Wert**. Dies ist die tatsächliche Zubereitungsdauer für eine normale Tasse.
   * Wiederhole den Vorgang für **eine große Tasse Kaffee** und notiere auch hier die entsprechende Zubereitungsdauer. Führe den Test am besten jeweils 2-3 Mal durch und nimm den Durchschnittswert, um die Ergebnisse zu glätten.

   > 💡 **Beispiel:**
   > * Normale Tasse: Deine Maschine zubereitet im Schnitt 25 Sekunden.
   > * Große Tasse: Deine Maschine zubereitet im Schnitt 68 Sekunden.

---

2. **Automation "☕️ Zubereitung erkennen" anpassen:**
   
   * Gehe in Home Assistant zu **Einstellungen → Automationen & Szenen**.
   * Suche die Automation mit dem Namen `☕️ Zubereitung erkennen` (oder dem Alias, den du vergeben hast) und **klicke sie an, um sie zu bearbeiten**.
   * **Scrolle im Editor ganz nach unten**. Dort findest du den Abschnitt **"Variablen"**. Hier sind die Werte für die minimale und maximale Zubereitungsdauer für normale und große Tassen direkt als Eingabefelder verfügbar.
  
<p align="center">
  <img src="https://github.com/Dajwitt/dajwitt_workplace2/blob/main/kaffeezubereitung_erkennen.png?raw=true" width="600"/>
</p>


   * Passe die Zahlenwerte in diesen Feldern an die von dir gemessenen Zubereitungsdauern an. Es ist ratsam, einen kleinen Puffer um deine ermittelten Werte zu lassen (z.B. +/- 15 Sekunden), um natürliche Schwankungen zu berücksichtigen. Es kann auch zu enormen Schwankungen kommen, hatte ich bisher nur einmal. Sollte das öfter vorkommen, kannst du bei **Sobald Kaffeemschine Power über 1000 ist**, 1300 Watt einstellen und beobachten, ob diese Werte stabiler sind.
   * **Speichere die Automation.**
---

3. **Automation "🍵 Tassengröße nach Zubereitung erkennen" anpassen:**
   * Gehe erneut zu **Einstellungen → Automationen & Szenen**.
   * Suche die Automation mit dem Namen `🍵 Tassengröße nach Zubereitung erkennen` und **klicke sie an, um sie zu bearbeiten**.
   * **Scrolle im Editor etwas nach unten** zum Abschnitt **"Variablen"**. Dort findest du den Schwellenwert, der zur Erkennung der Tassengröße verwendet wird.

<p align="center">
  <img src="https://github.com/Dajwitt/picture/blob/main/kaffeezubereitung_erkennen.png?raw=true" width="600"/>
</p>

   * Passe den Zahlenwert in diesem Feld entsprechend deinen ermittelten Zeiten an. Dieser Wert definiert, ab welcher Zubereitungsdauer eine Tasse als "groß" gezählt wird. Auch hier solltest du einen kleinen Puffer einplanen.
   * **Speichere die Automation.**

---

### 📈 Feinjustierung

Beobachte das System nach den Anpassungen über einige Tage. Sollten weiterhin Zählfehler auftreten (z.B. eine große Tasse wird als normale Tasse gezählt), passe die Werte in den **Variablen-Abschnitten** der Automationen schrittweise an, bis die Erkennung optimal ist.

---

**Mache weiter mit ❓ [Warum dieses Projekt](https://github.com/Dajwitt/homeassistant-smart-coffee-automation2.0/blob/main/%E2%9D%94%20Warum%20dieses%20Projekt.md)**

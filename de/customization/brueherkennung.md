---
title: Brüherkennung
parent: Konfiguration & Anpassung
grand_parent: DE - Handbuch
has_children: false
nav_order: 2
---

# Brüherkennung
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

Wie in dem vorherigen Kapitel erwähnt, soll der **brew heater detection limit** Wert auf „0“ gestellt werden, um diesen bei dem ersten Test zu deaktivieren. Wenn der normale PID gut läuft, ein für dich angenehmes Heizverhalten sich beim Starten zeigt und stabil am Soll-Wert läuft, dann kannst du die Brüherkennung dir genauer anschauen.

## Konfiguration der Erkennung

Eine Bezugserkennnung wird unterschiedlich beim Only PID oder Vollausbau realisiert. Dieser kann in folgender Zeile in der Userconfig konfiguriert werden: 
```
#define BREWDETECTION 1            // 0 = off, 1 = Software (Onlypid 0), 2 = Hardware (Onlypid 0), 3 = Sensor/Hardware for Only PID 
```
Bei Only PID kann Auswahl 1 und 3 (nur mit zusätzlichen Equipment, dazu später mehr) und bei der Hardwarelösung (Vollausbau) Auswahl 2 genommen werden. Beim Vollausbau wird direkt der Brühschalter an den Controller angeschlossen, daher kann dieser direkt abgefragt werden.
Bei PID Only ist dem Controller nicht direkt bekannt, ob der Schalter gedrückt ist, daher wird per Software der Brühvorgang ermittelt. Diese ist im nachfolgenden Kapitel erläutert.
Als Ergänzung wurde eine Lösung zwischen Only PID und Vollausbau entwickelt (Only PID Plus). Hierbei wird der Brühschalter mit seiner regulären 230 Volt Verschaltung mit einem zusätzlichen Sensor überwacht, ob dieser gedrückt wird oder nicht, um dem Controller bekannt zu machen, dass der Schalter aktiv/nicht aktiv ist. Da es unterschiedliche Sensoren gibt, muss dieser konfiguriert werden, wie das Signal dem Controller übermittelt wird:
```
#define PINVOLTAGESENSOR  15    //Input pin for volatage sensor
// BREWDETECTION 3 configuration
#define VOLTAGESENSORTYPE HIGH 
#define PINMODEVOLTAGESENSOR INPUT // Mode INPUT_PULLUP, INPUT or INPUT_PULLDOWN_16 (Only Pin 16)
#define PINVOLTAGESENSOR  15    //Input pin for volatage sensor
```
Der PINVOLTAGESENSOR gibt den gewählten PIN an. "VOLTAGESENSORTYPE HIGH" bedeutet, dass ein HIGH Signal (3,3 Volt) anliegt, wenn der Schalter gedrückt ist und bei "VOLTAGESENSORTYPE LOW" ein LOW Signal anliegt (GND). Je nach gewählten PIN und Aufbau muss ggf. ein INPUT Pullup oder Pulldown (nur Pin 16) erfolgen (PINMODEVOLTAGESENSOR INPUT oder INPUT_PULLUP oder INPUT_PULLDOWN_16). Hintergrund ist, dass durch ein Pullup oder Pulldown der PIN definiert in LOW oder HIGH gehalten wird, um dann genauer das gegensätzliche Signal zu messen. 

Folgende Beispielkonfiguration gelten für folgende Sensoren:
1. Wago 859-358
https://www.wago.com/de/relais-optokopplermodule/relaismodul/p/859-358

Der Sensor erhält 3,3 Volt und die andere Seite wird mit dem PIN 15 verbunden
```
#define PINVOLTAGESENSOR  15    //Input pin for volatage sensor
// BREWDETECTION 3 configuration
#define VOLTAGESENSORTYPE HIGH 
#define PINMODEVOLTAGESENSOR INPUT // Mode INPUT_PULLUP, INPUT or INPUT_PULLDOWN_16 (Only Pin 16)
#define PINVOLTAGESENSOR  15    //Input pin for volatage sensor
```

2. 220V Sensor (Optokoppler - TTL AC 220V Isolation Modul SCM Test Board)

Der Sensor erhält 3,3 Volt und die andere Seite wird mit dem PIN 16 verbunden
https://www.funduinoshop.com/epages/78096195.mobile/de_DE/?ObjectPath=/Shops/78096195/Products/B-7-2&Locale=de_DE

```
#define PINVOLTAGESENSOR  16    //Input pin for volatage sensor
// BREWDETECTION 3 configuration
#define VOLTAGESENSORTYPE LOW 
#define PINMODEVOLTAGESENSOR INPUT // Mode INPUT_PULLUP, INPUT or INPUT_PULLDOWN_16 (Only Pin 16)
```

## Funktionsweise

Ohne zu tief in die technischen Details der Erkennung einzusteigen, soll dir dennoch kurz die grundlegende Funktionsweise erläutert werden. Der Mikrocontroller überwacht bei der Software Brüherkennung (BREWDETECTION 1 ) kontinuierlich die Temperatur. Dabei wird die zeitliche Veränderung der Heizrate/Kühlrate für fortlaufend Zeitfenster analysiert. Das Ergebnis ist dann die „heat average“. Wenn diese negativ wird, kühlt die Maschine ab, bei einem Hochheizen wird diese positiv.

![Brüherkennung](../../img/fullsizeoutput_1c57.jpeg)

Die Brüherkennung „horcht“ nun auf dieser „heat average“, in dem der negative Grenzwert definiert wird, ab dem die Maschine von einem Bezug ausgehen soll. Dieser wird bei „brew heater detection limit“ definiert. Hierbei ist zu beachten, dass hier der absolute Werte eingetragen wird: 70 entspricht -70. Die Übersetzung in den negativen Wert erfolgt im Quellcode!

Vereinfacht kann festgehalten werden, dass die „brew heater detection limit“ letztendlich die Empfindlichkeit der Erkennung wiedergibt: Je kleiner der Wert ist, je empfindlicher reagiert die Brüherkennung. Wenn die zu empfindlich (kleiner Wert, z.B. 5) ist, wird jedes normale Abkühlung als Brühvorgang erkannt, ist der Wert zu groß (z.B. 1000) wird erst zu spät oder gar nicht die Brüherkennung ausgelöst. Es kann dazu hilfreich sein den Verlauf der heat average über eine längere Zeit zu beobachten und somit einen geeigneten Werte zu finden.

Wenn die Erkennung ausgelöst werden, dann gelten für den definierten Zeitraum in „brew timer Software Seconds“ (im oberen Screenshot, 120 Sekunden) andere PID Werte. Somit kann der Regler nun aggressiver auf den Brühvorgang reagieren und schneller hochheizen. Wichtig ist hierbei, dass jede Unterschreitung des Grenzwertes zu einer Auslösung der Erkennung führt. Der Verlauf nach dem Auslösen wird nicht weiter ausgewertet, sondern die geänderten PID Werte gelten fix für die definierte Zeit nach der Erkennung des Bezuges.

## PID Werte
Die geänderten PID Werte gelten immer, wenn ein Brühvorgang erkannt wird, sei es per Sofware oder im Vollausbau durch die Abfrage am Brühschalter. Die Zeitdauer wird mit "brew timer Software Seconds" festgelegt in der Blynksteuerung. 
Für den kurzen Zeitraum muss der PID schnell wieder auf Temperatur kommen, ohne überzuschwingen. Hierzu muss vor allem der I-Anteil erhöht werden, damit sich der Regler nicht die erfolgte Abweichung vom Soll-Wert für die Zukunft „merkt“. Der D-Anteil kann auch erhöht werden, um den Regler beim Abfallen der Temperatur zu „beschleunigen“ und „abzubremsen“, wenn die Temperatur wieder Richtung Soll-Wert geht. Als Größenordnung können die Werte aus dem oberen Screenshot genommen werden.
In der nachfolgenden Tabelle sind bewährte PID für die Brüherkennung zu finden.

Maschine |	P |	I |	D | Timer |  Limit 
:-|-|-|-|-|-
Rancilio Silvia (nicht isoliert) | 50 | 0 | 20 | 120 | 45 
Rancilio Silvia E (isoliert) | 70 | 0 | 20 | 240 | 65 
Gaggia | 75 | 0 | 15 | 180 | 90 

## Vergleich bei einem Bezug

Ausgangssituation sind folgende PID Parameter:

![PID Parameter](../../img/Screenshot-at-M%C3%A4rz-15-07-47-28.png)

Bei dem Vergleich von einem Bezug mit und ohne Brüherkennung ist zu sehen, dass die Solltemperatur zu einem ähnlichen Zeitpunkt wieder „durchschritten“ wird, aber ohne Erkennung die Temperatur nach oben ausschlägt (96 °C). Die Erkennung kann hier ein deutlich besseres Ergebnis liefern (ca. 93,5 °C). Auch fällt die Temperatur nicht so rapide nach unten ab bei dem Bezug, da die Heizung schneller reagieren kann bei der Erkennung.

In der Praxis zeigt sich bei mir zu hause, dass bei Gästen zügig und reproduzierbar Espresso hintereinander gezogen werden können, da meistens die 3 Minuten ausreichen den Kaffee zu verteilen und neue Bohnen zu mahlen.

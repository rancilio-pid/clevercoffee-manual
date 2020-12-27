---
title: Aufbau und Einbau
parent: DE - Handbuch
grand_parent: DE - Handbuch
has_children: false
nav_order: 1
---

# Aufbau und Einbau der Hardware
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Trockenaufbau

Wenn ihr die einzelnen Komponenten beisammenhabt, startet ihr am besten mit einem Trockenaufbau außerhalb eurer Maschine. So könnt ihr das System zum Laufen bringen und kommt jederzeit problemlos an alle Stecker etc. heran.

Die Heizung eurer Maschine könnt ihr z. B. mit einer Glühbirne simulieren, jeder andere 230V Verbraucher tut es aber genauso gut.

![Trockenaufbau](http://rancilio-pid.de/wp-content/uploads/2020/10/image-2.png)

Das PCB für den Controller sieht wie folgt aus:

![PCB](http://rancilio-pid.de/wp-content/uploads/2020/10/image-3.png)


###  Grundversion PID-Only

Die einzelnen Komponenten werden wie folgt angeschlossen:

PIN | Belegung
-|-
PIN 14 | SSR Heizung     
PIN 2 | Temperatursensor
PIN 4 | Display-PIN SDA
PIN 5 | Display-PIN SCL
GND/Vin | Netzteil

### Vollausbau

Bei dem „Vollausbau“ wird noch die Steuerung für Magnetventil und Pumpe benötigt:

PIN | Belegung
-|-
PIN 12 | Relais Ansteuerung Magnetventil
PIN 13 | Relais Ansteuerung Pumpe

## Einbau

Besondere Sorgfalt müsst ihr bitte beim Anschließen des Temperatursensors TSIC306 walten lassen: sobald dieser einmal falsch angeschlossen Spannung bekommen hat, ist er entweder sofort zerstört oder zumindest vorgeschädigt und liefert dadurch fehlerhafte Messwerte. Daher ist es immer ratsam einen Ersatz-Sensor parat zu haben.

* Sensor V+ : Board PIN 2 5V
* Sensor Signal: Board PIN 2 Signal
* Sensor GND:  Board PIN 2 GND

![TSIC Sensor](http://rancilio-pid.de/wp-content/uploads/2020/11/z4fdgmmn8jyz8rrqojj157yxjh-20200503_223844-1152x1536.jpg)

Beim Anschließen des SSR zur Ansteuerung der Heizung ist es wichtig, dass die Polarität der SSR-Ports 3 und 4 beachtet werden:

* SSR Port 3 (+) : Board PIN 14 Signal
* SSR Port 4 (-) : Board PIN 14 GND

Damit habt ihr das System zum ersten Mal aufgebaut.

## Tipps & Tricks

Hier einige gesammelte Hinweise zum Einbau in die Maschine:

* Verbaut die Komponenten an einem trockenen Ort und möglichst entfernt von der Hitzequelle Boiler.

* Das SSR schaltet die Heizleistung von ca. 1.000 W, von daher kann eine Montage mit wärmeleitendem Kleber bzw. Klebepads nicht schaden.

*  Den Temperatursensor solltet ihr wenn möglich nicht nur an den Kessel ankleben, sondern fest verschrauben. Bei der Rancilio Silvia kann man dazu die Halteklammer des nun überflüssigen Brühthermostaten nutzen, bei der Gaggia Classic kann der Sensor am vorhandenen M4-Gewinde der Thermostataufnahme verschraubt werden.

* Zum Anschluss des Temperatursensors TSIC keine Steckverbinder nehmen, sondern Litze an die Beine des TSIC löten. Das ist etwas fummelig, aber dafür habt ihr weniger Neigung zu Wackelkontakten im verbauten Zustand.

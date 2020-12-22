---
title: Arduino IDE einrichten
has_children: false
nav_order: 1
---

# Arduino IDE einrichten

Inhaltsverzeichnis

* TOC
{:toc}

## Installationsvideo

In diesem kurzen Video erklären wir die Installation der Arduino IDE und zeigen wie unsere OpenSource Software Rancilio-PID auf dem NodeMCU installiert wird. Viel Spaß!

[![Installationsvideo](https://img.youtube.com/vi/w7vBGSVWPrw/hqdefault.jpg)](https://www.youtube.com/watch?v=w7vBGSVWPrw)

## Download

Wird benötigt, um den Code auf den Controller zu spielen.

https://www.arduino.cc/en/Main/Software

![Screenshot der Arduino Homepage](http://rancilio-pid.de/wp-content/uploads/2018/10/1.png)

## Der Programmcode

Download des aktuellen Programmcode findest du im aktuellen Release.

https://github.com/rancilio-pid/ranciliopid/releases

![Screenshot der Github Homepage](http://rancilio-pid.de/wp-content/uploads/2018/10/2.png)

## Installation der Arduino IDE

![Arduino Installation](./img/installation.gif)

Hinweise zur Installation befinden sich auf der [Arduino Homepage](https://www.arduino.cc/en/Guide).

Nach der erfolgreichen Installation kann Arduino über das Startmenü gestartet werden.

## Arduino Voreinstellungen

### Boardverwaltungs-URL anlegen

Wir benötigen für den Einsatz des NodeMCUs eine zusätzliche Boardverwaltungs-URL.

Diese erreicht ihr unter: Datei > Voreinstellungen

| Key | Value |
|-|-|
| Boardverwaltungs-URL | `http://arduino.esp8266.com/stable/package_esp8266com_index.json`|

<details markdown="block">
  <summary> Windows </summary>

  ![Windows Arduino Voreinstellungen](http://rancilio-pid.de/wp-content/uploads/2018/10/8.png)

</details>

<details markdown="block">
  <summary> Linux (Ubuntu) </summary>

  ![Linux (Ubuntu)](img/arduino-voreinstellungen-ubu.png)

</details>

### Boardtreiber installieren

Als nächstes müssen die ESP8266 Boardtreiber installiert werden.

Dies erreicht ihr unter: Werkzeuge > Board: "[\<Version\>]" > Boardverwalter...

<details markdown="block">
  <summary> Windows </summary>

  ![Windows Arduino Boardverwalter](http://rancilio-pid.de/wp-content/uploads/2018/10/9.png)

</details>

<details markdown="block">
  <summary> Linux (Ubuntu) </summary>

  ![Linux (Ubuntu) Boardverwalter](img/arduino-boardverwalter-ubu.png)

</details>

Bitte die aktuelle Version installieren.

Typ \<Alle\> > "esp": "**esp8266** by **ESP8266 Community**"

![ESP8266 installieren](./img/boardtreiber.gif)

Nun ist die Arduino IDE vorbereitet. Weiter geht es mit den Bibliotheken.

## Bibliotheken installieren

Der sicherste und einfachste Weg alle Bibliotheken korrekt zu installieren, ist es, die [Bibliotheken aus Github](https://github.com/rancilio-pid/ranciliopid/tree/master/rancilio-pid/libraries) zu nehmen. Diese solltet ihr bereits heruntergeladen haben (siehe [Programmcode](#der-programmcode)). Kopiert die kompletten Ordner einfach in den Arduino Libraries Ordner zu kopieren:

| OS | Arduino Libraries Ordner |
|-|-|
| Windows | `My Documents\Arduino\libraries\` |
| OSX | `~/Documents/Arduino/libraries/` |
| Linux |`~/Arduino/libraries`|

Wie immer ist es empfehlenswert beim offiziellen Guide mehr Infos einzuholen: [Link](https://www.arduino.cc/en/Guide/Libraries).

### Bibliotheken manuell installieren

Alternativ müssen folgende Libraries per Hand installiert werden:

* Blynk
* TimeLib
* WidgetRTC
* U8x8lib
* OneWire
* DallasTemperature
* PID_v1.h

Die Installation der einzelnen Bibliotheken erfolgt wieder über die Verwaltung in Arduino IDE:

![Bibliotheken verwalten](http://rancilio-pid.de/wp-content/uploads/2018/10/12.png)

<details markdown="block">
  <summary> OneWire </summary>

  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/13.png)
</details>

<details markdown="block">
  <summary>
    DallasTemperature
  </summary>

![](http://rancilio-pid.de/wp-content/uploads/2018/10/14.png)
</details>

<details markdown="block">
  <summary> U8x8lib </summary>

  1. Geht auf https://github.com/olikraus/u8g2
  1. Code > Download Zip
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/15.png)
  1. Legt die Dateien im [Arduino Libraries Ordner](#bibliotheken-installieren) ab
  1. Erstellen einen Ordner: `U8x8lib`
  1. Den Inhalt aus dem ZIP File Ordner: u8g2-master.zip\u8g2-master\cppsrc  UND csrc in den neu erstellten Ordner kopieren (ja, es sind eine ganze Menge Dateien :))
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/16.png)
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/17.png)  
</details>

<details markdown="block">
  <summary> PID_v1.h </summary>

  1. Geht auf https://github.com/br3ttb/Arduino-PID-Library
  1. Code > Download Zip  
  ![](./img/arduino-pid-lib.png)
  1. Legt die Dateien im [Arduino Libraries Ordner](#bibliotheken-installieren) ab
  1. Erstellen einen Ordner: `PID_v1`
  1. Die vier Dateien aus dem ZIP File kopieren und in den neuen Ordner einfügen:
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/19.png)
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/20.png)  
</details>

<details markdown="block">
  <summary> Blynk </summary>

  1. Geht auf https://www.blynk.cc/getting-started/
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/21.png)
  1. Geht auf https://github.com/blynkkk/blynk-library/releases/tag/v0.5.4
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/22.png)
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/23.png)
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/25.png)
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/26.png)
  1. Wechseln in den [Arduino Libraries Ordner](#bibliotheken-installieren)
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/27.png)
  ![](http://rancilio-pid.de/wp-content/uploads/2018/10/28.png)  
</details>

## Board einstellen

![](http://rancilio-pid.de/wp-content/uploads/2018/10/29.png)
![](http://rancilio-pid.de/wp-content/uploads/2019/07/Bildschirmfoto-2019-07-03-um-00.01.26.png)

Wenn alle Bibliotheken installiert sind, müsste es wie folgt aussehen:

![](http://rancilio-pid.de/wp-content/uploads/2018/10/31.png)

Somit ist alles nun für das Einrichten von Blynk und das Flashen von dem Code vorbereitet. Dann kann der erste Test beginnen.

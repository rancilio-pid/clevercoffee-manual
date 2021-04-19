---
layout: default
title: Visual Studio Code mit PlatformIO einrichten
parent: Software Teil I
grand_parent: DE - Handbuch
has_children: false
nav_order: 1
---

#   {{ page.title }}

<details open markdown="block">
  <summary>
    Inhaltsverzeichnis
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

# Einführung

[Visual Studio Code](https://code.visualstudio.com/) ist ein plattformübergreifend verfügbarer Code-Editor, das sich über zahlreiche Plugins erweitern lässt. Eines für die Entwicklung eingebetteter Systeme hilfreichsten Plugins ist [PlatformIO](https://platformio.org/)

## Installationsvideo

In diesem kurzen Video erklären wir die Installation der Arduino IDE und zeigen wie unsere OpenSource Software Rancilio-PID auf dem NodeMCU installiert wird. Viel Spaß!

[![Installationsvideo](https://img.youtube.com/vi/w7vBGSVWPrw/hqdefault.jpg)](https://www.youtube.com/watch?v=w7vBGSVWPrw)

## Download

Wird benötigt, um den Code auf den Controller zu spielen.

[Link zu Arduino](https://www.arduino.cc/en/Main/Software)

![Screenshot der Arduino Homepage](../../img/1.png)

## Der Programmcode

Download des aktuellen Programmcode findest du im aktuellen Release.

[Link zum Github Repository](https://github.com/rancilio-pid/ranciliopid/releases)

![Screenshot der Github Homepage](../../img/2.png)

## Installation der Arduino IDE

![Arduino Installation](../../img/installation.gif)

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

  ![Windows Arduino Voreinstellungen](../../img/8.png)

</details>

<details markdown="block">
  <summary> Linux (Ubuntu) </summary>

  ![Linux (Ubuntu)](../../img/arduino-voreinstellungen-ubu.png)

</details>

### Boardtreiber installieren

Als nächstes müssen die ESP8266 Boardtreiber installiert werden.

Dies erreicht ihr unter: Werkzeuge > Board: "[\<Version\>]" > Boardverwalter...

<details markdown="block">
  <summary> Windows </summary>

  ![Windows Arduino Boardverwalter](../../img/9.png)

</details>

<details markdown="block">
  <summary> Linux (Ubuntu) </summary>

  ![Linux (Ubuntu) Boardverwalter](../../img/arduino-boardverwalter-ubu.png)

</details>

Bitte die aktuelle Version installieren.

Typ \<Alle\> > "esp": "**esp8266** by **ESP8266 Community**"

![ESP8266 installieren](../../img/boardtreiber.gif)

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
* Adafruit VL53L0X

Die Installation der einzelnen Bibliotheken erfolgt wieder über die Verwaltung in Arduino IDE:

![Bibliotheken verwalten](../../img/12.png)

<details markdown="block">
  <summary> OneWire </summary>

  ![](../../img/13.png)
</details>

<details markdown="block">
  <summary>
    DallasTemperature
  </summary>

![](../../img/14.png)
</details>

<details markdown="block">
  <summary> U8x8lib </summary>

  1. Geht auf [https://github.com/olikraus/u8g2](https://github.com/olikraus/u8g2)
  1. Code > Download Zip
  ![](../../img/15.png)
  1. Legt die Dateien im [Arduino Libraries Ordner](#bibliotheken-installieren) ab
  1. Erstellen einen Ordner: `U8x8lib`
  1. Den Inhalt aus dem ZIP File Ordner: u8g2-master.zip\u8g2-master\cppsrc  UND csrc in den neu erstellten Ordner kopieren (ja, es sind eine ganze Menge Dateien :))
  ![](../../img/16.png)
  ![](../../img/17.png)  
</details>

<details markdown="block">
  <summary> PID_v1.h </summary>

  1. Geht auf [https://github.com/br3ttb/Arduino-PID-Library](https://github.com/br3ttb/Arduino-PID-Library)
  1. Code > Download Zip  
  ![](../../img/arduino-pid-lib.png)
  1. Legt die Dateien im [Arduino Libraries Ordner](#bibliotheken-installieren) ab
  1. Erstellen einen Ordner: `PID_v1`
  1. Die vier Dateien aus dem ZIP File kopieren und in den neuen Ordner einfügen:
  ![](../../img/19.png)
  ![](../../img/20.png)  
</details>

<details markdown="block">
  <summary> Blynk </summary>

  1. Geht auf [https://www.blynk.cc/getting-started/](https://www.blynk.cc/getting-started/)
  ![](../../img/21.png)
  1. Geht auf [https://github.com/blynkkk/blynk-library/releases/tag/v0.5.4](https://github.com/blynkkk/blynk-library/releases/tag/v0.5.4)
  ![](../../img/22.png)
  ![](../../img/23.png)
  ![](../../img/25.png)
  ![](../../img/26.png)
  1. Wechseln in den [Arduino Libraries Ordner](#bibliotheken-installieren)
  ![](../../img/27.png)
  ![](../../img/28.png)  
</details>

## Board einstellen

![](../../img/29.png)
![](../../img/Bildschirmfoto-2019-07-03-um-00.01.26.png)

Wenn alle Bibliotheken installiert sind, müsste es wie folgt aussehen:

![](../../img/31.png)

Somit ist alles nun für das Einrichten von Blynk und das Flashen von dem Code vorbereitet. Dann kann der erste Test beginnen.

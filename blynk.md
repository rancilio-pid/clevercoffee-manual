---
title: Einrichtung von Blynk
has_children: false
nav_order: 3
---

# Einrichtung von Blynk

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

Als nächstes richtet ihr zur Bedienung des PIDs auf eurem Smartphone die App Blynk ein. Blynk ist ein Cloud“-Dienst, über den der NodeMCU mit dem Handy oder Tablet steuerbar ist. Freundlicherweise steht uns ein eigener Blynk Server zur Verfügung, den Markus hostet. Natürlich könntet Ihr auch den Public Server von Blynk nutzen, hättet ggf. aber Kosten für das Einrichten der App.

Vom Prinzip funktioniert es wie folgt:

Die Maschine sendet Daten an einen Blynk-Server. Die App greift ebenfalls auf den Server zu und holt sich die benötigten Daten ab. Das Ganze funktioniert bidirektional: der Blynk-Server stellt einerseits die Parameter zum Betrieb des PIDs bereit, andererseits empfängt er auch vom PID die Daten zum aktuellen Betriebszustand der Maschine. Ein Auth Token stellt hierbei sicher, dass nur euere Maschine gesteuert wird.

Auch hierzu hat Markus ein Video auf Youtube, in dem die Installation gut erläutert wird.

## Video: Installieren und einrichten der Blynk App

[![Installationsvideo](https://img.youtube.com/vi/JHDRUN044gQ/hqdefault.jpg)](https://www.youtube.com/watch?v=JHDRUN044gQ)

## Schritt 1: App herunterladen

https://www.blynk.cc/ gibt es für alle gängigen Betriebssysteme

## Schritt 2: Account anlegen

Öffnet hierzu die Blynk-App & Klickt auf „Create New Account“

![](http://rancilio-pid.de/wp-content/uploads/2018/10/IMG_0115-576x1024.png)

Klickt jetzt zuerst auf das Ampel-Symbol um den Server zu wechseln!
Sonst nutzt Ihr den „normalen Blynk“-Server.

![](http://rancilio-pid.de/wp-content/uploads/2018/10/IMG_0116-576x1024.png)

**WICHTIG**:

Legt den Schalter auf „Custom“ um.
Als Server tragt Ihr: blynk.remoteapp.de
Port: 9443
Bestätigt die Eingabe mit „OK“

...

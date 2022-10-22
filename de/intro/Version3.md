---
layout: default
title: Version 3.0.0 & Upgrade von 2.X.X
parent: Einführung
grand_parent: DE - Handbuch
has_children: false
nav_order: 4
---

# Was ist anders bei Version 3.0.0 ? 
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}


## Einführung
[![Installationsvideo](https://img.youtube.com/vi/KZPjisOEcQ4/hqdefault.jpg)](https://www.youtube.com/watch?v=KZPjisOEcQ4)


Mit der Version 3.0.0 ändern sich wesentliche Konzepte der PID. Das Handbuch konnte noch nicht vollständig aktualisiert werden.
Mit dem Release der Version 3.0.0 werden wir das Handbuch auch schrittweise aktualisieren. Diese Übersicht gibt euch die wichtigsten Änderungen im Überblick.  

## Einrichtung
Der Ardunio IDE wird nicht mehr aktiv von uns unterstüzt. Wir setzen ab der 3.0.0 nun vollständig auf Platform IO und VS Code.

## Funktionen

### Wifi Manager
Für die Ersteinrichtung wird der Wifi-Manager benutzt. Beim ersten Start vom Nodemcu wird ein Access Point von diesem geöffnet mit dem Namen "silvia" und Passwort "CleverCoffee". Dies kann in der Userconfig auch konfiguriert werden. Verbindet euch mit Access Point, wählt euer WLAN aus und gibt euer Passwort ein, dann wird dies automatisch gespeichert beim nächsten Start.      

### Webseite & Blynk 
Blynk wird noch unterstützt, ist aber nicht mehr das zentrale Bedienelement von der PID. Wir haben nun eine eigene auf dem NodeMCU gehostet Webseite.
Die IP von dem NodeMCU könnt ihr in eurem Router herausfinden oder per Monitor vom NodeMCU. Es bietet sich an dem NodeMCU eine feste IP über den Router zu vergeben.

## Wie upgrade ich von einer ältern Version (2.X.X oder jünger)? 
Es müssen wichtige Schritte vor dem Upgraden durchgeführt werden, sonst wird euer PID nicht richtig funktionieren.
In Platform IO (VS Code) müssen folgende Schritte erfolgen, eine USB Verbindung zum NodeMCU ist zwingend notwendig:
Schritt | Erklärung
:--|:--
1) Erease FLASH | nodemcuv2_usb -> Platform -> Erase Flash
2) Build Filesystem | nodemcuv2_usb -> Platform -> Buid Fileystem Image
3) Upload FileSystem Image | Upload Fileystem Image

Alle 3 Schritte müssen nach einander erfolgen.
 
![Update](../../img/platformio_upgrade.png)
 

## Helft uns!
Habt ihr Bugs oder ähnliches gefunden, lasst es uns bitte wissen. 

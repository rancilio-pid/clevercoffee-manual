---
title: Code Laden
parent: Der erste Test
has_children: false
nav_order: 2
---

# Code Laden

Inhaltsverzeichnis

* TOC
{:toc}

## Code auf den Controller laden

Im aktuellen Release befinden sich zwei Datein:
* rancilio-pid.ino
* userConfig.h

Die rancilio-pid.ino ist das eigentliche Programmcode und die userConfig.h eine ausgelagerte Konfigurationsdatei. Diese einhaltet folgende Punkte.

### Vorab Konfig

Die wichtigsten Funktionen müssen hier parametriert werden. Denkt daran, den richtigen PID Mode, Temperatursensor und das ggf. passende Display auszuwählen.

```
define DISPLAY 2 // 1=U8x8libm, 0=Deaktiviert, 2=Externes 128x64 Display

define OFFLINEMODUS 0 // 0=Blynk und WLAN wird benötigt 1=OfflineModus (ACHTUNG EINSTELLUNGEN NUR DIREKT IM CODE MÖGLICH)

define ONLYPID 0 // 1=Nur PID ohne Preinfussion, 0=PID + Preinfussion

define TEMPSENSOR 2 // 1=DS19B20; 2=TSIC306

define BREWDETECTION 1 // 0 = off ,1 = Software, 2 = Hardware

define FALLBACK 1 // 1: fallback auf eeprom Werte, wenn blynk nicht geht 0: deaktiviert

define TRIGGERTYPE HIGH // LOW = low trigger, HIGH = high trigger relay

define OTA true // true=activate update via OTA

define PONE 1 // 1 = P_ON_E (normal), 0 = P_ON_M (spezieller PID Modus, ACHTUNG andere Formel zur Berechnung)
```

### Wifi

Unter Wifi müsst ihr euren Auth Token aus Blynk eintragen und eure Wlan SSID und das zugehörige Passwort. Bei der WLAN SSID bitte drauf achten, dass keine Leerzeichen darin enthalten sind! Auch Sonderzeichen machen gerne Schwierigkeiten im Betrieb.

```
#define AUTH "blynkauthcode"

#define D_SSID "wlanname"

#define PASS "wlanpass"
```

### OTA

Hier wird der Update **O**ver **T**he **A**ir eingestellt.

### PID

Hier definiert ihr eure initialen PID Werte.

## Temperatursensor anschließen

Wie ihr zu der Beschreibung zum Board sehen könnt, muss an Pin 2 der Temperatursensor angeschlossen werden. Die oberen Ports (14, 2, 12, 13, 15) sind einheitlich jeweils von links nach rechts mit Minus(-), Signal, 5V(+) belegt.

![](http://rancilio-pid.de/wp-content/uploads/2020/05/20200503_223844-scaled.jpg)

Da wir öfters hören, dass die Bildbeschreibung zum TISIC nicht gut ist, haben wir hier nochmals die Pins vom Sensor dargestellt. Die flache Seite liegt unten. Ein falsch gepolter TISIC sollte entsorgt werden! Er misst vermeintlich richtig, aber definitiv nicht mehr genau.

## PIN Belegung vom PCB

Pin|Funktion
-|-
Pin 12| Relay für das Ventil
Pin 13| Relay für die Pumpe
Pin 15| frei
Pin 14| Relay für die Heizung
Pin 2| Temperatursensor
A0| Schalter Brühtaste
|
Pin 4| SDA
Pin 5| SCL
Pin 16| frei

![](http://rancilio-pid.de/wp-content/uploads/2019/03/Screenshot-at-M%C3%A4rz-10-20-53-04.png)

## Code hochladen und testen

Wenn ihr die .ino Datei öffnet, öffnet sich automatisch im zweiten Tab die userConfig.h mit den wichtigen Einstellungen. Danach auf den Pfeil klicken Achtet drauf, dass Ihr schon einen Auth-Code der Blynk-App und die WLAN-Zugangsdaten im Code der userConfig.h hinterlegt habt.

![](http://rancilio-pid.de/wp-content/uploads/2019/07/image-2.png)

Bitte achtet vorher drauf, dass Ihr in den Board Einstellungen den richtigen COM Port ausgewählt habt.

Diesen könnt ihr auch auch im Gerätemanager prüfen (falls ihr ihn nicht wisst)

![](http://rancilio-pid.de/wp-content/uploads/2018/10/34.png)

![](http://rancilio-pid.de/wp-content/uploads/2018/10/35.png)

Den erfolgreichen Test könnt ihr einmal am Handy die Raumtemperatur sehen, wenn ihr korrekt den Temperatursensor angeschlossen habt, und auf dem Serial Monitor erkennen, wie sich der NodeMCU mit Blynk verbindet.

![](http://rancilio-pid.de/wp-content/uploads/2018/10/36.png)

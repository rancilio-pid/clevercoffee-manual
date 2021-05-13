---
layout: default
title: Software Teil II
parent: DE - Handbuch
has_children: false
nav_order: 4
---

# Software Teil II
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

In diesem Kapitel wird beschrieben wie der Code auf den Mikrocontroller (NodeMCU) geladen wird. Damit könnt ihr loslegen, sobald ihr den Mikrocontroller zur Hand habt (weitere Teile werden nicht hierfür nicht benötigt). Für einen Test sollte dann zumindest der Temperatursensor angeschlossen werden.

## userConfig.h
In dem rancilio-pid/rancilio-pid Ordner befindet sich eine für euch wichtige Datei: 
* userConfig_sample.h

Die userConfig_sample.h muss in userConfig.h umbenannt werden und mit euren Werten anpasste werden. 
Alle wichtigen Einstellungen werden für eure PID in dieser Datei vorgenommen, diese werden nun gleich genauer erläutert.
Bei einem Update auf eine neuere Version bitte unbedingt die neuste userConfig_sample.h nehmen und mit eueren Werten anpassen.
Wenn Ihr das nicht tut, kann dies zu unspezifischen, nicht erwünschten Verhalten an der Maschine kommen: Display hängt, PID geht nicht und weitere


## Die Parameter in der userConfig.h

Die userConfig.h ist in mehrere Abschnitte unterteilt. Die wir nun nach und nach euch vorstellen werden. 


### MACHINETYPE, use the exakt name of the machine 
```
MACHINE machine = RancilioSilvia;      //	RancilioSilvia, RancilioSilviaE, Gaggia, QuickMill
```
Hier müsst ihr eure Maschine eintragen, dieser Parameter steuert die Logodarstellung auf dem Display (wenn angeschlossen) und bei der Quickmill die Erkennung des Brühvorgangs und den Dampfmodus bei BREWDETECTION 3 

### MACHINETYPE, use the exakt name of the machine 

```
#define DISPLAY 2                  // 0 = deactivated, 1 = SH1106 (e.g. 1.3 "128x64), 2 = SSD1306 (e.g. 0.96" 128x64)
#define OLED_I2C 0x3C		           // I2C address for OLED, 0x3C by default
#define DISPLAYTEMPLATE 3          // 1 = Standard Display Template, 2 = Minimal Template, 3 = only Temperatur, 4 = Scale Template, 20 = vertical Display see git Handbook for further information
#define DISPLAYROTATE U8G2_R0      // rotate display clockwise: U8G2_R0 = no rotation; U8G2_R1 = 90°; U8G2_R2 = 180°; U8G2_R3 = 270°
#define SHOTTIMER 1                // 0 = deactivated, 1 = activated 2 = with scale
#define HEATINGLOGO 0              // 0 = deactivated, 1 = Rancilio, 2 = Gaggia 
#define OFFLINEGLOGO 1             // 0 = deactivated, 1 = activated
#define BREWSWITCHDELAY 3000       // time in ms
#define LANGUAGE 1                 // LANGUAGE = 0 (DE), LANGUAGE = 1 (EN), LANGUAGE = 2 (ES)
```
DISPLAY definiert den Displaytyp. 

OLED_I2C gibt die I2C Adresse an, hier muss in der Regel nichts angepasst werden.  

DISPLAYTEMPLATE definiert das Template was ihr verwenden möchtet, siehe [Displayausgabe](https://manual.rancilio-pid.de/de/customization/Display.html).

DISPLAYROTATE lässt das Display rotieren. Beim Hochformat kann ein entsprechendes vertikale Displaytemplate verwendet werden.

SHOTTIMER lässt euch den Shottimer aktivieren (1), bei der Verwendung einer Waage kann (2) ausgewählt werden, um auch das Gewicht zu sehen.

HEATINGLOGO zeigt euch bis kurz vor Erreichen der Solltemperatur ein entsprechendes Logo anzeigen.

OFFLINEGLOGO zeigt euch beim deaktivieren der PID via Blynk ein Logo an.

BREWSWITCHDELAY ermöglicht euch einzustellen, wie lange die letzte Dauer beim Bezug im Display angezeigt werden soll.

LANGUAGE sollte selbsterklärend sein. 
```
// Wlan and Connection

// Offline mode
#define OFFLINEMODUS 0             // 0 = Blynk and Wifi are used, 1 = offline mode (only preconfigured values in code are used!)
#define FALLBACK 1                 // 1 = fallback to values stored in eeprom, 0 = deactivated
#define GRAFANA 1                  // 1 = grafana visualisation (access required), 0 = off (default)

// PID & Hardware
#define ONLYPID 1                  // 1 = Only PID, 0 = PID and preinfusion
#define ONLYPIDSCALE 0             // 0 = off , 1= OnlyPID with Scale
#define BREWMODE 1                 // 1 = NORMAL preinfusion ; 2 = Scale with weight
#define BREWDETECTION 1            // 0 = off, 1 = Software (Onlypid 1), 2 = Hardware (Onlypid 0), 3 = Sensor/Hardware for Only PID 
#define COLDSTART_PID 1            // 1 = default coldstart values, 2 = custom values via blynk (expert mode activated) 
#define TRIGGERTYPE HIGH           // LOW = low trigger, HIGH = high trigger relay // BREWDETECTION 3 configuration
#define VOLTAGESENSORTYPE HIGH 
#define PINMODEVOLTAGESENSOR INPUT // Mode INPUT_PULLUP, INPUT or INPUT_PULLDOWN_16 (Only Pin 16)

// TOF sensor for water level
#define TOF 0                      // 0 = no TOF sensor connected; 1 = water level by TOF sensor
#define TOF_I2C 0x29               // I2C address of TOF sensor; 0x29 by default
#define CALIBRATION_MODE 0         // 1 = enable to obtain water level calibration values; 0 = disable for normal PID operation; can also be done in Blynk
#define WATER_FULL 102             // value for full water tank (=100%) obtained in calibration procedure (in mm); can also be set in Blynk
#define WATER_EMPTY 205            // value for empty water tank (=0%) obtained in calibration procedure (in mm); can also be set in Blynk

// E-Trigger
#define ETRIGGER 0                 // 0 = no trigger (for Rancilio except Rancilio E), 1 = trigger for CPU of Rancilio E
#define ETRIGGERTIME 60            // seconds, time between trigger signal
#define TRIGGERRELAYTYPE HIGH      // LOW = low trigger, HIGH = high trigger relay for E-Trigger

//Weight SCALE
#define WEIGHTSETPOINT 30          // Gramm 

/// Wifi 
#define HOSTNAME "rancilio"
#define D_SSID "myssid"
#define PASS "mypass"
#define MAXWIFIRECONNECTS 5        // maximum number of reconnection attempts, use -1 to deactivate
#define WIFICINNECTIONDELAY 10000  // delay between reconnects in ms

// OTA
#define OTA true                   // true = OTA activated, false = OTA deactivated
#define OTAHOST "rancilio"         // Name to be shown in ARUDINO IDE Port
#define OTAPASS "otapass"          // Password for OTA updtates

// MQTT
#define MQTT 0                     // 1 = MQTT enabled, 0 = MQTT disabled
#define MQTT_USERNAME "mymqttuser"
#define MQTT_PASSWORD "mymqttpass"
#define MQTT_TOPIC_PREFIX "custom/Küche."  // topic will be "<MQTT_TOPIC_PREFIX><HOSTNAME>/<READING>"
#define MQTT_SERVER_IP "XXX.XXX.XXX.XXX"  // IP-Address of locally installed mqtt server
#define MQTT_SERVER_PORT 1883    

// BLynk
#define AUTH "myauth"
#define BLYNKADDRESS "blynk.clevercoffee.de"  // blynk-server IP-Address
#define BLYNKPORT 8080             // blynk-server portver 

// PID - offline values
#define SETPOINT 95                // Temperatur setpoint
#define STEAMSETPOINT 120          // Temperatur setpoint
#define AGGKP 69                   // Kp normal
#define AGGTN 399                  // Tn
#define AGGTV 0                    // Tv

// PID coldstart
#define STARTKP 50                 // Start Kp during coldstart
#define STARTTN 150                // Start Tn during cold start

// PID - offline brewdetection values
#define AGGBKP 50                  // Kp
#define AGGBTN 0                   // Tn 
#define AGGBTV 20                  // Tv

// Backflush values
#define FILLTIME 3000              // time in ms the pump is running
#define FLUSHTIME 6000             // time in ms the 3-way valve is open -> backflush
#define MAXFLUSHCYCLES 5           // number of cycles the backflush should run, 0 = disabled

// Pin Layout
#define ONE_WIRE_BUS 2             // Temp sensor pin
#define PINBREWSWITCH 0           // 0: A0 Analog PIN ; >0 : DIGITAL PIN, ESP8266: ONLY USE PIN15 AND PIN16! 
#define pinRelayVentil 12          // Output pin for 3-way-valve
#define pinRelayPumpe 13           // Output pin for pump
#define pinRelayHeater 14          // Output pin for heater
#define PINVOLTAGESENSOR  15       //Input pin for volatage sensor
//#define OLED_RESET 16            // Output pin for dispaly reset pin
#define PINETRIGGER 16             // PIN for E-Trigger relay
#define STEAMONPIN 17              // STEAM active
#define OLED_SCL 5                 // Output pin for dispaly clock pin
#define OLED_SDA 4                 // Output pin for dispaly data pin
#define HXDATPIN 99                // weight scale PIN 
#define HXCLKPIN 99                // weight scale PIN  
#define SCREEN_WIDTH 128           // OLED display width, in pixels
#define SCREEN_HEIGHT 64           // OLED display height, in pixels  

// Historic (no settings)
#define PONE 1                     // 1 = P_ON_E (default), 0 = P_ON_M (special PID mode, other PID-parameter are needed)
#define TEMPSENSOR 2               // 2 = TSIC306 1=DS18B20


// Check BrewSwitch
#if (defined(ESP8266) && ((PINBREWSWITCH != 15 && PINBREWSWITCH != 0 && PINBREWSWITCH != 16 )))
  #error("WRONG Brewswitch PIN for ESP8266, Only PIN 15 and PIN 16");  
#endif


#endif // _userConfig_H
```


### Wifi

Unter Wifi müsst ihr euren Auth Token aus Blynk eintragen und eure Wlan SSID und das zugehörige Passwort. Bei der WLAN SSID bitte drauf achten, dass keine Leerzeichen darin enthalten sind! Auch Sonderzeichen machen gerne Schwierigkeiten im Betrieb.

```
#define AUTH "blynkauthcode"

#define D_SSID "wlanname"

#define PASS "wlanpass"
```

### PID

Hier definiert ihr eure initialen PID Werte.


## Code hochladen

Wenn ihr die .ino Datei öffnet, öffnet sich automatisch im zweiten Tab die userConfig.h mit den wichtigen Einstellungen. Danach auf den Pfeil klicken für den Upload auf den Microkontroller. Achtet darauf, dass Ihr den Auth-Code der Blynk-App und die WLAN-Zugangsdaten im Code der userConfig.h hinterlegt habt.

![](../img/image-2.png)

Bitte achtet vorher drauf, dass Ihr in den Board Einstellungen den richtigen COM Port ausgewählt habt.

Diesen könnt ihr auch auch im Gerätemanager prüfen (falls ihr ihn nicht wisst):

![](../img/34.png)

![](../img/35.png)

## Testen

Wenn alles geklappt habt könnt ihr auf dem Serial Monitor erkennen, wie sich der Microkontroller mit Blynk verbindet.

![](../img/36.png)

Klappt das und ist der Temperatursensor korrekt angeschlossen seht ihr am Handy in der Blynk App die Raumtemperatur.
Jetzt könnt iht nach und nach die anderen Bauteile verbinden (Relais) und weiter testen.

### OTA

Hier wird der Update **O**ver **T**he **A**ir eingestellt.

Dafür muss die Maschine eingeschalten sein und sich euer Rechner (mit Arduino) im selben WLAN Netz befinden. Dann erscheint unter Werkzeuge > Port <aktuelle Auswahl> > Netzwerkschnittstellen "Rancilio <IP-Addresse>". Wählt diesen Port aus und lädt den Code entsprechend hoch.

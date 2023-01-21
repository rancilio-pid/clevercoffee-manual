---
layout: default
title: Ersteinrichtung WLAN
parent: Software
grand_parent: DE - Handbuch
has_children: false
nav_order: 5
---


# Ersteinrichtung WLAN
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## WICHTIGER HINWEIS
Am ESP8266 gibt es ein Problem bei der Ersteinrichtung. Der NodeMCU stürzt immer wieder ab, wenn der Access Point geöffnet wird. Als Lösung muss für die Ersteinrichtung das OLED_DISPLAY auf 0 gesetzt werden in der Konfig. Danach könnt ihr die Einrichtung vom WLAN machen und danach wieder auf 1 oder 2 setzen und erneut den Code auf den Controller laden. 
Das Problem tritt nicht beim ESP32 auf.

## Kurzfassung

Für die Ersteinrichtung wird der Wifi-Manager benutzt. Beim ersten Start vom Mikrocontroller wird ein Access Point von diesem geöffnet mit dem in der userConfig.h eingestellten ```HOSTNAME``` (default: "silvia") und Passwort ```PASS``` (default: "CleverCoffee"). Verbindet euch mit dem Access Point, wählt euer WLAN aus und gebt das Passwort des Netzwerks ein, dann wird dieses gespeichert und beim nächsten Start automatisch verwendet.
Der ESP wird immer für 10 Sekunden versuchen, dass eingerichtete WLAN zu erreichen, falls dies nicht möglich ist, wird für 60 Sekunden das Konfigurationsportal wieder gestartet. Falls kein Zugriff auf das Portal passiert, startet die Maschine im Offline-Modus.
## Schritt für Schritt
Wenn ihr den Code hochladet, ist im Log (Monitor-Befehl) etwa folgendes zu sehen:

```
*wm:[1] AutoConnect 
*wm:[1] No Credentials are Saved, skipping connect 
*wm:[2] Starting Config Portal 
*wm:[2] AccessPoint set password is VALID 
*wm:[2] Disabling STA 
*wm:[2] Enabling AP 
*wm:[1] StartAP with SSID:  silvia
*wm:[1] AP IP address: 192.168.4.1
*wm:[1] Starting Web Portal 
*wm:[2] HTTP server started 
*wm:[2] Config Portal Running, blocking, waiting for clients... 
```
Diese IP-Adresse solltet ihr euch notieren, um später die Webseite für die Ersteinrichtung aufzurufen (falls diese nicht automatisch geöffnet wird).
Wenn ihr nun per Mobile/Tablet/Desktop nach einem Wlan sucht werdet ihr das Netzwerk "silvia" sehen.

![](../../img/wlan-setup1.PNG)

Wenn ihr euch mit dem Netzwerk verbunden habt, geht eine Portalseite auf oder ihr gibt per Browser die IP 192.168.4.1 ein.

![](../../img/wlan-setup2.PNG)

Mit dem Klick auf "Configure Wifi" könnt ihr eurer Wlan auf dem Nodemcu einrichten.

![](../../img/wlan-setup3.PNG)

Wählt das Netzwerk oben aus der Liste ein oder gebt eure SSID manuell ein, zusätzlich eurer Passwort vom Wlan.
Nach dem "Save" sollte der ESP neu starten und ist für euer Wlan eingerichtet.

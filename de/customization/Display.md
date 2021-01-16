---
title: Display
parent: Konfiguration & Anpassung
grand_parent: DE - Handbuch
has_children: false
nav_order: 4
---

# Display
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung
Es stehen dir aktuell 2 Designs für dein Display zur Verfügung.
Diese können in der Userconfig mit ausgewählt werden
#define DISPLAYTEMPLATE 1    // 1: Standard Display Template, 2: Minimal Template, 

## Standard Design - DISPLAYTEMPLATE 1 
![Display Template 1](../../img/Displaytemplate1.png)

Erläuterung zur Anzeige: 
Oben sind von (links) folgende Symbole zu sehen:
* Wlan (Durchgestrichen wenn kein Empfang)
* Blynk (Durchgestrichen wenn kein Blynk vorhanden)
* MQTT (Wenn MQTT aktiviert ist)
* Offline (wenn kein Wlan vorhanden ist)

Links zeigt dir das Thermometer mit einem Blinken, wenn die Solltemperatur erreicht ist.
Die mittige Anzeige (von oben)
* IST: Ist-Temperatur
* Soll: Soll-Temperatur
* Brew: Bei einem Bezug wird softwareseitig oder hardwareseitig angzeigt, welche Zeit beim Bezug verstrichen ist
* P | I | D : Anzeige der aktuellen PID Werte, die aktuell gültig sind. Kann sich je nach Phase ( Kaltstart, Brühvorgang oder Normalbetrieb) ändern


## Minimal Design - DISPLAYTEMPLATE 2

 

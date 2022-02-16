---
layout: default
title: Einbau
parent: Hardware
grand_parent: DE - Handbuch
has_children: false
nav_order: 3
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

Grundsätzlich würde ich alle Kabel erstmal mit einer Kabellänge von ca. 60 cm abschneiden. Nach dem Einbau auf Seite 1 und dem Verlegen sollten diese beim Anschließen an Seite 2 gekürzt werden.

Vorbereitung:
* Node MCU bespielen (ggf. sicherstellen dass WLAN funktioniert)
* PCB zusammenlöten (Link zur Anleitung folgt)
* ggf. Blynk einrichten und verbinden
* ggf. Displayhalter drucken / bestellen

Zeitaufwand:
* PID Only ca. 3 h
* Vollaubau weitere 2-3 h

## Zerlegen

Als erstes muss die Maschine zerlegt werden. Hier findet ihr einen [Link zur Demontage](https://clevercoffee.de/rancilio-silvia-demontage/).

## PID only

### Thermostat gegen Temperatursensor tauschen

Kabel (0,14mm2) am Temperatursensor anlöten und mit Schrumpfschlauch versehen. **!!!Unbedingt Pinbelegung beachten!!!** Es empfiehlt sich folgende Belegung zu verwenden:

> Rot = +  
> Schwarz = -  
> Grüne = Signal

Freies Kabelende beschriften

Stecker mit rotem Kabel und Stecker mit grauem Kabel abziehen.

Schrauben 1 + 2 lösen.
Schraube 3 ein wenig lockern.
Das alte Thermostat beiseite legen und aufheben; bereich von der Wärmeleitpaste reinigen.

Bügel mit Schraube, Beilagscheiben und Muttern vorbereiten. Bügel wieder einbauen dabei Schraube 3 und 2 festziehen, 1 noch etwas locker lassen.

Die neue Schraube mit Hilfe der zwei Muttern so einstellen, dass die Schraube auf dem Temperatursensor aufliegt. Muttern festziehen.
Temperatursensor auf der Unterseite mit etwas Wärmeleitpaste versehen, unter der neuen Schraube platzieren und Schraube 1 anziehen. Der Bügel sollte sich dabei leicht verformen. So wird sichergestellt, dass der Sensor fest sitzt, aber nicht zu sehr gequetscht wird.  


### Stromversorgung

1,5mm2 Kabel blau mit Flachsteckhülse mit Abzweig versehen und in den abgezogenen Stecker mit Rotem Kabel stecken.
Ein weiteres 1,5mm2 Kabel blau mit Flachstecker versehen und ebenfalls einstecken. Alles mit einem Schrumpfschlauch versehen.
Kabel eins geht zum SSR der Heizung, Kabel zwei zum Netzteil. Welches Kabel dabei wofür verwendet wird ist egal.

1,5mm2 Kabel schwarz mit Flachsteckhülse mit Abzweig versehen. Den unteren Stecke am Schutzschalter abziehen, auf den Abzweig stecken und beides direkt wieder anstecken.

Kabel sinnvoll verlegen und einen Platz für das (USB)Netzteil definieren. Kabel vor dem anschließen entsprechend kürzen. (Ich habe das aus dem Gehäuse ausgebaute USB Netzteil rechts an der Rückwand mit doppelseitigem Klebeband angebracht)

Am USB Netzteil ein blaues Kabel und ein schwarzen Kabel anschließen / anlöten. Wird das Schaltnetzteil verwendet, das schwarze Kabel an N anschließen und das blaue Kabel an L anschließen. Es empfiehlt sich hierfür die Ringösen zu verwenden. Zusätzlich muss hier noch ein Schutzleiter verlegt werden. Dieser lässt sich an der Erdung des Kessels oder des 3-Wege Ventils "klauen". Vor dem Einbau die Ausgangsspannung am Poti auf ca. 5.2V einstellen.

Am Ausgang ein Rotes und ein Schwarzes Kabel anbringen. Ich habe dafür 0,5mm2 Kabel verwendet, die 0,14mm2 sollten aber auch reichen. Die beiden Kabel richtung 3-Wege Ventil legen und beschriften.

### SSR Relais Heizung

Montagepunkt für das SSR festlegen. (Ich habe es über der "CPU" neben dem Wasserschlauch mit doppelseitigem Klebeband angebracht)

An Kabel 2 (blau) des schrittes oben, eine Ringöße pressen (Kabel vor dem anschließen entsprechend kürzen) und an einen beliebigen Pol des SSR Ausgangs anschließen.
Ein weiteres Kabel 1,5mm2 mit einer Ringöße versehen und an Pol zwei des SSR Ausgangs anschließen. Kabel zum Stecker mit dem grauen Kabel verlegen welches ursprünglich am Thermostat war und entsprechend kürzen. Einen Flachstecker aufpressen, anschleißen und mit eiem Schrumpfschlauch versehen.

Zwei Kabel (rot und schwarz) an der Eingangsseite des SSR anschließen. Ich habe dafür 0,5mm2 Kabel verwendet und ebenfals Ringößen aufgepresst. Es können aber auch die 0,14mm2 Kabel mit Aderendhülsen o.ä. verwendet werden.
Freie Kabelenden beschriften und richtung 3 Wege Ventil legen.

### Einbau NodeMCU

folgt

## Vollausbau

**Wichtig!: Beim anschließen des Brühschalter bitte unbedingt den Hinweis im Schaltplan zur Trennung von 230V und 3.3/5V am Schalter beachten.**

folgt

## Spannende Addons die gleich mit erledigt werden können

* Senkschraube am Sieb
* Reinigung der Wasserschläuche (sofern die Maschine nicht neu ist)
* LED Umbau der Schalter

## Ausblick
Projekte die unterstützt werden können:
* digitales Manometer
* integrierte Waage
* Silvia E Zeit für automatisches Ausschalten verändern
* Automatische Funktion zum wechsel von Dampf auf Brühen

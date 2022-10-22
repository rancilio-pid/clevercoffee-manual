---
layout: default
title: PID-Werte ab Vers. 3.0.0
parent: Konfiguration & Anpassung
grand_parent: DE - Handbuch
has_children: false
nav_order: 1
---

# PID-Werte
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

Ab Release 3.0.1 wurde die PID nochmals deutlich vereinfacht und verbessert. Die frühere Brüherkennung (wer sie noch kennen sollte) ist faktisch nur noch in seltenen Fälle notwendig.
Die PID muss später folgende 3 Betriebszustände korrekt regeln, hierfür sind unterschiedliche Parameter für wichtig.

![PID-Einführung](../../img/Bildschirmfoto-2020-11-04-um-20.51.31-1536x733.png) 

Bereiche | Erklärung
:--|:--
1 | Kaltstart
2 | Regulärer Betrieb
3 | Brüherkennung (BD)

Die zugehörigen Werte lassen sich am NodeMCU direkt einstellen unter "Parameters":

![PID-Parametersmenu](../../img/PIDparametersmenu.png) 

Parameter | Erklärung
:--|:--
Enable PID Controller | muss beim erstmaligen Betrieb aktiviert werden, Schaltet die PID an/aus
Enable PonM | für den alten Kaltstart relevant, Standardmäßig "aus"
PID Kp | P-Anteil vom PID
PID Tn (=Kp/Ki)| I-Anteil vom PID
PID Tv (=Kd/Kp) | D-Anteil vom PID
PID Integrator Max | Begrenzt den I Anteil, wichtig für den Kaltstart.
Steam Kp | P-Anteil für den Dampfmodus
Set point (°C) | Soll-Temperatur von der PID
Offset (°C) | Offset zur Temperatur, Standard: 0
Enable Brew PID | Eigene PID-Werte für Brüherkennung, wird nicht mehr benötigt regulär bei der Silvia, Gaggia
PID BD Time (s)| Bei "Only-PID" Bezugszeit im Display
PID BD Sensitivity | Empfindlichkeit vom PID BD (0 = aus, kleinere Werte: hohe Empfindlichkeit, höhere Werte: geringe Empfindlichkeit der Erkennung

## Standardwerte für diverse Maschinentypen

### Rancilio Siliva
Parameter | Rancilio Siliva Standardwerte 1
:--|:--
PID Kp | 50
PID Tn (=Kp/Ki)| 200
PID Tv (=Kd/Kp) | 20
PID Integrator Max | 75
Steam Kp | 150
PID BD Sensitivity | 60

## Hinweise zur Optimierung
Bei einer Optimierung sollte zunächst der normale Betriebszustand angepasst werden,
hierbei sind vor allem PID Kp und PID Tn relevant für die Einstellungen.
Beim Kaltstart muss vor allem PID Tv, PID Integrator Max angepasst werden. 
Beim Bezug spielen vor allem PID Tn und PID Tv eine Rolle.

### Brühvorgang
Bei "Only-PID" ist die "PID BD Time (s)" und "PID BD Sensitivity" nur noch notwendig, um die Zeitanzeige im Display korrekt anzuzeigen. Diese Werte haben keinen Einfluss mehr auf den PID, solange "Enable Brew PID" deaktiviert ist. Mit Aktivierung von "Enable Brew PID", können nochmals eigene PID-Werte für den Brühvorgang gesetzt werden. Diese sind für die Dauer von "PID BD Time (s)" aktiv.

![PID-Parametersmenu BD](../../img/PIDparametersBDmenu.png) 

Parameter | Erklärung
:--|:--
Enable PID Controller | muss beim erstmaligen Betrieb aktiviert werden, Schaltet die PID an/aus
Enable PonM | für den alten Kaltstart relevant, Standardmäßig "aus"
BD Kp | P-Anteil vom PID bei Bezug
BD Tn (=Kp/Ki)| I-Anteil bei Bezug
BD Tv (=Kd/Kp) | D-Anteil bei Bezug

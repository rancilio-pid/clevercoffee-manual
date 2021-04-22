---
layout: default
title: Schaltpläne
parent: Hardware
grand_parent: DE - Handbuch
has_children: false
nav_order: 2
---

# Schaltpläne
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Warnhinweis

> {{ site.warnhinweis }}

## Einleitung

Wenn der Test erfolgreich war, kannst du beginnen deinen Einbau zu planen. Je nach Ausbaustufe musst du nur das Netzteil und Controller mit Strom versorgen, den Temperatursensor einbauen am Kessel. Wir zeigen dir hier am Beispiel der Rancilio Siliva wie der Umbau gelingt. Weiter Maschinen, wie z.B. die Gaggia wurde auch schon erfolgreich umgebaut.

## Originaler Schaltplan

Der erste Schaltplan zeigt den original Zustand der Silvia vor dem Umbau.

![Org Schaltplan](../../img/Rancilio-Cable-Original-1.jpg)

## "Only PID"

Der zweite Schaltplan zeigt die PID Anpassung.
Diese Version ist nur für die Temperatursteuerung verantwortlich.
Die Pumpe und das 3-Wege-Ventil werden nicht durch den Controller gesteuert.

![PID Schaltplan](../../img/Screenshot-at-Dez.-11-11-16-33-1536x1168.png)

## "Vollausbau"

Der dritte Schaltplan ist der aktuelle „Vollausbau“.
Enthalten ist die PID für die Kesseltemperatursteuerung
Zusätzlich kann auch die Brühzeit oder eine „Preinfussion“ gesteuert werden. (Vorlauf-Brühzeit, Pause, Brühzeit).
Dabei werden Pumpe und das 3-Wege-Ventil vom Controller gesteuert.

**Wichtig!: Der aktuelle Schaltplan beinhaltet ein potentiellen Fehler in der Verkabelung, siehe [[Link]](https://chat.rancilio-pid.de/ranciliopid/pl/7j88qqmfzbfc8f7f5d1jcxsceh)**

**WICHTIGER HINWEIS: Dieser Umbau darf nur am Brüh-Schalter vorgenommen werden, wenn ein Schalter ohne Lampe genommen oder die Lampe ausgebaut oder eine neue Verkabelung gewählt wird, dass mit eingebauter Lampe KEINE 3,3 Volt und 230 Volt am Schalter anliegen! Sonst liegt KEINE galavanische Trennung zwischen 3,3 Volt und 230 Volt mehr vor! Das kann unter ungünstigen Umständen gefährlich für dich oder den Microcontroller sein!**

![Vollausbau Schaltplan](../../img/Screenshot-at-Dez.-11-11-12-33-1536x1147.png)

## Schematische Darstellung der Ausgänge der Platine ESPresso Rev 1

![Platine Schaltplan](../../img/Rancilio-Cable-Page-4.jpg)

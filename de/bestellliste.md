---
title: Bestellliste
parent: DE - Handbuch
has_children: false
nav_order: 2
---

# Bestellliste
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Warnhinweis

> {{ site.warnhinweis }}

## Die Liste

Unabhängig von dem Vollausbau benötigst du folgende Dinge:

ID | Beschreibung | Link
-|-|-
2x TSIC 306 TO92 | Temperatur Sensor | [Link](https://www.reichelt.de/tsic-digitale-halbleiter-temperatursensoren-tsic-306-to92-p82327.html?r=1)
SNT RS 15 5 | Schaltnetzteil | [Link](https://www.reichelt.de/schaltnetzteil-geschlossen-15-w-5-v-3-a-snt-rs-15-5-p137080.html?&trstct=pos_0)
RA 2425-D06 | SSR Relais – Heizung | [Link](https://www.reichelt.de/solid-state-relais-ust-2-32vdc-ulast-24-280v-ra-2425-d06-p22691.html?&trstct=pos_0)
NodeMCU esp8266 V2 | Mikrocontroller | [Link](https://www.amazon.de/AZDelivery-NodeMCU-ESP8266-ESP-12E-Development/dp/B06Y1LZLLY/ref=sr_1_1_sspa?ie=UTF8&qid=1538918768&sr=8-1-spons&keywords=nodemcu+esp8266&psc=1)
128 x 64 Pixel OLED | Display (optional) | [Link](https://www.amazon.de/AZDelivery-Display-Arduino-Raspberry-gratis/dp/B01L9GC470/ref=sr_1_3?ie=UTF8&qid=1544291613&sr=8-3&keywords=oled+128x64)
PCB | unsere erstellte Platine | [Bitte über unseren Chat anfragen!](https://chat.rancilio-pid.de/) **Bitte direkt an @toppo78 wenden**

Wir geben hier den Tipp gleich mindestens 2 TSIC Sensoren zu kaufen. Wir haben es nun häufiger erleben müssen, dass die Sensoren falsch verdrahtet werden. Daher denkt einfach gleich an eine Reserve bei der Bestellung bei Reichelt. Bitte einen falsch verpolten Sensor nicht mehr verwenden, dieser geht kurzfristig kaputt oder zeigt unrealistische Werte an (für Details siehe [Temperatursensor anschließen](./hardware/hardware.md#temperatursensor-anschließen))

> Hinweis: Man kann beim NodeMCU nicht die V1 oder V3 nehmen.

Zusätzlich helfen folgende Dinge beim Umbau, die teilweise auch schon zu Hause in der Bastelkiste vorhanden sind:

Bezeichnung|	Artikelnr. bei Reichelt|	Menge
-|-|-
Schaltlitze H07V-K, 1,5 mm, 10 m, blau|H07VK 1,5-10BL|1
Flachsteckhülsen mit Schrumpfschlauch – 1,5 … 2,5 mm², blau|WE F602638HS|10
Flachsteckhülsen mit Abzweig – 1,5 … 2,5 mm², transp., vollisoli|WE F606638.1N|10
Kupferlitze isoliert, 10M, 1×0,14mm², braun|LITZE BR|1
Kupferlitze isoliert, 10M, 1×0,14mm², blau|LITZE BL|1
Kupferlitze isoliert, 10M, 1×0,14mm², orange|LITZE OR|1
Crimpzange, 240 mm, isolierte Kabelschuhe + Kabelverbinder |KN 97 22 240|1
Schaltlitze H07V-K, 1,5 mm, 10 m, schwarz|H07VK 1,5-10SW|1
Flachstecker mit Schrumpfschlauch – 1,5 … 2,5 mm², blau|WE F616638HS|10
|
Relais nur für **Vollausbau** (siehe Hinweise unten)| DEBO RELAY 4WAY | 1

Ferner wird benötigt:

* Wärmeleitkleber (nichtleitend): [Link](https://www.amazon.de/Silverbead-W%C3%A4rmeleitkleber-10-Gramm-SG100X/dp/B019MNSABG/ref=sr_1_1?ie=UTF8&qid=1538938085&sr=8-1&keywords=w%C3%A4rmeleitkleber) (Silverbead Wärmeleitkleber) für den Sensor
* Schrumpfschlauch für die Kabel

## Vollausbau

Wir haben im Projekt viele diverse Relais für die Pumpe und das Ventil testen „dürfen“ – diese sind leider nicht so stabil wie die der SSR für die Heizung. Folgende Erkenntnisse haben wir dabei gesammelt:

###  Schlechteste Lösung: Spulen Relais
Ja, Spulen Relais kann man verwenden, dabei können durch die Bauweise der Relais Probleme entstehen, die sich nicht immer lösen oder reproduzieren lassen: [Link](https://www.amazon.de/AZDelivery-2-Relais-Optokoppler-Low-Level-Trigger-Arduino/dp/B078Q326KT/ref=sr_1_7_sspa?__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&dchild=1&keywords=azdelivery%2Bspulen%2Brelais&qid=1603614378&sr=8-7-spons&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUExNDdFUE9JRkxXSkNEJmVuY3J5cHRlZElkPUEwNDU5MDU1OVlVSENDWEZNQTQzJmVuY3J5cHRlZEFkSWQ9QTAwNDA1MTEzUlBCUzUwVFdZSTI3JndpZGdldE5hbWU9c3BfbXRmJmFjdGlvbj1jbGlja1JlZGlyZWN0JmRvTm90TG9nQ2xpY2s9dHJ1ZQ&th=1). Lösungen mit einer galvanischen Trennung können manchmal helfen [Link](https://www.kollino.de/arduino/4-8-kanal-relais-anleitung/). Daher ist es die schlechteste Lösung bei den Relais.

### SSR Board von Amazon
Manche gehen ins Spielcasino, wir bestellen bei Amazon – Manchmal hat man Pech und wo „High Trigger“ drauf steht, ist manchmal „Low Trigger“ drin. Einen Low Trigger erkennt ihr an einem „2TY“ auf dem einen Baustein des SSR Boards. „J3Y“ Steht hierbei für den besseren HIGH Trigger. SSR Boards sind besser als die Spulen Relais, aber Low Trigger können auch Probleme verursachen.

### Beste Lösung: High Trigger SSR
User im Chat haben zuverlässige Bezugsquellen für High Trigger gefunden: [Link](https://www.roboter-bausatz.de/1450/2-kanal-solid-state-relais-modul-5v/230vac-high-level-trigger). Daher ist dies momentan unsere Favorit.

Alternativ kann bei Reichelt auch folgender High Trigger mitbestellt werden: [Link](https://www.reichelt.de/entwicklerboards-4-wege-solid-relais-5v-240v-2a-debo-relay-4way-p280064.html?&trstct=pos_0&nbc=1).


### Alternative: 2x Heizungs SSR
Wenn der Platz vorhanden ist, könnte man auch 2x den Heizung SSR nutzen.

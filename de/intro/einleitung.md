---
title: Einleitung PID System
parent: Einführung
grand_parent: DE - Handbuch
has_children: false
nav_order: 2
---

# Einleitung PID System
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Was bringt mir eine PID-Steuerung?

Eine PID-Steuerung ermöglicht es deiner Espressomaschine die Temperatur des Brühwassers sehr viel exakter und konstanter zu regeln als das mit den werksseitig verbauten Bimetall-Thermostaten möglich ist.

Die gängigen Thermostate haben eine Schwankung der durch sie geregelten Temperatur von bis zu 10°, auch Hysterese genannt. Grob gesagt bedeutet das: eure Maschine heizt hoch, bis der Thermostat seine Schalttemperatur erreicht hat und den Strom zur Heizung unterbricht. Gleichzeitig leuchtet die Lampe eurer Maschine auf und zeigt euch Brühbereitschaft an.

Jetzt verliert der Kessel eurer Maschine je nach Ausführung mehr oder weniger schnell Wärmeenergie durch Abstrahlung an die Umgebung. Dies geschieht so lange, bis der Anschaltpunkt des Thermostaten erreicht ist und er den Stromkreis zur Heizung wieder aktiviert. Die Brühlampe eurer Maschine erlischt und die Maschine heizt wieder hoch bis zum Erreichen des Abschaltpunktes.

Zwischen diesen beiden Temperaturpunkten leuchtet die ganze Zeit die Brühbereitschaftslampe eurer Maschine. Die wirkliche Brühtemperatur des Wassers kann sich aber entweder ganz unten nah beim Anschaltpunkt des Thermostaten befinden, oder ganz oben kurz vor dem Abschaltpunkt, oder irgendwo im Bereich dazwischen.

Beim Espresso ziehen ist die Temperatur des Brühwassers einer DER entscheidenden Faktoren für den Geschmack des Kaffees. Schon eine Differenz von 1° kann den Unterschied zwischen sauer (zu kalt), verbrannt (zu heiß) oder lecker (genau richtig) bedeuten. Das hängt jeweils stark von der verwendeten Bohne ab.

Eine Maßnahme ist das sogenannte Temperatursurfen, eine relativ aufwendige manuelle Methode der Temperaturkontrolle die es erfordert, dass der Bediener tatsächlich an der Maschine steht.

Viele Nutzer sind davon irgendwann genervt, wir waren es genauso.

Die Lösung für kleinere Einkreiser-Maschinen ist, den Thermostaten der Maschine aus dem Spiel zu nehmen und einen PID-Regler zu verbauen. Dieser regelt die Brühtemperatur mit einer Schwankung von deutlich unter 1°, unser System kann auf bis zu 0,1° genau regeln. Man muss nicht mehr an der Maschine bleiben um den richtigen Zeitpunkt zum Bezug zu treffen, der richtige Zeitpunkt ist ab jetzt einfach immer sobald die Maschine einmal durchgeheizt ist!


## Was kann unser System?

Folgende Eckdaten zeichnen unseren DIY PID aus:

* Regelung der Brühtemperatur mit einer Genauigkeit von bis zu +/- 0,1°
* Steuerung der Brühzeit inkl. Pre-Infusion in der Ausbaustufe „Vollausbau“ möglich
* Bedienung über eine Smartphone-App (iOS & Android)
* Datenmonitoring über Grafana (webbasiert) und MQTT (IoT) möglich
* Updates der PID-Software sind drahtlos über WLAN möglich
* Unsere PID-Software ist OpenSource: für euch kostenfrei und auf persönliche Anforderungen anpassbar
* Geringer Platzbedarf, passt problemlos in die meisten kleineren Espressomaschinen
* Die serienmäßige Verkabelung der Maschine bleibt erhalten und wird nur erweitert. Die Maschine kann nach dem Umbau problemlos wieder zurückgerüstet werden.
* Aktive User-Community im Projektchat mit schnellem Support
* Anregungen zur Weiterentwicklung der Software werden von uns gerne aufgenommen. User-Input ist immer willkommen und bringt den PID weiter!

## Universell – Umgebaute Maschinentypen

Entwickelt wurde unser System ursprünglich an einer Rancilio Silvia, es ist aber universell einsatzbar. Bislang haben unsere User die folgenden Maschinen erfolgreich umgebaut:

  Rancilio Silvia V1 – V5
  Gaggia Classic (9303) / Classic Pro (9480)
  Lelit PL41 / PL42
  La Pavoni EPL / Saeco Aroma / Gaggia New Classic (9403)
  E61 Einkreiser (Bazzar A1 Livello, Fiorenzato Colombina)
  E61 Zweikreiser (Profitec Pro500)

## Aufbau / Unterschiede PID Only vs. Vollausbau

Grundsätzlich besteht unser PID-Regler aus den folgenden Komponenten:

ID | Erklärung
-|-
1 | Mikrocontroller NodeMCU V2                 
2 | Temperatursensor TSIC 306                 
3 | Solid State Relais (SSR)                       
4 | Netzteil zur Stromversorgung               
5 | Display (empfohlen, aber optional)      

![Trockenaufbau](../../img/trockenaufbau.png)

Es gibt zwei verschiedene Ausbaustufen unseres Systems: PID Only und den erweiterten Vollausbau.

## Grundversion (PID Only)

Die Grundversion ist ein klassischer PID-Regler: der Temperatursensor nimmt die aktuelle Temperatur des Kessels auf (Input) und gibt den Wert an die PID-Software auf den Mikrocontroller ( auch NodeMCU genannt) weiter. Diese gibt dann das Regler-Signal (Output) an das SSR aus, welches die Heizung eurer Maschine aktiviert bzw. deaktiviert.

Damit habt ihr eine exakte Regelung der Brühtemperatur auf euren Wunschwert durch die PID-Software, die restliche Bedienung eurer Maschine bleibt unangetastet. MQTT, Displayausgabe und Handy Steuerung geht auch bei Only PID

## Vollausbau

Beim Vollausbau gehen wir einen Schritt weiter und überlassen die Ansteuerung der Pumpe und des Magnetventils ebenfalls der Software. Dadurch könnt ihr in der App 3 Zeitintervalle vorgeben:

* Pre-Infusion: die Pumpe baut Druck auf + das Magnetventil gibt das Brühwasser auf den Siebträger

* Pause: die Pumpe pausiert, der aufgebaute Druck bleibt aber durch das aktivierte MV im Siebträger bestehen. So wird der Kaffeepuck gleichmäßig durchfeuchtet, z. B. kann so Channeling reduziert werden.

* Brühzeit: jetzt startet der „normale“ Bezug mit der von dir festgelegten Bezugszeit, z. B. 25 Sekunden. Je nach Bohnensorte und persönlichem Geschmack kann eine kürzere oder längere Bezugszeit den Geschmack des Espressos noch mehr nach vorne bringen.

Beim Vollausbau ändert sich die Bedienung eurer Maschine auch etwas: der Brühschalter, mit dem ihr bislang den Bezug gestartet und auch wieder gestoppt habt, dient nun nur noch als Taster, der den automatisierten Bezug startet. Gestoppt wird der Bezug durch die Software, auch wenn der Schalter noch auf ON steht.

Unsere Empfehlung, basierend auf unseren eigenen Erfahrungen und denen der bislang mehr als 250 User des PIDs, lautet ganz klar, zuerst die Grundversion PID-Only umzusetzen. Damit ist die größte geschmackliche Verbesserung im Vergleich zum vorherigen Serienzustand eurer Maschine zu erwarten. Der Vollausbau ist darauf aufbauend eine Erweiterung der Möglichkeiten, aber gleichzeitig auch ein komplexerer Umbau.  

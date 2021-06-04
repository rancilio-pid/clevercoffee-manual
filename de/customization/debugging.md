---
layout: default
title: Debugging
parent: Konfiguration & Anpassung
grand_parent: DE - Handbuch
has_children: false
nav_order: 8
---

# Debugging
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

Während des Betriebs der PID lassen sich Debug-Informationen zum Zustand der Maschine ausgeben. Neben der Standard-Ausgabe auf den Seriellen Bus mittels Serial.print() und Serial.println() bietet die PID weitere Möglichkeiten. 
Dazu dient die Klasse DebugStreamManager, die Ausgaben entweder über die Serielle Schnittstelle oder über Wifi ermöglicht. Sie nutzt die von Joao Lopez entwickelten Bibliotheken [SerialDebug](https://github.com/JoaoLopesF/SerialDebug) und [RemoteDebug](https://github.com/JoaoLopesF/RemoteDebug). Beide Bibliotheken sind im Zusammenspiel mit der PID mit ESP8266 Board Manager Versionen bis 2.7.4 getestet.  


## 1. Debug Methoden und Zugriff

In der userConfig.h lässt sich der Debug Modus im Bereich WiFi einstellen. Dabei kann zwischen drei Modi unterschieden werden
```
#define DEBUGMETHOD 1              // 0 = none, 1 = SerialDebug, 2 = RemoteDebug
```
Um SerialDebug nutzen zu können, muss der ESP per USB verbunden sein, damit der Serial Monitor (in Arduino IDE: Tools - Serial Monitor) geöffnet werden kann. 

Um RemoteDebug zu nutzen, muss das WiFi konfiguriert sein. Für den Zugriff auf die Debug Informationen benötigt man einen telnet Client. Mit diesem verbindet man sich direkt über die  IP des ESP, z.B. 
```
telnet 192.168.188.54
```
In manchen Fällen kann es hilfreich sein, die Ausgabe parallel in eine Datei mitzuschreiben. Das kann mit dem Befehl 
```
telnet 192.168.188.54 | tee -a -i dateiname.txt
```
erfolgen.

Alternativ zum telnet Client gibt es auch eine RemoteDebugApp. Link und Beschreibung findet man auf der [git-Seite von RemoteDebug](https://github.com/JoaoLopesF/RemoteDebug). Bislang ist die App erfolgreich in Safari getestet worden. Mit anderen Browsern liegen noch keine Erfahrungen vor. Rückmeldungen sind gerne willkommen.

## 2. Logbuch 

Die beiden Bibliotheken SerialDebug und RemoteDebug bieten die Möglichkeit, Funktionen zu definieren, die zur Laufzeit aus dem Debug Fenster heraus aufgerufen werden können. Über diesen Mechanismus ist für den DebugStreamManager ein Logbuch implementiert. 

Da der Speicherplatz des ESP begrenzt ist, können nicht beliebig viele Debug Informationen gespeichert werden. In der userConfig.h ist die maximale Anzahl von Logbuchzeilen anzugeben
```
#define MAXLOGLINES 100            // Number of log lines (>=0) stored in logbook, (-> command "loghist" in terminal window)
                                   // if set too large the ESP will run out of memory and reboot unexpectedly
```
Die Beschreibung des Logbuchs erfolgt rollierend, so dass nach erreichen der MAXLOGLINES bereits enthalten Zeilen überschrieben werden. 

Es ist darauf zu achten, dass genügend Speicherplatz während des Betriebs frei bleibt. Den freien Speicherplatz kann man sich im Debug Fenster mit "m" anzeigen lassen. 
Für den aktuellen Softwarestand 2.9.2 ist es auf dem ESP8266 möglich, bis zu ca. 200 Zeilen zu speichern. 

Sollte es im Betrieb zu Speicherproblemen kommen, äußert sich das durch zufälliges rebooten des ESP. Da das Logbuch ja sukzessiv beschrieben wird und die Größe kontinuierlich anwächst, ist damit nicht gleich zum Start zu rechnen sondern nach einiger Laufzeit. 

Das Logbuch lässt sich im Debug Fenster anzeigen. Bei SerialDebug muss dazu zunächst das Interface aktiviert werden, z.B. durch Eingabe eines "?"
```
* SerialDebug: Please press ? or another command and enter to activate debugs
```
Solange dies nicht geschehen ist, werden nur Debug Ausgaben der Kategorie E im Fenster ausgegeben (Einträge ins Logbuch erfolgen dennoch). Anschließen erfolgt die Ausgabe des Logbuchs mit dem Befehl
```
f loghist
```
Für RemoteDebug ist keine Aktivierung erforderlich, hier kann direkt der Befehl
```
loghist
```
verwendet werden.

## 3. Erzeugen eines Debug Stream

Im Folgenden soll kurz darauf eingegangen werden, wie die Klasse DebugStreamManager rancilio-pid.ino verwendet wird. 

Zunächst wird die Header-Datei der Klasse eingebunden und ein Objekt debugStream erzeugt
```
#include "DebugStreamManager.h"
DebugStreamManager debugStream;
```
Dabei werden die Einstellungen aus der userConfig.h für DEBUGMODE und MAXLOGLINES ausgelesen. 

In der setup() Schleife ist muss für den debugStrem ebenfalls eine setup() Funktion aufgerufen werden
```
void setup() {
  ...
  debugStream.setup();
  ...
}
```
In der loop() Schleife ist die handle() Funktion aufzurufen
```
void loop() {
  ...
  debugStream.handle();
  ...
```


## 4. Debug Ausgabe und Debug Level

Debug Ausgaben werden in fünf Kategorien unterteilt
- **E**rror: für Fehlermeldungen
- **W**arning: für Warnungen
- **I**nfo: Ausgaben, die Ereignisse protokollieren, z.B. wlan-Aufbau, Signalstärke, Blynk-Verbindung, Änderungen des machinestate, Änderungen der PID-Werte, Schalten von Tastern, ...
- **D**ebug: für temporäre Ausgaben bei aktuellen Entwicklungen, kommen später wieder raus
- **V**erbose: kontinuierliche Ausgabe von Sensordaten, ...

Die Level sind hierarchisch, d.h. **E** ist Teilmenge von **W** ist Teilmenge von **I** ist Teilmenge von **D** ist Teilmenge von **V**.

Um eine Debug Ausgabe zu erzeugen, die einer dieser Kategorien zugeordnet ist, stehen die Befehle
```
debugStream.writeE(...);
debugStream.writeW(...);
debugStream.writeI(...);
debugStream.writeD(...);
debugStream.writeV(...);
```
zur Verfügung. Allen Funktionen ist mindestens ein Argument mitzugeben, die Syntax ist wie beim printf Befehl, wobei jeder Befehl automatisch eine Zeilenendmarkierung beinhaltet. 

Beispiele:
```
debugStream.writeI("Bezugsdauer: %4.1f s",lastbezugszeit/1000);
debugStream.writeD("1 (T,hra) --> %6.2f %8.2f",Input,heatrateaverage);
debugStream.writeE("********** ERROR: ... **********");
```

Im Debug Fenster kann mit den Befehlen 'e', 'w', 'i', 'd' und 'v' die Ausgabe auf einzelne Debug Level eingeschränkt werden. Voreingestellt ist Level **D**.

Die Ausgaben der Level **E**, **W**, **I** und **D** werden automatisch ins Logbuch geschrieben.

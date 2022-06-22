---
layout: default
title: Visual Studio Code mit PlatformIO einrichten
parent: Software
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

# Einführung

[Visual Studio Code](https://code.visualstudio.com/) ist ein plattformübergreifend verfügbarer Code-Editor, der sich über zahlreiche Extensions erweitern lässt. Eines der für die Entwicklung eingebetteter Systeme hilfreichsten Extensions ist [PlatformIO](https://platformio.org/). PlatformIO ermöglicht das einfache Kompilieren und Debuggen von Code für zahlreiche Mikrocontroller und ist in seiner Handhabung und Installation deutlich weniger komplex ArduinoIDE. Gleichzeitig hat PlatformIO in Verbindung mit Visual Studio Code allerdings einen deutlich größeren Funktionsumfang, wie zum Beispiel die automatische Installation aller Abhängigkeiten (Compiler, Bibliotheken, etc.) und die gleichzeitige Unterstützung mehrerer Mikrocontroller.

## Installationsvideo

In diesem kurzen Video erklären wir die Installation von Visual Studio Code und PlatformIO und zeigen, wie Rancilio-PID eingerichtet und auf dem NodeMCU installiert wird. Die Installation erfolgt hier beispielhaft in Lubuntu, funktioniert aber analog natürlich auf jedem von Visual Studio Code unterstützten Betriebssystem.

[![Installationsvideo](http://i3.ytimg.com/vi/OpYECpZG_FE/hqdefault.jpg)](https://www.youtube.com/watch?v=OpYECpZG_FE)

## Download und Installation

[Visual Studio Code](https://code.visualstudio.com) ist für Windows, macOS und Linux verfügbar.

### Windows über [chocolatey](https://chocolatey.org/)

```choco install vscode```

### macOS über [homebrew](https://brew.sh)

```brew install vscode```

### Linux über [Snap](https://snapcraft.io/)

```snap install vscode```

PlatformIO kann über das Extensions-Menü installiert werden. Eine allgemeine Anleitung, wie Extensions installiert werden, ist [hier](https://code.visualstudio.com/docs/editor/extension-gallery) zu finden. 

## Der Programmcode

Download des aktuellen Programmcode findest du im aktuellen Release.

[Link zum Github Repository](https://github.com/rancilio-pid/ranciliopid/releases)

![Screenshot der Github Homepage](../../img/2.png)
## Einrichtung von Visual Studio Code und PlatformIO

Im Gegensatz zur ArduinoIDE ist es bei der Arbeit mit Visual Studio Code und PlatformIO nicht notwendig, manuell Bibliotheken zu kopieren oder den Mikrocontroller (das Board) zu installieren, für das der Code kompiliert werden soll. Die notwendigen Informationen sind bereits in der Datei `platformio.ini` voreingestellt, welche Teil des Releases `rancilio-pid` ist.

Nach dem Herunterladen des Programmcodes muss man diesen in PlatformIO in Visual Studio Code über "Open Project" unter "PIO Home" -> "Open" auswählen. Beim ersten Öffnen installiert PlatformIO an dieser Stelle alle notwendigen Abhängigkeiten und Tools, wie die benötigten Compiler und Bibliotheken für die Boards. Das Projekt öffnet sich nun in der Projektansicht von PlatformIO. 

Bevor man den Programmcode nun kompilieren und auf das Board laden kann, muss erst noch die Datei `userConfig.h` erstellt werden, in der alle für Dich spezifischen Einstellungen, wie zum Beispiel die WLAN-Zugangsdaten, eingetragen werden. Für Linux-Nutzer haben wir in `rancilio-pid/scripts/create_user_config.sh` ein Skript abgelegt, das Dich nach den von Dir gewünschten Grundeinstellungen fragt und die `userConfig.h` erstellt. Alle weiteren Einstellungsmöglichkeiten auf Basis dieser Datei sind in [Software Teil II](../software-part-II.md#userconfigh) erklärt. 

## Kompilieren und Hochladen der Software

Sind alle Einstellungen getroffen, wählt man in der Projektansicht von PlatformIO unter  `nodemcuv2_usb` den Befehl `Build` und kompiliert so den Programmcode. Wenn dies ohne Fehler abschließt, was man anhand der `SUCCESS`-Nachricht im Terminal unten rechts ablesen kann, kann man den Code auf das per USB angeschlossene Board laden. Dazu wählt man den Befehl `Upload`, welcher auch mit `SUCCESS` erfolgreich durchlaufen sollte. 

Wenn alle diese Schritte erfolgreich durchgelaufen sind, sollte sich euer Board schon in eurem WLAN anmelden und kann, wenn gewünscht, ab jetzt auch per Over-the-Air-Update mit neuer Software versorgt werden, also über das WLAN und ohne USB-Verbindung mit dem Computer. Dafür muss lediglich die Datei `platformio.ini` angepasst und dort der zu eurem Board und euren Einstellungen passende Hostname unter `upload_port` eingetragen werden[^1]. Ist dies geschehen, wählt ihr im PlatformIO-Menü unter `nodemcuv2_ota` den Befehl `Upload`, und die Software des Boards wird über das WLAN aktualisiert. 
<!-- Dieser Prozess ist für die ArduinoIDE kurz [hier](../software-part-II.md#ota-1) erklärt.  -->

[^1]: Dieser Name kann auch mittels des Skripts `create_user_config.sh` gesetzt werden. 

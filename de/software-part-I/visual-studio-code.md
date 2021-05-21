---
layout: default
title: Visual Studio Code mit PlatformIO einrichten
parent: Software Teil I
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

In diesem kurzen Video erklären wir die Installation der Arduino IDE und zeigen wie unsere OpenSource Software Rancilio-PID auf dem NodeMCU installiert wird. Viel Spaß!

[![Installationsvideo](../../img/vscode.mp4)

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

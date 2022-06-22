---
layout: default
title: Software
parent: DE - Handbuch
has_children: true
nav_order: 3
---

# Software
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

In diesem Kapitel wird beschrieben wie der Code auf den Mikrocontroller (NodeMCU) geladen wird. Damit könnt ihr loslegen, sobald ihr den Mikrocontroller zur Hand habt (weitere Teile werden nicht hierfür nicht benötigt). Für einen Test sollte dann zumindest der Temperatursensor angeschlossen werden.

# userConfig.h
In dem rancilio-pid/rancilio-pid Ordner befindet sich eine für euch wichtige Datei: 
* userConfig_sample.h

Die userConfig_sample.h muss in userConfig.h umbenannt werden und mit euren Werten anpasste werden. 
Alle wichtigen Einstellungen werden für eure PID in dieser Datei vorgenommen, diese werden nun gleich genauer erläutert.
Bei einem Update auf eine neuere Version bitte unbedingt die neuste userConfig_sample.h nehmen und mit euren Werten anpassen.
Wenn Ihr das nicht tut, kann dies zu unspezifischen, nicht erwünschten Verhalten an der Maschine kommen: Display hängt, PID geht nicht und weitere
Probleme können auftreten. 
Die genaue Beschreibung findet ihr im nächsten Menüpunkt. 
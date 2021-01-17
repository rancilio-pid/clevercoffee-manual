---
title: Brüherkennung
parent: Konfiguration & Anpassung
grand_parent: DE - Handbuch
has_children: false
nav_order: 2
---

# Brüherkennung
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

Wie in dem vorherigen Kapitel erwähnt, soll der **brew heater detection limit** Wert auf „0“ gestellt werden, um diesen bei dem ersten Test zu deaktivieren. Wenn der normale PID gut läuft, ein für dich angenehmes Heizverhalten sich beim Starten zeigt und stabil am Soll-Wert läuft, dann kannst du die Brüherkennung dir genauer anschauen.

## Funktionsweise

Ohne zu tief in die technischen Details der Erkennung einzusteigen, soll dir dennoch kurz die grundlegende Funktionsweise erläutert werden. Der Mikrocontroller überwacht kontinuierlich die Temperatur. Dabei wird die zeitliche Veränderung der Heizrate/Kühlrate für fortlaufend Zeitfenster analysiert. Das Ergebnis ist dann die „heat average“. Wenn diese negativ wird, kühlt die Maschine ab, bei einem Hochheizen wird diese positiv.

![Brüherkennung](../../img/fullsizeoutput_1c57.jpeg)

Die Brüherkennung „horcht“ nun auf dieser „heat average“, in dem der negative Grenzwert definiert wird, ab dem die Maschine von einem Bezug ausgehen soll. Dieser wird bei „brew heater detection limit“ definiert. Hierbei ist zu beachten, dass hier der absolute Werte eingetragen wird: 70 entspricht -70. Die Übersetzung in den negativen Wert erfolgt im Quellcode!

Vereinfacht kann festgehalten werden, dass die „brew heater detection limit“ letztendlich die Empfindlichkeit der Erkennung wiedergibt: Je kleiner der Wert ist, je empfindlicher reagiert die Brüherkennung. Wenn die zu empfindlich (kleiner Wert, z.B. 5) ist, wird jedes normale Abkühlung als Brühvorgang erkannt, ist der Wert zu groß (z.B. 1000) wird erst zu spät oder gar nicht die Brüherkennung ausgelöst. Es kann dazu hilfreich sein den Verlauf der heat average über eine längere Zeit zu beobachten und somit einen geeigneten Werte zu finden.

Wenn die Erkennung ausgelöst werden, dann gelten für den definierten Zeitraum in „brew timer Software Seconds“ (im oberen Screenshot, 120 Sekunden) andere PID Werte. Somit kann der Regler nun aggressiver auf den Brühvorgang reagieren und schneller hochheizen. Wichtig ist hierbei, dass jede Unterschreitung des Grenzwertes zu einer Auslösung der Erkennung führt. Der Verlauf nach dem Auslösen wird nicht weiter ausgewertet, sondern die geänderten PID Werte gelten fix für die definierte Zeit.

## PID Werte

Für den kurzen Zeitraum muss der PID schnell wieder auf Temperatur kommen, ohne überzuschwingen. Hierzu muss vor allem der I-Anteil erhöht werden, damit sich der Regler nicht die erfolgte Abweichung vom Soll-Wert für die Zukunft „merkt“. Der D-Anteil kann auch erhöht werden, um den Regler beim Abfallen der Temperatur zu „beschleunigen“ und „abzubremsen“, wenn die Temperatur wieder Richtung Soll-Wert geht. Als Größenordnung können die Werte aus dem oberen Screenshot genommen werden.
In der nachfolgenden Tabelle sind bewährte PID für die Brüherkennung zu finden.

Maschine |	P |	I |	D | Timer |  Limit 
:-|-|-|-|-|-
Rancilio Silvia (nicht isoliert) | 50 | 5000 | 20 | 120 | 45 
Rancilio Silvia E (isoliert) | 70 | 0 | 20 | 240 | 65 
Gaggia | 75 | 0 | 15 | 180 | 90 

## Vergleich bei einem Bezug

Ausgangssituation sind folgende PID Parameter:

![PID Parameter](../../img/Screenshot-at-M%C3%A4rz-15-07-47-28.png)

Bei dem Vergleich von einem Bezug mit und ohne Brüherkennung ist zu sehen, dass die Solltemperatur zu einem ähnlichen Zeitpunkt wieder „durchschritten“ wird, aber ohne Erkennung die Temperatur nach oben ausschlägt (96 °C). Die Erkennung kann hier ein deutlich besseres Ergebnis liefern (ca. 93,5 °C). Auch fällt die Temperatur nicht so rapide nach unten ab bei dem Bezug, da die Heizung schneller reagieren kann bei der Erkennung.

In der Praxis zeigt sich bei mir zu hause, dass bei Gästen zügig und reproduzierbar Espresso hintereinander gezogen werden können, da meistens die 3 Minuten ausreichen den Kaffee zu verteilen und neue Bohnen zu mahlen.

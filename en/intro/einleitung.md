---
layout: default
title: Introduction PID System
parent: Introduction
grand_parent: EN - Manual
has_children: false
nav_order: 2
---

# Introduction PID System
{: .no_toc }

Contents

* TOC
{:toc}

## What is PID control good for?

A PID controller gives considerably better control of the water temperature in your espresso machine than what the standard bimetal thermostat can do.

Mechanical thermostats will keep the water in your machine in a range of about 10° Celsius. This means that the boiler in the machine will heat up to the thermostat's cut out point. The thermostat shuts off the heating and switches on the 'ready' light on the machine.

Now the boiler cools down to the thermostat's cut in point. The 'ready' light goes off and the heater reheats up to cut off again. 

Between these two points, the machine is always signalling 'ready', although the water can be close to the cut out temperature, or just barely above cut in. Or somewhere in between.

In a tasteful shot of Espresso, water temperature is one of the critical parameters. Being off by just a degree C or two can make the difference between a sour shot (too cold), a burnt one (too hot) or a well tasting shot. Not all coffee beans like the same temperature.

One way to a reproducible temperature is called temperature surfing. It entails flushing the machine and watching to ready lamp to understand when the heating cuts out in order to know better at what temperature the boiler is when pulling the shot. Many people get annoyed by this - so were we.

The solution for small home use single boiler machines is to replace the thermostat with a PID controller that is able to hit the requested temperature within less than 1 °C. Our setup is quite capable to reach an accuracy of up to 0.1 °C. No need to hit the right time to pull a shot anymore - the right time is whenever the machine has warmed up.


## What can it do?

Our DIY PID has the following features:

* control the water temperature to within +/- 0.1 °C
* control brewing time as well as pre infusion in the "full expansion" build
* easy control via app for Android & iOS
* data monitoring via Grafana (web based) and MQTT (IoT) possible
* OTA (over the air) software updates
* PID software is open source: always free and customizable to your own needs
* compact build, fits into most small espresso machines
* the machine's stock cabling of the machine is not modified. The machine can always be restored to its original configuration
* Active community with fast support, always welcoming feedback and feature suggestions
 

## List of modified machines

Our system was originally developed for use in the Rancilio Silvia but can be used in other machines as well. So far, users have successfully modified the following machines:


 * Rancilio Silvia V1 – V4
 * Rancilio Silvia E(co) V5 & V6
 * Gaggia Classic (9303) / Classic Pro (9480)
 * Lelit PL41 / PL42
 * La Pavoni EPL / Saeco Aroma / Gaggia New Classic (9403)
 * E61 single boiler (Bazzar A1 Livello, Fiorenzato Colombina)
 * E61 single boiler, dual use (Profitec Pro500)
 * Quick Mill Retro (0835) & Orione (3000)

## Differences PID Only vs. full expansion

In principle, our PID consists of the following components:
ID | Explanation
-|-
1 | Micro controller NodeMCU V2                 
2 | Temperature sensor TSIC 306                 
3 | Solid State Relais (SSR)                       
4 | Powersupply               
5 | Display (recommended, but optional)      

![Trockenaufbau](../../img/trockenaufbau.png)


There are two different levels of our system: PID only and full expansion


## Basic version (PID Only)

The basic version resembles a classic PID controller: the temperature sensor measures the temperature of the boiler (input) and forwards this information to the PID software running on the Micro controller (in our case NodeMCU). From here a control signal (output) is sent to the SSR which in turn switches the heating on and off. 

By that, the PID software achieves an exact regulation of the brewing temperature while the remainder of your machine stays untouched. MQTT, Display output and control via app are also possible in the basic version. 


## Full expansion

Here, we go one step further and transfer control over the pump and the solenoid valve to the software too. This enables additional possibilities with three time intervals to define in the app:


* Pre-Infusion: the pump generates pressure and the solenoid valve applies water onto the portafilter

* Pause: the pump pauses, but since the solenoid is still activated, the build up pressure remains in the portafilter. The coffe puck gets evenly wet, which can help to reduce channeling.

* Brew time: now, the normal brewing starts with the predefined time, e.g. 25 seconds. Depending on the coffee and your personal preference, a longer or shorter brewing time can improve the taste of the Espresso


One more thing which slightly changes in full expansion mode is the use of the brewing switch, which so far has been used to start and stop the brewing. This switch turns into a button now which only starts the automatic brewing sequence. The brewing is stopped by the software only, even if the switch is still in the "on" position.

We recommend to start with the basic version first, which usually leads to the biggest improvement in terms of taste of the Espresso. The full expansion is a further addon with more possibilities but also goes along with a more complex modification of your machine.


---
title: MQTT
parent: Konfiguration & Anpassung
grand_parent: DE - Handbuch
has_children: false
nav_order: 4
---

# MQTT
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

# Konfiguration

Für MQTT können nach der Konfiguration von folgenden Punkten in der userconfig genutzt werden:
```
#define MQTT_USERNAME
#define MQTT_PASSWORD 
#define MQTT_TOPIC_PREFIX   
#define MQTT_SERVER_IP     
#define MQTT_SERVER_PORT 
```

Werte können mit 
custom/{MQTT_TOPIC_PREFIX}/{var}/set gesetzt werden. 

z.B:
custom/Küche.Rancilio/setPoint/set 96

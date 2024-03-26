---
title: Global remote
layout: default
parent: Roller shutters
nav_order: 3
has_children: true
---


Now that all devices are flashed, I need a common remote controller to open/close them all at once.

I have still many ESP-12 and I wanted a "generic" code with main features like OTA, RF management, AP mode, ...

So I decided to understand Tasmota to create my how configuration.

# Global remote controller
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

---

## Some additional info about ESP-12

ESP-12S and ESP-12L modules have those pins already pulled internally. It is recommended to choose this version for easier installation.

ESP-12E and ESP-12F modules need the GPIO15 pulled low and CH_PD or EN pin pulled high to boot
https://templates.blakadder.com/ESP-12.html



## How to set up PINs

I used console log to send configuration commands.

https://tasmota.github.io/docs/GPIO-Conversion/#gpio-conversion is required to know which indexes to use.

If you can avoid it, don't use GPIOs: 0, 1, 2, 6-11, 15 and 16. That leaves 4, 5, 12, 13, 14 as GPIOs without any constraints. 3 being RX is also good to avoid (PWM is not working on this GPIO).

Here my commands : 
- GPIO14 	32
- GPIO13 	33
- GPIO5 	34
- GPIO12    1152

32, 33 and 34 are Button1, Button2 and Button3.

1152 is to used RF receive signal

## About RF 433Mhz configuration

I wanted to use radio waves and with Tasmota this is possible.

First, you have to configure pins like described in previous section.

After, even if Tasmota can handle it, you need to activate it and compile it yourself.
(Check RF_SENSOR and USE_RC_SWITCH option in your code)

Finally, you can plug your RF 433Mhz module (in my case a RBX6) on correct PIN (GPIO12 in my case).


## About rules 

TODO

To use RF module :
```
ON RfReceived#Data=<hex-value> DO <command> ENDON
```

For buttons : 
```
GPIO5 	162
Rule3 ON Switch3#state DO Reset 1 ENDON
Rule3 1


GPIO13 	161
Rule2 ON Switch2#state DO Backlog publish cmnd/Volet_Salon_centre/Start_Opening; publish cmnd/Volet_Cuisine_terrasse/Start_Opening; publish cmnd/Volet_Salon_terrasse/Start_Opening; publish cmnd/Volet_Salon_devant/POWER ON; publish cmnd/Volet_Cuisine_fenetre/POWER ON ENDON

Rule2 1


GPIO14 	160
Rule1 ON Switch2#state DO Backlog publish cmnd/Volet_Salon_centre/Start_Closing; publish cmnd/Volet_Cuisine_terrasse/Start_Closing; publish cmnd/Volet_Salon_terrasse/Start_Closing; publish cmnd/Volet_Salon_devant/POWER2 ON; publish cmnd/Volet_Cuisine_fenetre/POWER2 ON ENDON

rule1 1
```

## Tricks

I don't know exactly why and how I could simplify this but 
- I have to set up "generic" template with 18 pins first
- Don't forget to configure MQTT
- Not found a better way to configure pins that commands in console log
- Not forget to ACTIVATE rules with ruleX 1
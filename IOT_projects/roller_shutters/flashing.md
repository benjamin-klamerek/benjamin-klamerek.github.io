---
title: Flashing
layout: default
parent: Roller shutters
nav_order: 1
---

# Flashing
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

## Tasmota and OpenBeken

First, I tried to use [Tasmota](https://github.com/arendst/Tasmota), 
but I discover that the model that I choose are not using ESP microcontrollers but specific Tuya models.

Even if they are really close in terms of structure (size, features, pins, ...) you CANNOT use Tasmota (yet).

In my roller shutters, the Tuya model used is CB3S. 

I saw a [tutorial](https://blakadder.com/replace-tuya-esp12/) to swap Tuya model by an ESP. But in my case, it was not working.
(Not sure if this is not possible or if I did a mistake when soldering)

Hopefully, there is one another [project](https://github.com/openshwprojects/OpenBK7231T_App) to flash these devices.

But it requires a little more work.


## Flash tooling

### Device accessibility

To flash it, you will have either to solder some pins or either unsolder the full CB3S component.

![etersky.jpg]({% link IOT_projects/roller_shutters/images/unsolder_device.jpg %})

In my case, I decided to fully remove CB3S component because : 
- I thought it was possible to replace it per an ESP12 (failed)
- It seems that if you solder the pins directly you have to cut one connection

{: .note } 
After destroying 2 devices when trying to unsolder them, I found that the best option is to solder a copper wire first and, when removing, NEVER force. 

### Tool

https://github.com/openshwprojects/BK7231GUIFlashTool

Nothing particular about this open, I just used a burner like this one :

![etersky.jpg]({% link IOT_projects/roller_shutters/images/espburner.jpg %})

{: .note } 
Don't forget to test and use `OBK partition` to help you about Wifi configuration. 




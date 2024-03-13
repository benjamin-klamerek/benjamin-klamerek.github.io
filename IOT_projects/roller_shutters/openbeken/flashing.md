---
title: Flashing
layout: default
parent: OpenBeken
nav_order: 1
grand_parent: Roller shutters
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

## Flash tooling

### Device accessibility

To flash it, you will have either to solder some pins or either unsolder the full CB3S component.

![etersky.jpg]({% link IOT_projects/roller_shutters/images/unsolder_device.jpg %})

In my case, I decided to fully remove CB3S component because : 
- I thought it was possible to replace it per an ESP12 (failed)
- It seems that if you solder the pins directly you have to cut one connection (and repair it after, which may be even more hard to operate)

{: .note } 
After destroying 2 devices when trying to unsolder them, I found that the best option is to solder a copper wire first and, when removing, NEVER force. 

### Tool

https://github.com/openshwprojects/BK7231GUIFlashTool

Nothing particular about this open, I just used a burner like this one :

![etersky.jpg]({% link IOT_projects/roller_shutters/images/espburner.jpg %})

{: .note } 
Don't forget to test and use `OBK partition` to help you about Wifi configuration. 




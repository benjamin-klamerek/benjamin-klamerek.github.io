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

To flash it, you will either need to solder some pins or unsolder the full CB3S component.

![etersky.jpg]({% link IOT_projects/roller_shutters/images/unsolder_device.jpg %})

In my case, I decided to fully remove the CB3S component because:
- I thought it was possible to replace it with an ESP12 (it failed)
- It seems that if you solder the pins directly, you have to cut one connection (and repair it afterward, which may be even harder)

{: .note } 
After destroying 2 devices while trying to unsolder them, I found that the best option is to solder a copper wire first and, when removing it, NEVER force. 

### Tool

https://github.com/openshwprojects/BK7231GUIFlashTool

Nothing particular about this tool, I just used a burner like this one:

![etersky.jpg]({% link IOT_projects/roller_shutters/images/espburner.jpg %})

{: .note } 
Don't forget to test and use `OBK partition` to help with Wi-Fi configuration. 




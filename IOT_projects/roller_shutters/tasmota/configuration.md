---
title: Tasmota configuration
layout: default
parent: Tasmota
nav_order: 2
grand_parent: Roller shutters
---

# Tasmota configuration
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

## Find device after flashing

The Tasmota web installer provides this information directly.

It can also be found if you configured MQTT.

## PIN configuration

Simply follow these [instructions](https://templates.blakadder.com/etersky_WF-CS01.html)

{: .note }
Don't forget the link about WF-CS02 and execute command **Backlog Interlock 1,2,3; Interlock ON** before **ShutterRelay1 1**


{: .warning }
I wasted a lot of time due to unexpected behavior. After the template was applied, the buttons were not responding and showed the wrong color. I fixed the issue by saving the *module configuration*.

Finally, you will need to perform a [calibration](https://github.com/tasmota/docs-7.1/blob/master/Blinds-and-Shutters.md#calibration) depending on your configuration.


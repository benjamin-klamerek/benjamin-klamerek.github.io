---
title: Tasmota configuration
layout: default
parent: Tasmota
nav_order: 2
grand_parent: Roller shutters
---

# tasmota configuration
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

Tasmota web install give you this information directly.

It can also be found if you configured MQTT.

## PIN configuration

You just have to follow these [instructions](https://templates.blakadder.com/etersky_WF-CS01.html)

{: .note }
Don't forget the link about WF-CS02 and execute command **Backlog Interlock 1,2,3; Interlock ON** before **ShutterRelay1 1**


{: .warning }
I lost a lot of time due to a weird behavior. After template applied, buttons were not responding and of the wrong color. I fixed the issue by saving *module configuration*.

Finally, you will have to perform a [calibration](https://github.com/tasmota/docs-7.1/blob/master/Blinds-and-Shutters.md#calibration) depending on your configuration.


---
layout: default
title: Roller shutters
permalink: /roller_shutters/
nav_order: 4.5
has_children: true
---

Main page about every that I did about my roller shutters.

Model used : etersky WF-CS01

Why flashing ?

- Avoid using external server to send a command (Internet not required)
- Build a future common remote controller for all devices at once
- Build advanced workflows (like open partially depending on the day or sun detection) 

## Tasmota and OpenBeken

First, I tried to use [Tasmota](https://github.com/arendst/Tasmota),
but I discover that the model that I choose are not using ESP microcontrollers but specific Tuya models (CB3S).

Even if they are really close in terms of structure (size, features, pins, ...) you CANNOT use Tasmota (yet).

As always, *there is a trick* : the manufacturer switched from ESP12 like modules to Tuya models (CB3S).

You cannot guess it from the inside, you have to open it and check device label :

- CB3S or WB3S => specific Tuya model => [OpenBeken](https://github.com/openshwprojects/OpenBK7231T_App)
- TYWE3S => ESP like =>  [Tasmota](https://github.com/arendst/Tasmota)

I also saw a [tutorial](https://blakadder.com/replace-tuya-esp12/) to swap Tuya model by an ESP. But in my case, it was not working.
(Not sure if this is not possible due to hardware modifications or if I made a mistake when soldering)

![etersky.jpg]({% link IOT_projects/roller_shutters/images/etersky.jpg %})

## Table of contents
{: .no_toc .text-delta }


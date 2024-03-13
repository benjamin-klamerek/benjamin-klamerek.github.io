---
title: Flashing
layout: default
parent: Tasmota
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

Exactly the same compared to OpenBeken.

![etersky.jpg]({% link IOT_projects/roller_shutters/images/espburner.jpg %})

Previously it seems that you could flash directly with OTA but it's not more the case.

### Tool

Tasmota propose a highly useful tool to flash devices : https://tasmota.github.io/install/

It's very good because you can directly set up you Wifi parameters.

But, as always, we will have to do differently.

In my case, I took tasmota project to compile a firmware myself because I wanted to activate [blinds and shutters](https://tasmota.github.io/docs/Blinds-and-Shutters/).

With VS code and platform io, setting up the project is quite easy.

You will have to update *user_config_override.h* to define Wifi configuration, MQTT broker and to enable shutter code :

(https://tasmota.github.io/docs/Compile-your-build/#enabling-a-feature-in-tasmota
)
```
#ifndef USE_SHUTTER
#define USE_SHUTTER           // Add Shutter support (+6k code)
#endif
```

{: .note }
You may have issues with *firmware.bin* due to lack of space. Use the zipped version (automatically done by the project).
Therefore, you may have to install the minimal version before putting your version. Again, for spacing issues.






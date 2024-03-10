---
title: Roller shutters and MQTT
layout: default
parent: Roller shutters
nav_order: 3
---

Here the format of MQTT commands.

{: .warning }
Don't update the channel directly with MQTT. First, you will have stop manually the relay. Script is not launched when channel value is updated. Therefore, you may risk to activate both relays at the same time.

```
cmnd/XXX/YYY
```

Where :
- XXX must be replaced by device name set up in OpenBeken firmware
- YYY is the command (like `Start_Opening`). you can use an alias from teh script file.
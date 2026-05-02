---
title: MQTT
layout: default
parent: OpenBeken
nav_order: 3
grand_parent: Roller shutters
---

Here is the format of MQTT commands.

{: .warning }
Do not update the channel directly with MQTT. The script logic is not triggered when the channel value is updated. Therefore, you risk activating both relays at the same time.

```
cmnd/XXX/YYY
```

Where :
- XXX must be replaced by device name set up in OpenBeken firmware
- YYY is the command (like `Start_Opening`). You can use an alias from script file.

Examples:
- **cmnd/Volet_Salon_centre/Start_Opening**
- **cmnd/Volet_Salon_centre/Start_Closing**
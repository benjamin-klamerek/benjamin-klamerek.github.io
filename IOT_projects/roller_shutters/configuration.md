---
title: OpenBeken configuration
layout: default
parent: Roller shutters
nav_order: 2
---

# OpenBeken configuration
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

## Script

Here the script that emulate 90% of the behavior of the roller shutter :

(Some explanation can be found below the script)

```
// Set up Aliases
alias Start_Opening backlog stopAllScripts; startScript autoexec.bat openAction
alias Start_Closing backlog stopAllScripts; startScript autoexec.bat closeAction
alias Stop_All backlog stopAllScripts; startScript autoexec.bat stopAction
alias Stop_All_Channels backlog setChannel 1 0; setChannel 2 0; setChannel 3 0
alias Initial_Button_Color backlog setButtonColor 1 blue; setButtonColor 2 blue; setButtonColor 3 blue

//To make this component visible in Windows
startDriver SSDP

// create GUI buttons for HTTP panel
startDriver httpButtons

SetChannelLabel 1 UP 1
SetChannelLabel 2 STOP 1
SetChannelLabel 3 DOWN 1
SetChannelLabel 4 DURATION 1
SetChannelLabel 5 STOP_COUNT 1

setButtonEnabled 1 1
setButtonLabel 1 "Open"
setButtonCommand 1 Start_Opening
setButtonColor 1 blue

setButtonEnabled 2 1
setButtonLabel 2 "Stop"
setButtonCommand 2 Stop_All
setButtonColor 2 blue

setButtonEnabled 3 1
setButtonLabel 3 "Close"
setButtonCommand 3 Start_Closing
setButtonColor 3 blue

// Hide the default GUI buttons
setChannelVisible 1 0
setChannelVisible 2 0
setChannelVisible 3 0

// Loading Event Handlers
addEventHandler OnClick 24 Start_Opening
addEventHandler OnClick 10 Stop_All
addEventHandler OnClick 7 Start_Closing

setPinRole 7 Btn
setPinRole 10 Btn
setPinRole 24 Btn

setPinRole 6 Rel
setPinRole 9 Rel
setPinChannel 6 1
setPinChannel 9 3

setPinRole 14 LED
setPinRole 8 LED
setPinRole 23 LED
setPinChannel 14 1
setPinChannel 8 2
setPinChannel 23 3

setChannelType 5 TextField

setChannelType 4 TextField
if $CH4>0 then goto stopAction
setChannel 4 17

// Close on power up
goto stopAction

// do not proceed
return

openAction:
setChannel 5 0
setButtonColor 1 red
setButtonColor 2 blue
setButtonColor 3 blue
Stop_All_Channels
delay_s 0.1
setChannel 1 1
delay_s $CH4
setChannel 1 0
setChannel 2 1
delay_s 2
Stop_All_Channels
Initial_Button_Color
return

closeAction:
setChannel 5 0
setButtonColor 1 blue
setButtonColor 2 blue
setButtonColor 3 red
Stop_All_Channels
delay_s 0.1
setChannel 3 1
delay_s $CH4
setChannel 3 0
setChannel 2 1
delay_s 2
Stop_All_Channels
Initial_Button_Color
return

stopAction:
addChannel 5 1
if $CH5>9 then goto enterSafeMode
setButtonColor 1 blue
setButtonColor 2 red
setButtonColor 3 blue
setChannel 1 0
setChannel 2 1
setChannel 3 0
delay_s 2
Stop_All_Channels
Initial_Button_Color
return

enterSafeMode:
SafeMode 3
return
```
___

## Tips

- To make the device visible in Windows (not a DNS name) : 

```
startDriver SSDP
```

- `backlog` is needed to put multiple commands on the same line

- `alias Start_Opening` an alias is also useful to be called from external command (like MQTT)

- Channel 5 is a special counter to activate safe mode (after pushing `stop` button many times). 
In safe mode, you can access the device in AP mode. Pins are disabled. Very useful when Wifi configuration is not more valid.


TODO


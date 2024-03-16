---
title: OpenBeken configuration
layout: default
parent: OpenBeken
nav_order: 2
grand_parent: Roller shutters
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

## Find device after flashing

It's maybe obvious but flash tool will not give you the IP used by the device and there is no DNS setup.

So, to find it, you will have to use your local box and identify it (most the time : 192.168.1.1)

When you have the IP, you can open the browser and start configuration.

## PIN retro engineering

There is a screen with OpenBeken firmware where you can play with pin board to detect if they are set up as input and output.

(And also see the effect on the device)

{: .warning }
When trying to duplicate the logic on a second device, I discovered that depending on the controller used (WB3S or CB3S), the mapping is not exactly the same.

Here Etersky roller shutter pin allocation (CB3S): 

```
- P6 => Relay 1 (UP)
- P9 => Relay 2 (DOWN)
- P11 => Shutdown all button leds when active
- P14 => LED on button 1 red when activated (blue otherwise)
- P8 => LED on button 2 red when activated (blue otherwise)
- P23 => LED on button 3 red when activated (blue otherwise)
- P36 => Activate second LED on button 1 (green)
- P24 => Button 1
- P10 => Button 2
- P7 => Button 3
```

Here Etersky roller shutter pin allocation (WB3S):

```
- P6 => Relay 1 (UP)
- P7 => Relay 2 (DOWN)
- P11 => Shutdown all button leds when active
- P14 => LED on button 1 red when activated (blue otherwise)
- P26 => LED on button 2 red when activated (blue otherwise)
- P0 => LED on button 3 red when activated (blue otherwise)
- P1 => Activate second LED on button 1 (green)
- P24 => Button 1
- P10 => Button 2
- P8 => Button 3
```

You can assign roles to pins. This is done automatically by the script below.

Here some info about it : https://github.com/openshwprojects/OpenBK7231T_App/blob/main/docs/ioRoles.md?plain=1

## Script

Here the script that emulate 90% of the behavior of the roller shutter (CB3S version) :

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

And here the WB3S version :

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
addEventHandler OnClick 8 Start_Closing

setPinRole 24 Btn
setPinRole 10 Btn
setPinRole 8 Btn

setPinRole 6 Rel
setPinRole 7 Rel
setPinChannel 6 1
setPinChannel 7 3

setPinRole 14 LED
setPinRole 0 LED
setPinRole 26 LED
setPinChannel 14 1
setPinChannel 0 3
setPinChannel 26 2

setPinRole 1 LED_n
setPinChannel 1 6
setChannel 6 1

setChannelType 5 TextField

setChannelType 4 TextField
if $CH4>0 then goto stopAction
setChannel 4 40

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

- https://github.com/openshwprojects/OpenBK7231T_App/blob/main/docs/commands.md
  

- To make the device visible in Windows (not a DNS name) : 

```
startDriver SSDP
```

- `backlog` is needed to put multiple commands on the same line

- `alias Start_Opening` an alias is also useful to be called from external command (like MQTT)

- Channel 5 is a special counter variable to activate safe mode (after pushing `stop` button many times). 
In safe mode, you can access the device in AP mode. Pins are disabled. Very useful when Wifi configuration is no more valid.



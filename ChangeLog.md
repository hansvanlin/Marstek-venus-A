



### 1.01 Stability fix\

  • In some cases settings from Mode-engine did not get passed rbe.\
  • Removed delay and some rbe nodes causing timing issues.\


## **1.00 Release version**

> First public release of the Marstek Venus A controller.\
>\
> 🔧 Features:\
>\
> Local control\
> Charge / Discharge\
> AntiFeed\
> Price based control\
> Schedule control\
> Force mode control\
> Modbus register access\
> SMA integration examples\
> Battery tooling\
> Node-Red UI 



0.1.9. added the power slider\
0.1.8  cleanup unused nodes and bug fix\
0.1.7  due to the discharging fw bug I found a new way to contol the battery using the schedule scheme.\
0.1.6  added 3th battery and changed UI layout\
0.1.5  cleanup mode engine\
0.1.4  fixed unwanted switch to self during expensive hour\
0.1.3  fixing rbe issue out of sync in some situation\
0.1.2  cleanup and node reduction small fixes\
0.1.1  bugfix\
0.1    Changed to engine v4.1 removed deadlock\
0.09   Added hysteris in engine v4\
0.08.9 Changed to mode engine v3\
0.08.8 timebased issues simplified self\
0.08.7 simplified sequences solved timing issue\
0.08.6 cleanup and fixes\
0.08.5 sunrise / sunset triggers\
0.08.4 added zonneplan hours, start self mode when soft limits used\
0.08.3 after update to fw147.7 simplified restore modbus by just resetting networkswitch only\
0.08.2 close rs485 (off), cleaned up\
0.08.1 added take control part\
0.08   cleaned up and auto re boot "wake up the self mode" , bugfixes\
0.07.7 modbus still alive function\
0.07.6 minor fixes\
0.07.5 added actual check for charging, prevent discharge\
0.07.4 improved status charge led\
0.07.3 added status leds gates and values set.\
0.07.2 bug fix\
0.07.1 changed setting in core filternode

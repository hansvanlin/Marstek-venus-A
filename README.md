# Marstek-venus-A
Node-red script with UI to control the Marstek venus A (Tested up to firmware 149)
\
How to use Node-red: https://nodered.org \
\
Simple UI to control the schedule modes (modbus schedule registers) without diging deep into marstek app to toggle the options.
The flow is easy to adapt to your needs.
For now the script is using software ranges the target soc registers don't react yet on the values stored.
Maybe in the future with different firmware it is different.
If the limit is reached the mode is changed to manual. If in the morning enough solar is detected it 
switches back to self mode for charging and back to manual if not enough is generated and back to self if it does.
## **The UI has 3 modes:**
***1. Antifeed (soft limits):*** using the Marstek own antifeed routine which keeps the P1 at zero (zero feedback, MOM) and keep the SOC within min and max set value's.\
***2. Price based mode:*** Using enever (zonneplan) day ahead prices looking for the cheap and expensive hours. Default is 4 cheapest hours to charge and 1 hour for the expensive\    hours to discharge max power and save some capacity for self mode.\
***3. Charge PV:*** Charge the batteries whenever there is enough sun. Charge only without any feedback to the grid.\
\
The flow makes use of the "node-red-contrib-modbus" nodes.
Adapt the marstek Ip number to your "your Ip number" with port ":502"
\
From version 0.1.5 a 3th battery is added since I'm going to buy a 3th set. 

Also it is easier to remove/ disable batteries than adding them.
\
Due to the discharge bug I changed to different way of controlling the batteries. From version 0.1.7 I'm using the schedule's which I can change via Modbus.
In this version power settings can be set in the UI. The power can be set to 1500W in case it doesn't discharge try 1400W to avoid the fw bug.
\
\
<img width="1866" height="849" alt="image" src="https://github.com/user-attachments/assets/dab7ba52-5fc6-49d3-9a71-0387e06a8484" />
\
\
> [!IMPORTANT]
> **Firmware Update Workaround (Discharge Issue, not needed from v0.1.7):**
> If discharging at 1500W via Modbus does not start, create a 24-hour discharge schedule set to 1500W in the official Marstek app, but leave the schedule **Disabled** (do not turn it on). This forces the firmware to keep the necessary registers open, allowing this Node-RED script to control the battery correctly.

\
\
Check also my updated Inverter Control: https://github.com/hansvanlin/SMA-Tripower-5.0---Active-Power-Control
\
\
Modbus test tool: https://flows.nodered.org/flow/e23f1387358c45281e10b83a8fc65744
\
\
"Price Based Mode ON" result:\
Charge or buy during cheap hours and sell for eg 1hour at expensive hour;
\
<img width="585" height="1026" alt="image" src="https://github.com/user-attachments/assets/0fa33994-11fd-4764-901c-e4f1c216dd5d" />
\
\
\
Orange is energy used from grid.
\
\
<img width="1102" height="543" alt="image" src="https://github.com/user-attachments/assets/9ec237ec-6d33-4e17-857f-b84cac47b69d" />
\
Marstek simple fast schedule write sequence:
<img width="1319" height="203" alt="image" src="https://github.com/user-attachments/assets/d1f9779c-742d-4a94-9180-ab7d28449826" />
\
Pulldown menu items:
<img width="318" height="325" alt="image" src="https://github.com/user-attachments/assets/ef70cf06-a297-4bc6-b18c-2057ae50c545" />
\
\
Added Modbus " still alive " and scheduled auto reset/reboot function:\
<img width="265" height="1032" alt="image" src="https://github.com/user-attachments/assets/e6ce0539-3815-4147-8b77-e092493f9ac5" />



Modbus Leds:\
Red: communication error\
Green: commnunication ok\
Pink: communication ok, data not changed\
Light green: communication ok, data has changed

\
Added status Leds:\
<img width="429" height="1027" alt="image" src="https://github.com/user-attachments/assets/49de9165-c74c-4516-97c2-1f3690b7762e" />
\
Red: Disabled\
Pink: Enabled\
Green: Value within limits or Solar high enough to charge\
Yellow: Idle or Solar not high enough.
\

\
Force Mode:\
First switch on Force Mode\
Select in the pull down menu one off the options eg:discharge\
Then use the slider to which level it should discharge eg: 20% (For charge use 80-100%) \

example with exported SOC and Power to domoticz:
<img width="1752" height="686" alt="image" src="https://github.com/user-attachments/assets/afc33b4d-bdce-44ed-a5cf-fdf765726842" />

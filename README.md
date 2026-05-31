# Marstek-venus-A
Node-red script with UI to control the Marstek venus A (Tested up to firmware 149)
\
How to use Node-red: https://nodered.org \
\
Simple UI to control the schedule modes (modbus schedule registers) without diging deep into marstek app to toggle the options.

<img width="577" height="1805" alt="Screenshot_20260530_224551_Gallery" src="https://github.com/user-attachments/assets/a4b45200-8de4-4cd4-a87b-0fdbe3b85251" />


## **The UI has 3 modes:**
***1. Antifeed (soft limits):*** using the Marstek own antifeed routine which keeps the P1 at zero (zero feedback, NOM) and keep the SOC within min and max set value's.

***2. Price based mode:*** Using enever (zonneplan) day ahead prices looking for the cheap and expensive hours. Default is 4 cheapest hours to charge and 1 hour for the expensive\    hours to discharge max power and save some capacity for self mode.

***3. Charge PV:*** Charge the batteries whenever there is enough sun. Charge only without any feedback to the grid.\
\
The flow makes use of the "node-red-contrib-modbus" nodes.
Adapt the marstek Ip number to your "your Ip number" with port ":502"
\
\
Due to the discharge bug I changed to different way of controlling the batteries. 
From version 0.1.7 I'm using one of the Marstek schedule's and configure it via Modbus registers 43100-43104. These registers are written in one command thru the "Marstek Mode controller" node.
\
\
Dis/Charge Power setting can be set in the UI. The power can be set from 100W to 1500W in case it doesn't discharge try 1400W to avoid the fw bug.
\
\
<img width="1866" height="849" alt="image" src="https://github.com/user-attachments/assets/dab7ba52-5fc6-49d3-9a71-0387e06a8484" />
\
\
> [!IMPORTANT]
> **Firmware Update Workaround (Discharge Issue, not needed from v0.1.7):**
> If discharg,ing at 1500W via Modbus does not start, create a 24-hour discharge schedule set to 1500W in the official Marstek app, but leave the schedule **Disabled** (do not turn it on). This forces the firmware to keep the necessary registers open, allowing this Node-RED script to control the battery correctly.

\
\
Check also my updated Inverter Control: https://github.com/hansvanlin/SMA-Tripower-5.0---Active-Power-Control
\
\
Modbus test tool: https://flows.nodered.org/flow/e23f1387358c45281e10b83a8fc65744


## How to Install:

1. InstWall Node-RED
   https://nodered.org/docs/getting-started/

2. Open the Node-RED workspace
   http://localhost:1880

3. Install the missing nodes
   Not every node is included by default in Node-RED.

4. Import the flow files

   * Import the Zonneplan JSON file
   * Import the Marstek JSON file

5. Deploy the flows

6. Configure the Modbus nodes

   * Set the correct IP address
   * Use port `502`

7. Open the dashboard UI
   http://localhost:1880/ui




## **Write Schedule Method:**
Marstek Mode Controller Schedule Registers
\
The Mode Controller creates and activates a schedule by writing the following Modbus registers.
\
\
Register| Value| Description\
43100| 127| Active days bitmask (Monday-Sunday)\
43101| 0000| Start time (HHMM)\
43102| 2359| End time (HHMM)\
43103| Mode dependent| Power or control value\
43104| 0 / 1| Schedule enable (0 = disabled, 1 = enabled)\
\
Day Bitmask (Register 43100)\
\
Bit| Value| Day\
0| 1| Monday\
1| 2| Tuesday\
2| 4| Wednesday\
3| 8| Thursday\
4| 16| Friday\
5| 32| Saturday\
6| 64| Sunday\
\
Example:\
\
Value| Active Days\
127| Monday-Sunday\
31| Monday-Friday\
96| Saturday-Sunday\
\
Mode Values (Register 43103)\
\
Input Mode| Function| Register Value\
0| Disabled| 64036\
1| AntiFeed| 65535\
2| Discharge| Power value (100-1500 W)\
3| Charge| 65536 - Power value\
\
Examples
\
Mode| Power| Register 43103\
AntiFeed| N/A| 65535\
Discharge| 800 W| 800\
Charge| 800 W| 64736\
Disabled| N/A| 64036\
\
Write Sequence
\
The controller writes the registers in the following order:

1. Disable schedule ("43104 = 0")
2. Set active days ("43100 = 127")
3. Set start time ("43101 = 0000")
4. Set end time ("43102 = 2359")
5. Set mode/power value ("43103")
6. Enable schedule ("43104 = 1")


## **Some ScreenShots:**
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
\
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

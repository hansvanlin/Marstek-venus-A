# Marstek-venus-A
Node-red script with UI to control the Marstek venus A (Tested with firmware 144, 147 and 147.3) \
\
\
How to use Node-red: https://nodered.org \
\
Simple UI to control self or manual mode without diging deep into marstek app to toggle the options.
The flow is easy to adapt to your needs.
If the modbus becomes more clear what registers to use I will adapt the UI.
For now the script is using software ranges the target soc registers don't react yet on the values stored.
Maybe in the future with different firmware it is different.
If the limit is reached the mode is changed to manual. If in the morning enough solar is detected it 
switches back to self mode for charging and back to manual if not enough is generated and back to self if it does.
\
The flow makes use of the "node-red-contrib-modbus" nodes.
Adapt the marstek Ip number to your "your Ip number" with port ":502"

Check also my updated Inverter Control: https://github.com/hansvanlin/SMA-Tripower-5.0---Active-Power-Control
\
\
Modbus test tool: https://flows.nodered.org/flow/e23f1387358c45281e10b83a8fc65744
\

\
Added status Leds:\
<img width="429" height="1027" alt="image" src="https://github.com/user-attachments/assets/49de9165-c74c-4516-97c2-1f3690b7762e" />
\
Red: Disabled\
Pink: Enabled\
Green: Value within limits or Solar high enough to charge\
Yellow: Idle or no value detected yet.
\


Added controll options:\
<img width="482" height="1040" alt="image" src="https://github.com/user-attachments/assets/abe42db2-bcc5-49cc-a603-fd16c81a5e52" />


\
auto flow:
\
<img width="1166" height="602" alt="image" src="https://github.com/user-attachments/assets/da741154-4bc0-433b-92bf-027f2f5e90b2" />


\
Force Mode:\
First switch on Force Mode\
Select in the pull down menu one off the options eg:discharge\
Then use the slider to which level it should discharge eg: 20% (For charge use 80-100%) \




flow Reading modbus registers:
<img width="942" height="435" alt="image" src="https://github.com/user-attachments/assets/df028d9e-af0f-4dcd-aaa3-959b4411bb5b" />

flow Write to modbus registers:\
<img width="394" height="111" alt="image" src="https://github.com/user-attachments/assets/364ea11a-faab-4a28-a08a-7c846669ba1c" />

example with exported SOC and Power to domoticz:
<img width="1752" height="686" alt="image" src="https://github.com/user-attachments/assets/afc33b4d-bdce-44ed-a5cf-fdf765726842" />

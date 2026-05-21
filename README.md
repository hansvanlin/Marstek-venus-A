# Marstek-venus-A
Node-red script with UI to control the Marstek venus A (Tested with firmware 147.7 and 148) \
My Experience is that firmware 147.7 responds better with start charging (in self mode when requested by the script).
\
How to use Node-red: https://nodered.org \
\
Simple UI to control self or manual mode without diging deep into marstek app to toggle the options.
The flow is easy to adapt to your needs.
For now the script is using software ranges the target soc registers don't react yet on the values stored.
Maybe in the future with different firmware it is different.
If the limit is reached the mode is changed to manual. If in the morning enough solar is detected it 
switches back to self mode for charging and back to manual if not enough is generated and back to self if it does.
\
Started to implement Price based mode, using enever (zonneplan) day ahead prices looking for the cheap and expensive hours. Default is 4 cheapest hours to charge and 1 hour for the expensive hours to discharge max power and save some capacity for self mode.
\
The flow makes use of the "node-red-contrib-modbus" nodes.
Adapt the marstek Ip number to your "your Ip number" with port ":502"

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
<img width="1102" height="543" alt="image" src="https://github.com/user-attachments/assets/9ec237ec-6d33-4e17-857f-b84cac47b69d" />
\

\
<img width="1604" height="449" alt="image" src="https://github.com/user-attachments/assets/3fc994dd-673b-413e-8a29-f1a5e8eb631c" />


\
Added Modbus " still alive " and scheduled auto reset/reboot function:\
<img width="242" height="584" alt="image" src="https://github.com/user-attachments/assets/81deab9c-402a-4717-a78d-0fed46f7e416" />

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

\
auto flow:
\
<img width="1534" height="803" alt="image" src="https://github.com/user-attachments/assets/8141aa0a-eccf-467d-9edd-d249d7b16fa4" />



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

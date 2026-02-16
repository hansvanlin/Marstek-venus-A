# Marstek-venus-A
Node-red script with UI to control the Marstek venus A (Tested with firmware 144, 147 and 147.3) \
\
\
How to use Node-red: https://nodered.org \
\
Simple UI to control self or manual mode without diging deep into marstek app to toggle the options.
The flow is easy to adapt to your needs.
If the modbus becomes more clear what registers to use I will adapt the UI.
\
The flow makes use of the "node-red-contrib-modbus" nodes.
Adapt the marstek Ip number to your "your Ip number" with port ":502"

Check also my updated Inverter Control: https://github.com/hansvanlin/SMA-Tripower-5.0---Active-Power-Control
\
\
Modbus test tool: https://flows.nodered.org/flow/e23f1387358c45281e10b83a8fc65744
\

Added controll options:\
<img width="269" height="584" alt="image" src="https://github.com/user-attachments/assets/0f3c34b8-3225-44c4-8865-cc7bde6c68c6" />

\
auto flow:
\
<img width="828" height="470" alt="image" src="https://github.com/user-attachments/assets/50ccb0ac-f349-49a9-ae32-c2ad6f449fae" />

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

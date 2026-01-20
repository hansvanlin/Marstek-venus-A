# Marstek-venus-A
Node-red script with UI to control the Marstek venus A
\
Simple UI to control self or manual mode without diging deep into marstek app to toggle the options.
The flow is easy to adapt to your needs.
If the modbus becomes more clear what registers to use I will adapt the UI.
\
The flow makes use of the "node-red-contrib-modbus" nodes.
Adapt the marstek Ip number to your "your Ip number" with port ":502"

Check also my updated Inverter Control: https://github.com/hansvanlin/SMA-Tripower-5.0---Active-Power-Control

Added controll options:\
<img width="310" height="610" alt="image" src="https://github.com/user-attachments/assets/143c323d-58e9-4f7f-bb1d-eb8b5667b61a" />



flow Reading modbus registers:
<img width="942" height="435" alt="image" src="https://github.com/user-attachments/assets/df028d9e-af0f-4dcd-aaa3-959b4411bb5b" />

flow Write to modbus registers:\
<img width="394" height="111" alt="image" src="https://github.com/user-attachments/assets/364ea11a-faab-4a28-a08a-7c846669ba1c" />

example with exported SOC and Power to domoticz:
<img width="1752" height="686" alt="image" src="https://github.com/user-attachments/assets/afc33b4d-bdce-44ed-a5cf-fdf765726842" />

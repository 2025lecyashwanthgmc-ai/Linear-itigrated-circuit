# Linear-itigrated-circuit
## Simulation Setup

To replicate these results in LTspice, use the following parameters:\
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/ba092f8a-60e5-46f3-a6cb-8ff8ea25abab" />


### NMOS Model (TSMC 180nm)
* **Model Name:** CMOSN
* **Length (L):** 180nm
* **Width (W):** 10µm (Adjusted for $I_D \approx 0.3mA$)

### Components
| Component | Value | Function |
| :--- | :--- | :--- |
| **$R_D$** | 2 kΩ | Drain Resistor |
| **$C_L$** | 0.5 pF | Load Capacitor |
| **$V_{DD}$** | 1.2 V | Supply Voltage |
| **$V_{in}$** | 0.6 V (DC) | Gate Bias |

### SPICE Directives
* **Transient:** `.tran 5m` (5ms simulation)
* **AC Analysis:** `.ac dec 10 1 1G` (Frequency sweep)
* **DC Sweep:** `.dc Vin 0 1.2 0.01` (Voltage sweep)

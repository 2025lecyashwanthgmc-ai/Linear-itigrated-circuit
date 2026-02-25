# Linear-itigrated-circuit
## Simulation Setup

# Experiment 1: DC, Transient, and AC Analysis of CS Amplifier (180nm)

## 1. Introduction
The **Common Source (CS) Amplifier** is a fundamental building block in analog integrated circuit design. It is primarily used for voltage amplification due to its high input impedance and significant voltage gain. In this project, we utilize the **TSMC 180nm CMOS technology** to design an NMOS-based CS amplifier that meets specific power and gain constraints.

### Key Characteristics:
* **Input:** Gate terminal (High impedance)
* **Output:** Drain terminal (High gain)
* **Phase:** 180° phase inversion (Negative Gain)
* **Configuration:** Source terminal is grounded, making it "Common."



---

## 2. Design Specifications & Constraints
The design is governed by the following parameters to ensure operation within the 180nm process limits:

| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| Supply Voltage | $V_{DD}$ | 1.2V |
| Max Power Limit | $P$ | $\le 0.4$ mW |
| Load Capacitance | $C_L$ | 0.5 pF |
| Channel Length | $L$ | 180 nm |
| Threshold Voltage | $V_{th}$ | $\approx 0.366$ V |

---

## 3. Theoretical Derivations & Design Steps

## CIRCUIT DIAGRAM :

![Image description](https://github.com/2025lecyashwanthgmc-ai/Linear-itigrated-circuit/blob/main/circuit.jpeg?raw=true)
---

---

## THEORY :

A Common Source (CS) amplifier is one of the fundamental MOSFET amplifier configurations.  
In this configuration, the source terminal is grounded, the input is applied at the gate and the output is taken from the drain.
The amplifier provides voltage gain with a phase inversion of 180 degrees between input and output.  
For proper amplification, the MOSFET must operate in the saturation region.  
Therefore, the Q-point is fixed such that VDS ≈ VDD/2 to allow maximum symmetrical output swing.

A common Source (CS) amplifier is one of the most widely used MOSFET amplifier configurations due to its high voltage gain and simple design. In this configuration, the source terminal is connected to ground, the input signal is applied to the gate, and the output is taken from the drain terminal. When a small AC signal is applied at the gate, it modulates the drain current, which in turn produces a larger voltage variation across the drain resistor. This results in an amplified output signal

 A key characteristic of the CS amplifier is that the output voltage is inverted by 180° relative to the input signal, meaning a positive input swing produces a negative output swing.
For proper amplification, the MOSFET must operate in the saturation region, where the drain current becomes primarily dependent on the gate-to-source voltage rather than the drain voltage. To ensure this, a suitable DC biasing network is used to establish the operating point (Q-point).


Typically, the drain-to-source voltage is set near VDS ≈ VDD/2, allowing the output signal to swing equally in both directions without distortion, thereby achieving maximum symmetrical output swing. The biasing network may include a voltage divider at the gate, a drain resistor to convert current variations into voltage, and sometimes a source resistor for thermal stability and improved bias control.
The small-signal voltage gain of a CS amplifier is approximately given by Av ≈ −gmRD, where gm is the transconductance of the MOSFET and RD is the drain resistance. The negative sign indicates phase inversion. The input impedance of the CS amplifier is very high because the MOSFET gate draws negligible current, making it suitable for interfacing with high-impedance signal sources. The output impedance is relatively high and is mainly determined by the drain resistor and the transistor’s internal resistance.

## PROCEDURE :

1. The 180nm NMOS model file (tsmc018.lib) was included in LTspice using the .include directive.

2. The Common Source amplifier circuit was constructed with:
   - VDD = 1.2 V  
   - Drain resistor RD ≈ 1.8 kΩ  
   - NMOS transistor with L = 180 nm and W = 1.07 µm    

3. DC analysis was performed using the .op and .dc commands to determine the Q-point by setting VDS ≈ VDD/2.

4. RD was adjusted and W/L ratio was varied to achieve the required drain current under the power constraint (P ≤ 0.5 mW).

5. Transient analysis (.tran 5m) was carried out using a sine input SINE(0.9 10m 1k) to observe linear and non-linear behavior.

6. AC analysis (.ac dec 10 0.1 100G) was performed to obtain frequency response and determine gain and bandwidth parameters.

### A. DC Operating Point (Q-Point)
To maximize the output signal swing, we target a quiescent drain voltage ($V_{DS}$) at half of the supply voltage:
$$V_{DS} = \frac{V_{DD}}{2} = 0.6 \text{ V}$$

 Quiescent Drain Voltage Selection
To achieve maximum symmetrical output swing, the drain voltage is set at approximately half of the supply voltage.
This midpoint bias allows the output signal to swing equally in the positive and negative directions without distortion or clipping.
It also ensures the MOSFET remains in the saturation region during signal variations, enabling linear amplification.
![Image description](https://github.com/2025lecyashwanthgmc-ai/Linear-itigrated-circuit/blob/main/Qpoint.jpeg?raw=true)

### B. Drain Current Calculation
Using the power constraint $P = V_{DD} \times I_D$:
$$I_D = \frac{0.4 \text{ mW}}{1.2 \text{ V}} = 0.2 \text{ mA}$$
*Selected Design Value:* **$I_D = 0.2 \text{ mA}$** (to provide a 10% safety margin).

 Drain Current Consideration
The drain current is chosen based on the power budget and desired operating stability.
Selecting a moderate current ensures:
low power dissipation
improved device reliability
reduced thermal stress
stable biasing conditions
Designers often include a safety margin to prevent overheating and parameter variations from affecting performance.


### C. Drain Resistor ($R_D$) Selection
$$R_D = \frac{V_{DD} - V_{DS}}{I_D} = \frac{1.2 - 0.6}{0.3 \text{ mA}} = 2 \text{ k}\Omega$$

 Role of the Drain Resistor (RD)
The drain resistor converts variations in drain current into output voltage.
It plays a crucial role in:
setting the DC operating point
controlling the output voltage swing
determining the voltage gain
A properly chosen RD ensures sufficient voltage drop while maintaining the transistor in saturation.

 
### D. Small-Signal Voltage Gain ($A_v$)

## W CALCULATION :

The gain is defined by the transconductance ($g_m$):
$$A_v = -g_m \times R_D$$
Based on simulation, for a $V_{GS} = 0.6\text{V}$, the expected gain is $\approx 5 \text{ V/V}$ (14 dB).


Using MOSFET saturation equation:

ID = (kn'/2) × (W/L) × (VGS − Vth)²  

Given:

VGS = 0.9 V  
Vth = 0.366 V  

(VGS − Vth) = 0.534 V  

L = 180 nm = 180 × 10⁻⁹ m  

Substituting:

2.00 × 10⁻⁴ = (2.30 × 10⁻⁴ / 2) × (W / 180 × 10⁻⁹) × (0.534)²  

Solving,

W ≈ 1.07 µm  

After simulation tuning to obtain accurate Q-point:

Final selected width:

W = 1.5 µm

---

## 4. Simulation Results

### DC Analysis (Operating Point)
The transistor is confirmed to be in the **Saturation Region** because:
* $V_{GS} (0.9V) > V_{th} (0.366V)$

### Transient Analysis
A 10mV, 1kHz sine wave was applied. The output shows a peak-to-peak swing of ~50mV, confirming a gain of 5.

Working Principle

The small AC signal applied at the gate causes variations in drain current.
These current variations produce amplified voltage variations across the drain resistor, resulting in an amplified output signal at the drain terminal.

Expected Output Behavior

Output signal is amplified relative to input.

Output waveform is inverted (180° phase shift).

Signal shape remains sinusoidal in the linear region.

Excessive input amplitude causes clipping and distortion.

Voltage Gain from Transient Response

Voltage gain can be measured directly from waveform amplitudes:

Av = Vout / Vin

Linear vs Non-Linear Operation

Linear Region:

Output waveform is undistorted.

Gain remains constant.

Non-Linear Region:

Occurs when input amplitude is too large.

Output shows clipping due to cutoff or triode operation.
![Image description](https://github.com/2025lecyashwanthgmc-ai/Linear-itigrated-circuit/blob/main/transient.jpeg?raw=true)

### AC Analysis (Frequency Response)
* **Midband Gain:** 6.9 dB
* **Bandwidth:** The high-frequency cutoff ($f_H$) is influenced by $C_L$.
* **Pole Frequency:** $f_p = \frac{1}{2\pi R_D C_L} \approx 159 \text{ MHz}$.
The input source AC magnitude was set to 1 V to directly obtain gain in V/V (or dB).

Voltage Gain

The small-signal voltage gain of a CS amplifier is approximately:
​

gm = transconductance of the MOSFET
RD = drain resistance

The negative sign indicates 180° phase inversion between input and output.

 - Frequency Response

The gain response of the amplifier consists of three regions:

- 1. Low-Frequency Region
Gain decreases due to coupling and bypass capacitors.

- 2. Midband Region
Gain remains constant and maximum.
This is the normal operating region of the amplifier.

- 3. High-Frequency Region
Gain decreases due to MOSFET parasitic capacitances (Cgs, Cgd, Cdb).

Cutoff Frequencies

- Lower cutoff frequency: fL (gain drops by 3 dB)

- Upper cutoff frequency: fH (gain drops by 3 dB)

Bandwidth​

Bandwidth indicates the range of frequencies over which the amplifier operates effectively.

---
## AC ANALYSIS SIMULATION :

![Image description](https://github.com/2025lecyashwanthgmc-ai/Linear-itigrated-circuit/blob/main/AC%20analysis.jpeg?raw=true)

## AC ANALYSIS WITH CAPACITOR :
![Image description](https://github.com/2025lecyashwanthgmc-ai/Linear-itigrated-circuit/blob/main/WITH%20C.jpeg?raw=true)

 ## AC ANALYSIS SIMULATION WITH CAPACITOR  :

![Image description](https://github.com/2025lecyashwanthgmc-ai/Linear-itigrated-circuit/blob/main/ac%20with%20c.jpeg?raw=true)


## 5. Conclusion
The CS amplifier was successfully modeled. By accurately biasing the NMOS in saturation and selecting an appropriate $R_D$, we achieved the target gain while staying well within the $0.4\text{mW}$ power budget.

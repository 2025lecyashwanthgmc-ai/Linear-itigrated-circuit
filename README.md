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
| Supply Voltage | $V_{DD}$ | 1.2 V |
| Max Power Limit | $P$ | $\le 0.4$ mW |
| Load Capacitance | $C_L$ | 0.5 pF |
| Channel Length | $L$ | 180 nm |
| Threshold Voltage | $V_{th}$ | $\approx 0.366$ V |

---

## 3. Theoretical Derivations & Design Steps

### A. DC Operating Point (Q-Point)
To maximize the output signal swing, we target a quiescent drain voltage ($V_{DS}$) at half of the supply voltage:
$$V_{DS} = \frac{V_{DD}}{2} = 0.6 \text{ V}$$

### B. Drain Current Calculation
Using the power constraint $P = V_{DD} \times I_D$:
$$I_D = \frac{0.4 \text{ mW}}{1.2 \text{ V}} = 0.333 \text{ mA}$$
*Selected Design Value:* **$I_D = 0.3 \text{ mA}$** (to provide a 10% safety margin).

### C. Drain Resistor ($R_D$) Selection
$$R_D = \frac{V_{DD} - V_{DS}}{I_D} = \frac{1.2 - 0.6}{0.3 \text{ mA}} = 2 \text{ k}\Omega$$

### D. Small-Signal Voltage Gain ($A_v$)
The gain is defined by the transconductance ($g_m$):
$$A_v = -g_m \times R_D$$
Based on simulation, for a $V_{GS} = 0.6\text{V}$, the expected gain is $\approx 5 \text{ V/V}$ (14 dB).

---

## 4. Simulation Results

### DC Analysis (Operating Point)
The transistor is confirmed to be in the **Saturation Region** because:
* $V_{GS} (0.6V) > V_{th} (0.366V)$
* $V_{DS} (0.6V) > V_{GS} - V_{th} (0.234V)$

### Transient Analysis
A 10mV, 1kHz sine wave was applied. The output shows a peak-to-peak swing of ~50mV, confirming a gain of 5.


### AC Analysis (Frequency Response)
* **Midband Gain:** 14 dB
* **Bandwidth:** The high-frequency cutoff ($f_H$) is influenced by $C_L$.
* **Pole Frequency:** $f_p = \frac{1}{2\pi R_D C_L} \approx 159 \text{ MHz}$.


---

## 5. Conclusion
The CS amplifier was successfully modeled. By accurately biasing the NMOS in saturation and selecting an appropriate $R_D$, we achieved the target gain while staying well within the $0.4\text{mW}$ power budget.

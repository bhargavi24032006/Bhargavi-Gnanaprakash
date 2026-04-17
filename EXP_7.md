# Lab Report: Design and Simulation of an Op-Amp Integrator

## 1. Theory
An **Op-Amp Integrator** is an operational amplifier circuit that performs the mathematical operation of integration. It produces an output voltage proportional to the integral of the input voltage over time. 



In a practical integrator, a feedback resistor $R_f$ is connected in parallel with the feedback capacitor $C_f$. This is necessary to:
* **Limit Low-Frequency Gain:** Without $R_f$, the DC gain is infinite ($1 / \omega C$), causing the op-amp to saturate due to input offset voltages.
* **Stability:** It provides a DC path for the feedback, ensuring the output remains centered and doesn't "drift" to the power supply rails.

---

## 2. Design Requirements

Based on the experimental specifications provided in the manual (Part B):

* **Operating Frequency Range:** $250\text{ Hz}$ to $1\text{ kHz}$

* **Lower Cutoff Frequency ($f_a$):** $250\text{ Hz}$

* **Upper Operating Frequency ($f_b$):** $1\text{ kHz}$

* **Input Voltage ($V_p$):** $1\text{ V}$

* **Supply Voltage ($V_{cc}$):** $\pm 13\text{ V}$

---

## 3. Design Calculations
To ensure the circuit acts as an integrator within the specified range, we use the following design steps:

### Feedback Capacitor ($C_1$)

We select a standard value to simplify the design:

$$C_1 = 0.1\text{ }\mu\text{F}$$

### Feedback Resistor ($R_1$)

Calculated at the lower cutoff frequency ($f_a$) to limit the gain:

$$R_1 = \frac{1}{2 \pi f_a C_1} = \frac{1}{2 \pi \times 250 \times 0.1 \times 10^{-6}} \approx 6366.19\text{ }\Omega$$

### Input Resistor ($R_2$)

Calculated at the upper frequency ($f_b$) where the circuit must perform integration:

$$R_2 = \frac{1}{2 \pi f_b C_1} = \frac{1}{2 \pi \times 1000 \times 0.1 \times 10^{-6}} \approx 1591.55\text{ }\Omega$$

### Compensation Resistor ($R_3$)

To minimize errors caused by input bias currents, we set $R_3$ to the parallel combination of $R_1$ and $R_2$:

$$R_3 = R_1 \parallel R_2 \approx 1273.24\text{ }\Omega$$

---

## 4. Parameters Taken
| Component | Label | Value (Simulated) |
| :--- | :--- | :--- |
| Operational Amplifier | U1 | uA741 |
| Feedback Resistor | R1 | $6366.19\text{ }\Omega$ |
| Input Resistor | R2 | $1591.55\text{ }\Omega$ |
| Compensation Resistor | R3 | $1273.24\text{ }\Omega$ |
| Feedback Capacitor | C1 | $0.1\text{ }\mu\text{F}$ |
| Supply Voltage | V1 / V2 | $+13\text{ V} / -13\text{ V}$ |

---

## Circuits and waveforms

## (a) Sine wave

<img width="951" height="817" alt="a" src="https://github.com/user-attachments/assets/cf2defe3-f4a2-4e73-bda7-cd8c7163b9a7" />

<img width="965" height="820" alt="b" src="https://github.com/user-attachments/assets/6d36777f-e9bc-4d23-bb55-838972b635ee" />

<img width="956" height="824" alt="c" src="https://github.com/user-attachments/assets/23805bb9-3671-43d3-a9df-6765848c8b9e" />


## (b) Square wave

<img width="957" height="823" alt="d" src="https://github.com/user-attachments/assets/747aca8f-285f-4147-bc12-08327546a280" />

<img width="959" height="825" alt="e" src="https://github.com/user-attachments/assets/379b1fe7-1053-4aae-8ebc-0d3be4c3057f" />


## (c) Triangular wave

<img width="953" height="824" alt="f" src="https://github.com/user-attachments/assets/bcc9602b-6734-47d1-acc9-88a74cd9f930" />

<img width="958" height="823" alt="g" src="https://github.com/user-attachments/assets/67c0c5e9-d177-4cea-94b7-eb9690defb3a" />



## 5. Analysis and Waveforms
The circuit was simulated at $1\text{ kHz}$ for three different input types:

### i. Sine Wave Input
* **Behavior:** The integrator produces a $90^\circ$ phase shift (integration of $\sin$ is $-\cos$).
* **Observation:** The output is a sine wave shifted in phase relative to the input.

### ii. Square Wave Input
* **Behavior:** The integral of a constant is a linear ramp.
* **Observation:** The output is a **Triangular wave**. When the input is high, the output ramps down; when the input is low, the output ramps up.

### iii. Triangular Wave Input (Starwave)
* **Behavior:** The integral of a linear ramp is a quadratic (parabolic) function.
* **Observation:** The output is a smoothed wave with **parabolic peaks**, resembling a sine wave but mathematically distinct.
---

## 6. Result
The simulation results confirm:
1. **AC Analysis:** The Bode plot shows the expected $-20\text{ dB/decade}$ slope beginning after the $250\text{ Hz}$ corner frequency.
2. **Transient Analysis:** The circuit correctly transforms input shapes into their integral counterparts.
3. **Clipping:** The output remains within the $\pm 13\text{ V}$ range, avoiding saturation.

---


## 7. Inference
1. **Low Pass Filter:** The integrator inherently acts as a low-pass filter, attenuating high-frequency noise while integrating the desired signal.
2. **Frequency Sensitivity:** The quality of integration improves as the frequency increases toward $f_b$, as the capacitive reactance becomes much smaller than the feedback resistance.
3. **Frequency Dependence:** The circuit works best as an integrator when the signal frequency $f$ is much higher than $f_a$.
4. **Phase Inversion:** Because the signal is applied to the inverting terminal, the output is mathematically the negative integral of the input.
5. **Initial Transients:** As seen in the graphs, there is an initial DC offset settling period before the waveform stabilizes around the zero-axis.
6. **DC Offset:** The small initial drift seen in the simulation graphs is the transient response as the capacitor reaches its steady-state DC operating point.

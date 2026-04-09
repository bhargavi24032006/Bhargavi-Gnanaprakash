# Op-Amp Circuit Design and Simulation Report

## Project Overview

## 1. Introduction and Specifications
This report documents the design and LTspice simulation of operational amplifier circuits to perform specific arithmetic operations on three input signals:

### Input Parameters:
* **$x_1(t) = -1V$** (DC Source)
* **$x_2(t) = 0.5 \sin(2000\pi t)$** (AC Source, $f = 1kHz$, $V_p = 0.5V$)
* **$x_3(t) = +1V$** (DC Source)
* **Supply Rails ($V_{CC}/V_{EE}$)**: $\pm 15V$

---

## 2. **Target Function:** $y_2(t) = 6x_3(t) + 2x_2(t)$

### Circuit Theory: Non-Inverting Summing Amplifier
The design uses a non-inverting summing configuration with two inputs. The general form for the output voltage, based on the provided generic formula, is:

$$V_{out} = \left( 1 + \frac{R_f}{R_1} \right) \left[ \frac{R_b}{R_a + R_b} V_1 + \frac{R_a}{R_a + R_b} V_2 \right]$$

### Design Mapping and Calculations:

1. **Mapping Inputs:** Let $V_1 = x_3(t)$ and $V_2 = x_2(t)$.

2. **Determining Ratios:** By inspecting the bracketed term, we can establish the ratio of contributions.
  
3. From the target equation, the ratio of $x_3$ contribution to $x_2$ contribution is $6:2$ (or $3:1$).

   Matching with the generic formula: $\frac{R_b}{R_a} = \frac{6}{2} \implies R_b = 3R_a$.
   
   * We set $R_a = 10k\Omega$, therefore $R_b = 30k\Omega$.
     
4. **Calculating Voltage divider:** Substituting these values back into the formula:
   
   $$\text{Divider term} = \left[ \frac{30k}{10k + 30k} x_3 + \frac{10k}{10k + 30k} x_2 \right] = [0.75x_3 + 0.25x_2]$$
   
5. **Setting Gain:**

   Target Equation: $V_{out} = 6x_3 + 2x_2 = 8(0.75x_3 + 0.25x_2)$

   This implies we need a gain factor $\left( 1 + \frac{R_f}{R_1} \right) = 8$.

6. **Selecting Feedback Resistors:**
   $1 + \frac{R_f}{R_1} = 8 \implies \frac{R_f}{R_1} = 7 \implies R_f = 7R_1$.
   * Let $R_1 = 10k\Omega$, therefore $R_f = 70k\Omega$.

### Final Selected Components for (b)

* $R_a$ (to $x_2$): $10k\Omega$

* $R_b$ (to $x_3$): $30k\Omega$

* $R_1$: $10k\Omega$

* $R_f$: $70k\Omega$

### Final Output Equation

Substituting the actual input values into the target equation:

$$y_2(t) = 2(-0.5 \sin(2000\pi t)) + 6(1)$$

$$y_2(t) = 6 - 1 \sin(2000\pi t) \text{ Volts}$$

**Waveform Characteristics:**

* **DC Offset**: $6V$
  
* **Amplitude**: $1V$ peak
  
* **Phase**: Negative sine (starts at $6V$ and goes down to $5V$ first).


### Schematic & Simulation


<img width="953" height="855" alt="image" src="https://github.com/user-attachments/assets/86e2100d-9b97-4bf9-9b6d-6aefbd4bc0fd" />

<img width="960" height="858" alt="image" src="https://github.com/user-attachments/assets/f2249b87-f6a3-42a4-92bc-27ac6feacab5" />


---

## 3. **Target Function:** $y_4(t) = \frac{x_1(t) + x_2(t) + x_3(t)}{3}$

### Circuit Theory: Averaging Amplifier (Non-Inverting)
This design utilizes a passive averaging network followed by a voltage follower to prevent loading effects.

### Design Calculations:
1. **Input Resistor Network:** Connect $x_1, x_2,$ and $x_3$ to a common node (non-inverting terminal) through three equal resistors $R$.
   
   Using $R = 10k\Omega$, the voltage at the node $V_p$ is:
   
   $$V_p = \frac{x_1 + x_2 + x_3}{3}$$
3. **Buffer Stage:** To ensure $y_4 = V_p$, the op-amp is configured as a **Voltage Follower** (Gain = 1).

   * Feedback path: Output connected directly to the inverting input.

    * No feedback or ground resistors are required ($R_f = 0, R_g = \infty$).

5. **Final Values:** $R_1 = R_2 = R_3 = 10k\Omega$.

### Final Output Equation

Substituting the actual input values:

$$y_4(t) = \frac{(-1) + (-0.5 \sin(2000\pi t)) + (1)}{3}$$

$$y_4(t) = \frac{-0.5 \sin(2000\pi t)}{3}$$

$$y_4(t) \approx -0.166 \sin(2000\pi t) \text{ Volts}$$

**Waveform Characteristics:**

* **DC Offset**: $0V$ (Inputs $x_1$ and $x_3$ cancel out).

* **Amplitude**: $\approx 166.7mV$ peak.

* **Phase**: Negative sine.

### Schematic & Simulation

<img width="885" height="856" alt="image" src="https://github.com/user-attachments/assets/dde260cb-bcb7-41d6-b847-a28a6db2e48d" />


<img width="995" height="861" alt="image" src="https://github.com/user-attachments/assets/ce3b0314-8278-4fa0-962e-ddb4a6775385" />


<img width="960" height="863" alt="image" src="https://github.com/user-attachments/assets/a8288276-a49e-45a1-bc30-6e93358998e1" />



---

## 4. Discussion of Results
* **y<sub>2</sub>(t):** The waveform shows the signal centered at a $6V$ DC level with a $1V$ peak amplitude (since $2 \times 0.5V = 1V$).
  
* **y<sub>4</sub>(t):** Given $x_1 = -1V$ and $x_3 = +1V$,

  The DC components cancel out:

   $$y_4(t) = \frac{-1 + x_2(t) + 1}{3} = \frac{x_2(t)}{3}$$

   The simulation confirms an AC output with a peak of $\approx 166.67mV$ and $0V$ DC offset.

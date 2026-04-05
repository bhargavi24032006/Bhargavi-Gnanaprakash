# Op-Amp Circuit Design and Analysis

This project involves the design and frequency response analysis of two operational amplifier configurations: a **Non-Inverting Amplifier** and a **Voltage Follower**.

## 1. Design Specifications

| Parameter | Value |
| :--- | :--- |
| **Supply Voltage (Vcc/Vee)** | $\pm 12V$ |
| **Input Voltage ($V_{in(pp)}$)** | $9V$ (Peak-to-Peak) |
| **Input Frequency ($f$)** | $500Hz$ |
| **Op-Amp Model** | Ideal / LM741 (Typical) |

---

## 2. Part A: Non-Inverting Amplifier (Gain $A_v = 6 V/V$)

### A.1 Design & Circuit Description
In a non-inverting amplifier, the input signal is applied to the non-inverting ($+$) terminal. The gain is determined by the feedback network.
- **Load Resistance ($R_L$):** $1k\Omega$
- **Gain Formula:** $A_v = 1 + \frac{R_f}{R_1}$
- **Resistor Calculation:** 
  To achieve $A_v = 6$:
  $6 = 1 + \frac{R_f}{R_1} \implies \frac{R_f}{R_1} = 5$
  *Choosing **$R_1 = 2k\Omega$**, then **$R_f = 10k\Omega$**.*

### A.2 DC Analysis
- **Input DC:** $0V$ (assuming pure AC sine wave).
- **Quiescent Output:** $0V$.
- **Saturation Check:** Max output $V_{out(peak)} = \text{Gain} \times V_{in(peak)}$.
  $V_{in(peak)} = 4.5V$; $V_{out(peak)} = 6 \times 4.5V = 27V$.

  *Note: Since $27V > V_{cc}$ (12V), the output will be **clipped** at approximately $\pm 11V$ to $\pm 12V$. To avoid clipping, $V_{in(pp)}$ should be reduced to $< 4V$.*

### A.3 Transient Analysis ($500Hz$)
- **Input Waveform:** Sine wave, $9V_{pp}$ ($4.5V$ peak).
- **Output Waveform:** In-phase sine wave (clipped at rail voltages).
- **Expected $V_{out}$:** Theoretically $\pm 27V$, practically clipped at $\approx \pm 11.5V$.

### A.4 AC Analysis (Frequency Response)
- **Bandwidth:** $BW = \frac{GBW}{A_v}$. For a typical 741 ($GBW = 1MHz$), $BW \approx 166kHz$.
- **Gain in dB:** $20 \log(6) \approx 15.56 dB$.

---

## 3. Part B: Voltage Follower (Unity Gain)

### B.1 Design & Circuit Description
The voltage follower (buffer) provides unity gain ($A_v = 1$) with high input impedance and low output impedance.
- **Load Resistance ($R_L$):** $360\Omega$
- **Circuit:** Output connected directly to the inverting ($-$) terminal; $V_{in}$ at non-inverting ($+$) terminal.

### B.2 DC & Transient Analysis
- **Gain:** $1 V/V$.
- **Expected $V_{out}$:** $V_{out} = V_{in} = 9V_{pp}$ ($4.5V$ peak).
- **Current Drive:** $I_{out(peak)} = \frac{4.5V}{360\Omega} \approx 12.5mA$.
  *Note: Most standard op-amps (like LM741) can handle up to $\pm 25mA$.*

### B.3 AC Analysis
- **Bandwidth:** Maximum available (equal to $GBW \approx 1MHz$).
- **Gain in dB:** $0 dB$.

---

## 4. Expected Output Values Summary

| Configuration | Theo. Gain | Practical $V_{out(pp)}$ | Phase Shift |
| :--- | :--- | :--- | :--- |
| **Non-Inverting** | $6$ | $\approx 23V$ (Clipped) | $0^{\circ}$ |
| **Voltage Follower**| $1$ | $9V$ | $0^{\circ}$ |

---

## 5. Simulation Graphs (Placeholders)

### Transient Response ($500Hz$)
![Transient Graph](https://placeholder.com)
*Shows $V_{in}$ vs $V_{out}$. Note the clipping in the Non-Inverting stage.*

### AC Frequency Response (Bode Plot)
![Bode Plot](https://placeholder.com)
*Shows flat gain until the cut-off frequency $f_H$.*

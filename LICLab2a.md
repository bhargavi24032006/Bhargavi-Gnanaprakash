### DIFFERENTIAL AMPLIFIER

### CIRCUIT 1

 # Aim:

"Design and analysis of the MOS differential amplifier circuit for the following specifications."

*Drain Supply Voltage (VDD):* 0.9V
* **Source Supply Voltage (VSS):** -0.9V
* **Maximum Power Dissipation (P):** <= 1.5mW
* **Input Common Mode (VinCM):** 0V
* **Output Common Mode (VoCM):** 0V
* **Tail Node Voltage (VP):** -0.7V
* **Load Capacitance (CL):** 10pF
* length :360nm
  εr = 3.9
ε0 = 8.854 × 10⁻¹² F/m
tox = 4.1 × 10⁻⁹ m
μn = 273.809 cm²/Vs
μp = 115.689 cm²/Vs

Circuit diagram:
<img width="1110" height="623" alt="circuit 1 exp4" src="https://github.com/user-attachments/assets/912517e4-d1b5-4c3c-a640-be70858b9273" />

 # 1.DC analysis:

 In the ideal balanced state $$(V_{in1} = V_{in2})$$, the tail current $$I_{SS}$$ (labeled I1 in your schematic) splits equally between the two transistors (M1 and M2).

$$I_{D1} = I_{D2} = \frac{I_{SS}}{2}$$
 
$$I_{SS} = 1.5{mA}$$

$$V_{out(DC)} = V_{DD} - (I_D \cdot R_d)$$

$$0 = o.9-Rd*0.5mA$$

$$Rd = 1.8k$$

# Verification for  circuit:

$$V = 0.9{V}$$

$$ ID =0.461mA$$

$$ RD = 1.8k$$

$$ Vout(DC) = 0$$

 # NMOS width calculation ( for both M1 and M2)

$$Oxide Capacitance (Cox)$$
$$Cox = εr ε0 / tox$$
$$Cox = (3.9 × 8.854 × 10⁻¹²) / (4.1 × 10⁻⁹)$$
$$Cox = 8.42 × 10⁻³ F/m²$$

$$VGS - VTH = 0.7-0.36 = 0.34V$$

  Drain current equation:$$ ID/2 = (1/2) μn Cox (W/L) (VOV)²$$
Rearranging: $$Wn = ( ID L) / (μn Cox (VOV)²$$)
Substitute values: $$Wn = (1x 10^-3 x 480 x 10^-9)/ (273.809 × 10⁻⁴ × 8.42 × 10⁻³ × (0.34)²) Wn$$ ≈ 18 µm

$$Wn = 19.9 µm → Id = 0.5mA$$

# Vicmin and Vincmax calculation:

 ##  Input Common-Mode Range (ICMR) Analysis

The **ICMR** defines the allowable voltage range at the gates where all transistors remain in the **Saturation Region**.

---

### 1. Maximum Input Voltage ($V_{in,max}$)
To prevent $M_1/M_2$ from entering the triode region, the gate voltage must stay below the drain voltage plus one threshold voltage ($V_{th}$):

**Formula:**
$$V_{in,max} = V_{DD} - (I_D \cdot R_d) + V_{th}$$

**Calculation (Assuming $V_{th} \approx 0.36V$):**
* $V_{in,max} = 0.9V - (0.4165mA \cdot 2.16k\Omega) + 0.4V$
* $V_{in,max} = 0.9V - 0.9V + 0.36V$
* **$V_{in,max} = 0.36V$**

---

### 2. Minimum Input Voltage ($V_{in,min}$)
To ensure the tail current source $I_1$ has enough "headroom" ($V_{DS,sat} \approx 0.37V$) to stay active:

**Formula:**
$$V_{in,min} = V_{SS} + V_{DS,sat} + V_{GS}$$

**Calculation (Assuming $V_{GS} \approx 0.7V$):**
* $V_{in,min} = -0.9V + 0.2 - 0.5V$
* **$V_{in,min} = -1.2v$**

---

### 📋 ICMR Summary Table

| Boundary | Condition | Value |
| :--- | :--- | :--- |
| **Upper Limit ($V_{in,max}$)** | Saturation of $M_1, M_2$ | **+0.4V** |
| **Lower Limit ($V_{in,min}$)** | Tail Source Headroom | **-1.26V** |


> For linear amplification, input common-mode signal must stay between **-0.9V and +0.36V**.
><img width="641" height="670" alt="transeient 1" src="https://github.com/user-attachments/assets/5b04c618-dcf1-4cf1-abd4-03b87e0b41e8" />

if we increase the vin values then graph will be clipped( square form)
<img width="628" height="656" alt="clipped 1" src="https://github.com/user-attachments/assets/7f0d1a3a-b006-4dd0-9a8c-42f59f484646" /><img width="1279" height="695" alt="dc exp4 1" src="https://github.com/user-attachments/assets/07da19b2-d1ab-46f4-aabb-832e838bf6c2" />

# Vocm max and vocm min calculation:

VOcmax=VDD = 0.9v

vocmin = VDD-IDRD = 0v



## 📈 Small-Signal Differential Gain ($A_d$) Analysis

The **Differential Gain ($A_d$)** defines how much the difference between the two input signals ($V_{in1} - V_{in2}$) is amplified at the output ($V_{out1} - V_{out2}$).

---

### 1. Fundamental Formula
For a MOSFET differential pair with resistive loads, the gain is given by:

$$A_d = -g_m \cdot R_d$$

Where:
- **$g_m$**: Transconductance of the NMOS transistors ($M_1, M_2$).
- **$R_d$**: Drain resistance ($1.8\text{k}\Omega$).

---

### 2. Calculating Transconductance ($g_m$)
To get an accurate gain, we first find $g_m$. Using the branch current ($I_D = 0.5\text{mA}$):

**Formula:**
$$g_m = \sqrt{2 \mu_n C_{ox} \frac{W}{L} I_D} \quad \text{or} \quad g_m = \frac{2 I_D}{V_{GS} - V_{th}}$$

*Assuming typical 0.18µm parameters ($V_{ov} \approx 0.2\text{V}$):*
- $g_m = \frac{2 \cdot 0.5\text{mA}}{0.34\text{V}} = \mathbf{2.94\text{mS (mA/V)}}$

---

### 3. Final Gain Calculation
Plugging the values into the gain equation:

$$A_d = -(2.94\text{mS}) \cdot (1.8\text{k}\Omega)$$
$$A_d = \mathbf{-5.29\text{ V/V}}$$

**In Decibels (dB):**
$$Gain(dB) = 20 \cdot \log_{10}(5.29) \approx \mathbf{14.46\text{dB}}$$

---

### 📋 Gain Summary Table

| Parameter | Symbol | Estimated Value |
| :--- | :--- | :--- |
| **Transconductance** | $g_m$ | $5\text{mS}$ |
| **Load Resistance** | $R_d$ | $1.8\text{k}\Omega$ |
| **Differential Gain** | $A_d$ | **9 V/V (14.469 dB)** |
| **Output Type** | Differential | $V_{out1} - V_{out2}$ |

# practical gain

Measured peak-to-peak value
            Measured peak-to-peak values:
* **Input Voltage:** $V_{in(p-p)} = 100\text{mV} - (-100\text{mV}) = 200\text{mV}$
* **Output Voltage:** $V_{out(p-p)} = 602\text{mV} - (-602\text{mV}) = 1204\text{mV}$

* AV= voutp-p/vinp-p

* 1204/200 === 6.02

* V(DB) =20 *log(6.02) = 15.59




# vid<root2 Vov

When the differential input voltage V_{id} (the difference between your two inputs $V_2$ and $V_3$) is less than $\sqrt{2} \cdot V_{ov}$ (where $V_{ov}$ is the overdrive voltage $V_{GS} - V_{th}$), the circuit is operating in its Linear Region.

## 📉 Operation for $V_{id} < \sqrt{2}V_{ov}$ (Linear Region)

When the differential input $V_{id}$ is small, both transistors ($M_1$ and $M_2$) remain **ON** and conduct a portion of the tail current. This is the intended operating range for an amplifier.
<img width="641" height="670" alt="transeient 1" src="https://github.com/user-attachments/assets/7c8218f9-dfaf-4aa2-bf37-64e4bd0f1f14" />



---

### 1. Current Steering Behavior
In this range, the tail current $I_{SS}$ (1mA) is shared between both branches. The current in each transistor changes linearly with the input:

- **$I_{D1} \approx \frac{I_{SS}}{2} + \frac{g_m V_{id}}{2}$**
- **$I_{D2} \approx \frac{I_{SS}}{2} - \frac{g_m V_{id}}{2}$**

As $V_{in1}$ increases, $M_1$ takes more of the 1mA current, and $M_2$ takes less, but **neither transistor is cut off yet.**

---

### 2. Output Voltage Effect
Since the currents are changing linearly, the output voltage at $V_{out1}$ and $V_{out2}$ will track the input signal accurately without significant distortion.

**Differential Output Formula:**
$$V_{out1} - V_{out2} = -g_m \cdot R_d \cdot V_{id}$$

**For your circuit:**
* The output will be a **sine wave** (if the input is a sine wave).
* The gain remains constant at approximately **5.29 V/V**.
* The output signal will be "clean" and follow the shape of the input.

---



Beyond this point ($V_{id} > \sqrt{2}V_{ov}$), the amplifier **saturates**. The output will "flat-top" or clip because the current cannot increase further than the 1mA provided by the tail source.

---

### 📋 Operation Summary

| Condition | Transistor Status | Output Behavior |
| :--- | :--- | :--- |
| **$V_{id} < \sqrt{2}V_{ov}$** | Both M1, M2 are **ON** | **Linear Amplification** (No Clipping) |
| **$V_{id} = \sqrt{2}V_{ov}$** | One is maxed, one is at 0 | **Edge of Saturation** |
| **$V_{id} > \sqrt{2}V_{ov}$** | One is **OFF** | **Output Clipping** (Distortion) |

> 
# vid>root2 Vov

## ⚠️ Operation for $V_{id} > \sqrt{2}V_{ov}$ (Current Steering/Clipping)

When the input difference is larger than $\sqrt{2}V_{ov}$, the differential pair can no longer amplify the signal linearly. The tail current is completely "steered" into one of the two transistors.
<img width="628" height="656" alt="clipped 1" src="https://github.com/user-attachments/assets/954e407c-810f-45fc-bf2a-13a0be5e6198" />

---

### 1. Transistor States (The "Switch" Effect)
In this condition:
- **One transistor ($M_1$ or $M_2$)** carries the **entire 1mA** tail current.
- **The other transistor** is completely **OFF** (Cutoff), carrying 0mA.



### 2. Output Voltage Saturation (Clipping)
Since the current in the branches can no longer increase (it is limited by the 1mA tail source), the output voltage reaches its maximum possible "swing" and stays there. This is known as **Clipping**.

**Maximum Output Levels:**
- **$V_{out,min}$**: $V_{DD} - (I_{SS} \cdot R_d) = 0.9V - (1mA \cdot 1.8k\Omega) = \mathbf{0V}$
- **$V_{out,max}$**: $V_{DD} - (0 \cdot R_d) = \mathbf{0.9V}$

The differential output ($V_{out1} - V_{out2}$) will flat-line at $\pm 0.9V$.

---

### 3. Visual Changes in the Output Waveform
If you run a **Transient Analysis (`.tran`)**, you will see the following:

- **Shape Distortion:** A sine wave input will turn into a **Square-like wave** with "flat tops."
- **Gain Drop:** The "Small-Signal Gain" ($A_v$) effectively drops to zero at the peaks because $dV_{out} / dV_{in} = 0$.
- **Harmonic Distortion:** The output will contain high-frequency harmonics because it is no longer a pure sine wave.

---

### 📋 Comparison Table

| Feature | Linear ($V_{id} < \sqrt{2}V_{ov}$) | Saturated ($V_{id} > \sqrt{2}V_{ov}$) |
| :--- | :--- | :--- |
| **Current $I_{D1}, I_{D2}$** | Both transistors share current | One is 1mA, one is 0mA |
| **Output Waveform** | Clean Sine Wave | **Clipped / Flat-topped** |
| **Transconductance** | Constant $g_m$ | $g_m$ drops to **0** |
| **Function** | Linear Amplifier | **Comparator / Switch** |

>
> **Your Simulation:** Since your input $V_2$ and $V_3$ have a 0.9V amplitude, your total $V_{id}$ is **1.8V peak-to-peak**. This is massive compared to a typical $\sqrt{2}V_{ov} \approx 0.3V$. You will see extreme clipping in  LTspice results.
>
> # AC analysis:
><img width="1278" height="725" alt="AC 1  GREEN" src="https://github.com/user-attachments/assets/562d95d9-40b0-4b14-ac3b-6b1b6e9bed78" />


AV = 14.33db

AV-3 =13.33-3= 10.33

FL=0HZ

FH =  7. 21HZ

BW = 7.21

UGB = AV * BW 

UGB =  74.47 

   ######## CIRCUIT 2


<img width="1068" height="647" alt="CIRCUIT2" src="https://github.com/user-attachments/assets/7f53f447-79a4-4fd1-95a8-5acdde94788d" />


"Active load functionality is provided by the $M_3$–$M_4$ PMOS current mirror. $M_3$ serves as the diode-connected reference, while $M_4$ mirrors the current to the opposite branch, achieving a much higher output resistance than possible with standard resistors."

GIVEN PARAMETERS

### Design Specifications

| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| **Supply Voltage (Positive)** | $V_{DD}$ | $+0.9\text{V}$ |
| **Supply Voltage (Negative)** | $V_{SS}$ | $-0.9\text{V}$ |
| **Power Constraint** | $P$ | $\= 1.8\text{mW}$ |
| **Channel Length** | $L_n$ | $480\text{nm}$ |
| **Input Common-Mode Voltage** | $V_{in,CM}$ | $0\text{V}$ |
| **Output Common-Mode Voltage** | $V_{O,CM}$ | $0\text{V}$ |
| **Tail Node Voltage** | $V_p$ | $-0.7\text{V}$ |
| **Load Capacitance** | $C_L$ | $10\text{pF}$ |
| **Threshold Voltage** | $V_T$ | $\approx 0.36\text{V}$ |

### Power  Analysis

The total power consumed by the differential amplifier is calculated using the total voltage swing and the tail current ($I_{SS}$):

$$P = (V_{DD} - V_{SS}) \cdot I_{SS}$$

**1. Total Supply Voltage:**
$$V_{DD} - V_{SS} = 0.9\text{V} - (-0.9\text{V}) = 1.8\text{V}$$

**2. Maximum Allowed Power:**
Given the constraint $P \le 1.8\text{mW}$:
$$1.8\text{V} \cdot I_{SS} \e 1.8 \times 10^{-3}\text{W}$$

**3. Maximum Tail Current:**
$$I_{SS} \= 1\text{mA}$$

### Quiescent Current Distribution

Under zero differential input ($V_{in,diff} = 0$), the tail current splits equally between the two branches of the differential pair:

$$I_{D1} = I_{D2} = \frac{I_{SS}}{2}$$

**Substituting the previously calculated $I_{SS}$:**

$$I_{D1} = I_{D2} = \frac{1\text{mA}}{2}$$



$$I_{D1} = I_{D2} = 0.5\text{mA}$$

### PMOS Operating Conditions

**1. Terminal Voltages**
* **Source ($V_S$):** Connected to $V_{DD} = 0.9V$
* **Drain ($V_D$):** $0V$

---

**2. Source-Drain Voltage Calculation**
The source-drain voltage ($V_{SD}$) is determined by the difference between the source and drain potentials:

$$V_{SD} = V_{DD} - V_{D}$$
$$V_{SD} = 0.9V - 0V$$
$$V_{SD} = 0.9V$$

---

**3. Saturation Condition**
For a PMOS transistor to operate in the **Saturation Region**, the following condition must be satisfied:

$$V_{SD} > V_{OV}$$

> 
> Since $0.9V$ is sufficiently large (typically much greater than the overdrive voltage $V_{OV}$), both PMOS transistors operate in **saturation**.

### NMOS Differential Pair DC Analysis ($M_1, M_2$)


$$V_{G1} = V_{G2} = 0\text{V}$$

**1. Source Node Voltage** From the design specifications, the tail node voltage ($V_p$) is the source voltage for $M_1$ and $M_2$:
$$V_p = V_S = -0.7\text{V}$$

**2. Gate-Source Voltage ($V_{GS}$)** $$V_{GS} = V_G - V_S = 0\text{V} - (-0.7\text{V})$$
$$V_{GS} = 0.7\text{V}$$

**3. Overdrive Voltage ($V_{OV}$)** Using the threshold voltage $V_T \approx 0.36\text{V}$:
$$V_{OV} = V_{GS} - V_T = 0.7\text{V} - 0.36\text{V}$$
$$V_{OV} = 0.34\text{V}$$

**4. Drain-Source Voltage ($V_{DS}$)** Given the output common-mode voltage $V_{O,CM} = 0\text{V}$:
$$V_D = 0\text{V}$$
$$V_{DS} = V_D - V_S = 0\text{V} - (-0.7\text{V})$$
$$V_{DS} = 0.7\text{V}$$

**5. Saturation Condition Check** For saturation, the condition $V_{DS} > V_{OV}$ must be met:
$$0.7\text{V} > 0.34\text{V}$$
> **Conclusion:** Both $M_1$ and $M_2$ are operating correctly in the **saturation region**.
>
> M5(NMOS)
>
VP = VD = -0.7V

VSS = VS =-0.9V

VDS = 0.2V

VDS=> VOV = 0.2V

### Tail Transistor DC Analysis ($M_5$)

The gate-source and gate voltages are calculated based on the required overdrive voltage ($V_{OV}$) and the negative supply rail ($V_{SS}$):

**1. Gate-Source Voltage ($V_{GS}$)** Using the threshold voltage $V_T \approx 0.36\text{V}$ and a design overdrive $V_{OV} = 0.2\text{V}$:
$$V_{GS} = V_T + V_{OV}$$
$$V_{GS} = 0.36\text{V} + 0.2\text{V} = 0.56\text{V}$$

**2. Gate Voltage ($V_G$)** Since the source is connected to the negative supply rail $V_{SS} = -0.9\text{V}$:
$$V_G = V_S + V_{GS}$$
$$V_G = -0.9\text{V} + 0.56\text{V} = -0.34\text{V}$$

IF WE TAKE vg has -0.35v also it will satisify the saturation region


**3. Saturation Condition Check** To ensure the transistor remains in the saturation region to act as a constant current source, the condition $V_{DS} \ge V_{OV}$ must be satisfied:
$$V_{DS} \ge 0.2\text{V}$$

### NMOS Current Source (M5)

The width $W$ for the current source transistor $M_5$ is calculated using the following parameters:

#### 1. Given Parameters
| Parameter | Value |
| :--- | :--- |
| **Drain Current ($I_D$)** | $I_{SS} = 1\text{ mA} = 1 \times 10^{-3}\text{ A}$ |
| **Overdrive Voltage ($V_{OV5}$)** | $0.2\text{ V}$ |
| **Channel Length ($L$)** | $480\text{ nm} = 480 \times 10^{-9}\text{ m}$ |
| **Process Transconductance ($\mu_n C_{ox}$)** | $2.365 \times 10^{-4}\text{ A/V}^2$ |

---

#### 2. Calculation Steps
Substituting the values into the width formula:

$$W = \frac{2 \times (1 \times 10^{-3}) \times (480 \times 10^{-9})}{2.365 \times 10^{-4} \times (0.2)^2}$$

**Step 1: Simplify the Numerator and Square the Overdrive Voltage**
$$W = \frac{960 \times 10^{-12}}{2.365 \times 10^{-4} \times 0.04}$$

**Step 2: Simplify the Denominator**
$$W = \frac{960 \times 10^{-12}}{9.46 \times 10^{-6}}$$


---



### NMOS Differential Pair (M1 and M2)

The width $W$ for the NMOS transistors is calculated using the saturation current formula:

$$W = \frac{2 \cdot I_D \cdot L}{\mu_n C_{ox} (V_{OV})^2}$$

#### 1. Given Parameters
| Parameter | Value |
| :--- | :--- |
| **Drain Current ($I_D$)** | $0.5\text{ mA} = 0.5 \times 10^{-3}\text{ A}$ |
| **Overdrive Voltage ($V_{OV}$)** | $0.34\text{ V}$ |
| **Channel Length ($L$)** | $480\text{ nm} = 480 \times 10^{-9}\text{ m}$ |


---

#### 2. Calculation Steps
Substituting the values into the equation:

$$W = \frac{2 \times (0.5 \times 10^{-3}) \times (480 \times 10^{-9})}{2.365 \times 10^{-4} \times (0.34)^2}$$

**Step 1: Simplify the Numerator and Square the Overdrive Voltage**
$$W = \frac{480 \times 10^{-12}}{2.365 \times 10^{-4} \times 0.1156}$$

**Step 2: Simplify the Denominator**
$$W = \frac{480 \times 10^{-12}}{2.733 \times 10^{-5}}$$

---


>
> ### Theoretical gain
>
> ## Small-Signal Analysis & Differential Gain Calculation

This section evaluates the gain performance of the amplifier by accounting for **Channel Length Modulation ($\lambda$)** and the interaction between the NMOS drivers and PMOS active loads.

---

### 1. Output Resistance Calculation ($r_o$)
To determine the intrinsic output resistance of the MOSFETs, we account for the Early effect using the parameter $\lambda = 0.1\text{ V}^{-1}$.

With a bias current of $I_D = 0.5\text{ mA}$:

$$r_o = \frac{1}{\lambda I_D}$$
$$r_o = \frac{1}{0.1 \times (0.5 \times 10^{-3})}$$
$$r_o = 20\text{ k}\Omega$$

#### Effective Node Resistance ($R_{out}$)
Since the NMOS ($M_1/M_2$) and PMOS ($M_3/M_4$) are in parallel from a small-signal perspective, the total resistance at the output node is:

$$R_{out} = r_{on} \parallel r_{op}$$
$$R_{out} = 20\text{ k}\Omega \parallel 20\text{ k}\Omega$$
$$R_{out} = 10\text{ k}\Omega$$

---

### 2. Transconductance Calculation ($g_m$)
The transconductance represents the sensitivity of the drain current to changes in the gate-source voltage. Using $V_{OV} = 0.24\text{ V}$:

$$g_m = \frac{2 I_D}{V_{OV}}$$
$$g_m = \frac{2 \times 0.5 \times 10^{-3}}{0.24}$$
$$g_m \approx 4.17\text{ mS}$$

---

### 3. Differential Gain Determination ($A_d$)
The total differential gain is the product of the transconductance and the effective output resistance.

#### Linear Gain:
$$A_d = g_m \times R_{out}$$
$$A_d = (4.17 \times 10^{-3}) \times (10 \times 10^3)$$
$$A_d \approx 41.7\text{ V/V}$$

#### Logarithmic Gain (Decibels):
To express the gain in dB:
$$A_d(dB) = 20 \log_{10}(41.7)$$

> **Calculated  Gain: $\approx 32.4\text{ dB}$**
>
> ## Input Common-Mode Range (ICMR) Analysis

The **Input Common-Mode Range (ICMR)** defines the swing limits for the input voltage ($V_{ICM}$) such that all transistors ($M_1$ through $M_5$) remain in the **Saturation Region**. 

---

### 1. Minimum Input Limit ($V_{ICM, min}$)
For the amplifier to function, the tail current source ($M_5$) must stay in saturation, and the input drivers ($M_1, M_2$) must remain biased "ON."

**Constraint:**
The input voltage must be high enough to provide the required Gate-Source voltage ($V_{GS}$) for $M_1$ while maintaining the drain voltage of the tail transistor ($M_5$).

$$V_{ICM(min)} = V_{S1} + V_{THn}$$

**Calculation:**
Given the source voltage $V_{S1} = -0.7V$ and threshold voltage $V_{THn} = 0.36V$:
* $V_{ICM(min)} = -0.7V + 0.36V$
* **$V_{ICM(min)} = -0.34V$**

---

### 2. Maximum Input Limit ($V_{ICM, max}$)
The upper bound is restricted by the requirement that the input transistors ($M_1, M_2$) do not enter the triode region. This happens when the gate voltage rises too close to the drain voltage ($V_D$).

**Constraint:**
To keep the NMOS drivers in saturation, the gate voltage must not exceed the drain voltage by more than one threshold voltage:
$$V_{ICM(max)} = V_{D} + V_{THn}$$

*Note: In this specific load-balanced configuration, we observe the PMOS transition point.*

**Calculation:**
Using the drain node potential $V_D \approx 0V$ and the PMOS threshold $|V_{TP}| \approx 0.39V$:
* $V_{ICM(max)} = 0V + 0.39V$
* **$V_{ICM(max)} = 0.39V$**

---



Input signals outside of this window will cause either the tail current source to collapse (lower bound) or the input transistors to enter triode (upper bound), resulting in a significant drop in gain and CMRR.
>
> ### DC Analysis
>
> <img width="505" height="453" alt="dc circuit 2" src="https://github.com/user-attachments/assets/0d5777de-bddf-4041-9e7a-46e2140d2709" />

Wn = 30.625 µm  and Wn (M5) = 218.7u and Wp = 38.21u→ Id = 0.5mA

### Transient analysis

<img width="1273" height="697" alt="transeient 2 new" src="https://github.com/user-attachments/assets/c6922271-2ad9-41be-b7e3-6028e464bc28" />

# Practical gain 

  Sine wave
Frequency = 1kHz
Amplitude = 5mV (applied differentially)
DC Offset = 0V

   vin(p-p) = 5m - (-5m) = 10m 
   vout ( p-p) = 10.4 -(-8.409)= 18.8409v

   AV = vout(p-0)/vin(p-p)
   AV = 1.8809

   AV (db) = 20 *log(AV)
       = 5.4873

    ### Differential Input Range Analysis

For the differential pair to remain in its linear operating region and maintain proper current steering, the differential input voltage ($V_{id}$) must satisfy the following condition:

$$|V_{id}| < \sqrt{2} V_{OV}$$

---

#### 1. Given Parameters
* **Overdrive Voltage ($V_{OV}$):** $0.24\text{ V}$

#### 2. Calculation of the Input Limit
By substituting the overdrive voltage into the limit formula:

$$\text{Limit} = \sqrt{2} \times V_{OV}$$
$$\text{Limit} \approx 1.414 \times 0.24\text{ V}$$
$$\text{Limit} \approx 0.34\text{ V}$$

---

vid (10mv)< 0.34 v

<img width="1273" height="697" alt="transeient 2 new" src="https://github.com/user-attachments/assets/ab439c57-62f5-4515-87d4-8cf964e947c4" />


Output waveform is sinusoidal(linear)

### Analysis of Signal Clipping and Non-Linearity

This section examines the behavior of the differential pair when the input signal exceeds the theoretical linear operating limits.

#### 1. Theoretical Boundary
The maximum differential input voltage ($V_{id}$) for linear operation is defined by:

$$|V_{id, max}| = \sqrt{2} \cdot V_{OV}$$

Given $V_{OV} = 0.24V$:
$$\sqrt{2} \cdot 0.24V \approx 0.34V$$

---


#### 2. Applied Signal Comparison
The applied differential input voltage ($V_{id}$) is compared against the calculated limit:

* **Applied $|V_{id}|$:** $30V$
* **Linear Limit:** $0.34V$
* 

Since $30V \gg 0.34V$, the condition $|V_{id}| > \sqrt{2}V_{OV}$ is met.

---
<img width="632" height="505" alt="clipped 2" src="https://github.com/user-attachments/assets/6e2e37ca-9f6a-4f9a-9ca4-8e625320b872" />


#### 3. Observation & Conclusion

> **Waveform Distortion:**
> Because the input magnitude is significantly higher than the overdrive-defined limit, the tail current is completely steered into a single branch of the differential pair.
>
> 3#### AC analysis
>
<img width="1249" height="659" alt="ac 2" src="https://github.com/user-attachments/assets/2c16609c-339e-41f2-9b42-584306af91b6" />

### AC Simulation Results: Bandwidth Analysis

The frequency response was evaluated using an AC simulation to determine the mid-band gain and the associated -3 dB cutoff point.

#### 1. Gain Parameters
| Description | Value (dB) |
| :--- | :--- |
| **Mid-band Gain ($A_v$)** | $5.48\text{ dB}$ |
| **$-3\text{ dB}$ Reference Point** | $2.48\text{ dB}$ |

---

#### 2. Calculation of Cutoff Magnitude
To identify the bandwidth or the 3dB frequency ($\omega_H$), we subtract $3\text{ dB}$ from the peak gain:

$$A_{v, -3dB} = A_{v(peak)} - 3\text{ dB}$$
$$A_{v, -3dB} = 5.48\text{ dB} - 3\text{ dB}$$
$$A_{v, -3dB} = 2.48\text{ dB}$$

---

FL = 0 and FH = 3GHZ

 Band width = FH - FL = 3GHz

 ### Unity Gain Bandwidth (UGB)
   = AV*FH
   = 2.48* 3 

   = 7.44GHz
   

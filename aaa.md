# Experiment 04: MOS Differential Amplifier Analysis

## 1. Design Specifications & Given Values
The following parameters are applied across all three designs for a consistent comparison:


| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| Supply Voltage | $V_{DD}$ | $0.9\text{ V}$ |
| Negative Supply | $V_{SS}$ | $-0.9\text{ V}$ |
| Power Dissipation | $P$ | $1.5\text{ mW}$ |
| Channel Length | $L$ | $360\text{ nm}$ |
| Threshold Voltage | $V_{th}$ | $0.3664\text{ V}$ |
| Gate-Source Voltage | $V_{GS}$ | $0.5\text{ V}$ |
| Input Common Mode | $V_{inCM}$ | $0\text{ V}$ |
| Output Common Mode | $V_{OCM}$ | $0\text{ V}$ |
| Load Capacitance | $C_L$ | $10\text{ pF}$ |

---

## 2. Circuit 1: Resistive Load Differential Pair

### Step 1: DC Analysis & Operating Point
**1. Tail Current ($I_{SS}$):**

Calculated from the power budget $P = (V_{DD} - V_{SS}) \cdot I_{SS}$:

$$I_{SS} = \frac{1.5\text{ mW}}{0.9\text{ V} - (-0.9\text{ V})} = \frac{1.5\text{ mA}}{1.8} \approx \mathbf{0.833\text{ mA}}$$

**2. Drain Current ($I_{D1,2}$):**

Assuming perfect symmetry:

$$I_{D1} = I_{D2} = \frac{I_{SS}}{2} = \frac{0.833\text{ mA}}{2} \approx \mathbf{0.4166\text{ mA}}$$

**3. Node Voltage ($V_p$):**

With $V_{inCM} = 0\text{ V}$ and $V_{GS} = 0.5\text{ V}$:

$$V_p = V_{inCM} - V_{GS} = 0\text{ V} - 0.5\text{ V} = \mathbf{-0.5\text{ V}}$$

**4. Drain Resistor ($R_D$):**

To fix $V_{OCM} = 0\text{ V}$ at the output:

$$V_{OCM} = V_{DD} - (I_{D1} \cdot R_D)$$

$$0 = 0.9 - (0.4166\text{ mA} \cdot R_D) \implies R_D = \frac{0.9}{0.4166\text{ mA}} \approx \mathbf{2.16\text{ k}\Omega}$$

**5. Overdrive Voltage ($V_{ov}$):**

$$V_{ov} = V_{GS} - V_{th} = 0.5 - 0.3664 = \mathbf{0.1336\text{ V}}$$


 <img width="495" height="635" alt="DA1c" src="https://github.com/user-attachments/assets/64810d65-2ede-4cd3-8bcc-f6aac7b072d7" />


> ****

### Step 2: Transient Analysis
*   **Linear Region ($V_{id} < \sqrt{2}V_{ov}$):**

     $$\sqrt{2} \cdot 0.1336 \approx \mathbf{0.189\text{ V}}$$

    If $V_{id} < 0.189\text{ V}$, the output is an amplified sine wave.

    <img width="1917" height="858" alt="image" src="https://github.com/user-attachments/assets/19e535d9-c9b7-4ee4-91a3-cc99dd99db09" />


*   **Clipped Region ($V_{id} > 0.189\text{ V}$):** One transistor cuts off, steering all $I_{SS}$ to one branch, causing the output to flatline at $V_{DD}$.

  <img width="1916" height="856" alt="image" src="https://github.com/user-attachments/assets/6a7651ca-2345-4666-a0df-a40e275ac0e3" />


  
> ****

### Step 3: AC Analysis

*   **Transconductance ($g_m$):**
  
    $$g_m = \frac{2 I_D}{V_{ov}} = \frac{0.833\text{ mA}}{0.1336\text{ V}} \approx \mathbf{6.235\text{ mS}}$$
    
*   **Voltage Gain ($A_v$):**
  
    $$A_v = g_m \cdot R_D = 6.235\text{ mS} \times 2.16\text{ k}\Omega \approx \mathbf{13.4676\text{ V/V}}$$
    
    $$A_v = g_m \cdot R_D = 22.585\text{ dB}$$
    
*   **Inference:** Circuit 1 provides high linearity but the gain is limited by the physical size and value of the resistor $R_D$.
  

  <img width="1002" height="471" alt="image" src="https://github.com/user-attachments/assets/66f5b15e-dc50-44cb-b395-670df4e5f717" />


  
---

## 3. Circuit 2: Active Load (Current Mirror Load)

### Step 1: DC Analysis

**1. Tail Current Source ($M_3$):**

$M_3$ is biased to provide $I_{D3} = 0.833\text{ mA}$.

With $V_p = -0.7\text{ V}$

The drain-source voltage is $V_{DS3} = V_p - V_{SS} = 0.2\text{ V}$.

**2. PMOS Active Load ($M_4, M_5$):**

$R_D$ is replaced by PMOS transistors. Since $V_{OCM} = 0\text{ V}$, the PMOS must support $0.4165\text{ mA}$ each.

**3. Differential Gain ($A_v$):**

$$A_v = g_{m1} \cdot (r_{o1} \parallel r_{o4})$$

Since $r_o \gg R_D$, the gain increases significantly.

### Step 2: Transient Analysis

*   **Inference:** The high output resistance ($r_o$) leads to much higher gain but reduces the input swing range. Output swing is restricted by $V_{DS(sat)}$ of the NMOS and PMOS devices.

### Step 3: AC Analysis
*   **Gain ($A_v$):** Typically increases to **~30-45 V/V** due to the active load.
*   **Bandwidth:** Lower than Circuit 1 because $R_{out} \approx (r_{o1} \parallel r_{o4})$ is high, creating a dominant pole at a lower frequency with $C_L = 10\text{ pF}$.

> ****

---

## 4. Circuit 3: CMOS Current Mirror (Differential to Single-Ended)

### Step 1: DC Analysis
**1. Configuration:**
$M_4$ and $M_5$ are a current mirror. This forces $I_{D4}$ to equal $I_{D1}$, which is then mirrored to $M_5$ to combine with $I_{D2}$ at the output node.
**2. Power:**
Tail current $I_{SS}$ remains **$1.154\text{ mA}$** for the same $1.5\text{ mW}$ budget.

### Step 2: Transient Analysis
*   **Inference:** This is the industry standard for Op-Amp input stages. It effectively doubles the transconductance at the output node, providing excellent differential-to-single-ended conversion.

### Step 3: AC Analysis
*   **Gain ($A_v$):**
    $$A_v = g_{m1} \cdot (r_{o2} \parallel r_{o4})$$
    With $V_{GS} = 0.5\text{ V}$ increasing $g_m$, this circuit reaches the **highest gain (>80 V/V)**.
*   **GBP:** Optimized for high-gain analog signal processing.

> ****

---

## 5. Comparison Table (Final Analysis)
*Comparison for $L = 360\text{ nm}$, $V_{th} = 0.3664\text{ V}$, $P = 1.5\text{ mW}$, and $V_{GS} = 0.5\text{ V}$.*


| Parameter | Circuit 1 (Resistive) | Circuit 2 (Active) | Circuit 3 (CMOS Mirror) |
| :--- | :--- | :--- | :--- |
| **Voltage Gain** | ~13.5 V/V (Lowest) | ~40 V/V (Moderate) | >80 V/V (Highest) |
| **Power Consumption** | $1.5\text{ mW}$ | $1.5\text{ mW}$ | $1.5\text{ mW}$ |
| **Area Efficiency** | Low (Large $R_D$) | High | Excellent (All MOS) |
| **Output Swing** | Limited by $R_D$ | Good | Best |
| **Linearity** | Best | Moderate | Narrowest |

---
**Final Inference:**
- **Circuit 1** is best for applications needing high linearity and high speed where area is not a constraint.
- **Circuit 2** provides a balanced trade-off between gain and complexity.
- **Circuit 3** is the most area-efficient and provides the highest gain, making it ideal for the input stage of integrated Operational Amplifiers.



# Experiment 04: MOS Differential Amplifier Analysis (Vss = -0.9V)

## 1. Design Specifications & Given Values
The following parameters are applied across all three designs for a consistent comparison:


| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| Supply Voltage | $V_{DD}$ | $0.9\text{ V}$ |
| Negative Supply | $V_{SS}$ | $-0.9\text{ V}$ |
| Total Voltage ($V_{DD} - V_{SS}$) | $V_{total}$ | $1.8\text{ V}$ |
| Power Dissipation | $P$ | $1.5\text{ mW}$ |
| Channel Length | $L$ | $360\text{ nm}$ |
| Threshold Voltage | $V_{th}$ | $0.3664\text{ V}$ |
| Gate-Source Voltage | $V_{GS}$ | $0.5\text{ V}$ |
| Input Common Mode | $V_{inCM}$ | $0\text{ V}$ |
| Output Common Mode | $V_{OCM}$ | $0\text{ V}$ |
| Load Capacitance | $C_L$ | $10\text{ pF}$ |

---

## 2. Circuit 1: Resistive Load Differential Pair

### Step 1: DC Analysis & Operating Point
**1. Tail Current ($I_{SS}$):**
Calculated from $P = V_{total} \cdot I_{SS}$:
$$I_{SS} = \frac{1.5\text{ mW}}{1.8\text{ V}} \approx \mathbf{0.8333\text{ mA}}$$

**2. Drain Current ($I_{D1,2}$):**
Assuming perfect symmetry:
$$I_{D1} = I_{D2} = \frac{I_{SS}}{2} \approx \mathbf{0.4167\text{ mA}}$$

**3. Node Voltage ($V_p$):**
With $V_{inCM} = 0\text{ V}$ and $V_{GS} = 0.5\text{ V}$:
$$V_p = V_{inCM} - V_{GS} = 0\text{ V} - 0.5\text{ V} = \mathbf{-0.5\text{ V}}$$

**4. Drain Resistor ($R_D$):**
To fix $V_{OCM} = 0\text{ V}$ at the output:
$$R_D = \frac{V_{DD} - V_{OCM}}{I_{D1}} = \frac{0.9 - 0}{0.4167\text{ mA}} \approx \mathbf{2.16\text{ k}\Omega}$$

**5. Overdrive Voltage ($V_{ov}$):**
$$V_{ov} = V_{GS} - V_{th} = 0.5 - 0.3664 = \mathbf{0.1336\text{ V}}$$

> ****

### Step 2: Transient Analysis
*   **Linear Region ($V_{id} < \sqrt{2}V_{ov}$):**
    $$\sqrt{2} \cdot 0.1336 \approx \mathbf{0.189\text{ V}}$$
*   **Inference:** By increasing the negative supply to $-0.9\text{ V}$, the tail current transistor has a $V_{DS}$ of $0.4\text{ V}$ ($V_p - V_{SS} = -0.5 - (-0.9)$), ensuring it stays well within the saturation region for better current stability.

### Step 3: AC Analysis
*   **Transconductance ($g_m$):**
    $$g_m = \frac{2 I_D}{V_{ov}} = \frac{0.8333\text{ mA}}{0.1336\text{ V}} \approx \mathbf{6.24\text{ mS}}$$
*   **Voltage Gain ($A_v$):**
    $$A_v = g_m \cdot R_D = 6.24\text{ mS} \times 2.16\text{ k}\Omega \approx \mathbf{13.48\text{ V/V}}$$

---

## 3. Circuit 2: Active Load (Current Mirror Load)

### Step 1: DC Analysis
**1. Tail Current Source ($M_3$):**
$M_3$ is biased to provide $I_{D3} = 0.8333\text{ mA}$. $V_{DS3} = 0.4\text{ V}$, which provides excellent headroom compared to the previous design.
**2. PMOS Active Load ($M_4, M_5$):**
PMOS loads must support $0.4167\text{ mA}$ each. $R_{out}$ is now effectively $(r_{o1} \parallel r_{o4})$.

### Step 2: Transient Analysis
*   **Inference:** The increased $V_{total}$ allows for a significantly larger output swing before the transistors enter the triode region. The gain remains high due to the active load.

### Step 3: AC Analysis
*   **Gain ($A_v$):** $g_{m1} \cdot (r_{o1} \parallel r_{o4})$. Expect gain to be **~35-50 V/V**.
*   **Bandwidth:** Pole at output remains $\frac{1}{2\pi \cdot R_{out} \cdot C_L}$.

> ****

---

## 4. Circuit 3: CMOS Current Mirror (Differential to Single-Ended)

### Step 1: DC Analysis
**1. Configuration:**
Current mirror $M_4-M_5$ combines currents at the single-ended output node.
**2. Power:**
Tail current $I_{SS}$ is kept at **$0.8333\text{ mA}$** to strictly adhere to the $1.5\text{ mW}$ power budget.

### Step 2: Transient Analysis
*   **Inference:** This circuit utilizes the $1.8\text{ V}$ total supply to maximize the single-ended output voltage swing. The current mirror doubling effect is maintained.

### Step 3: AC Analysis
*   **Gain ($A_v$):**
    $$A_v = g_{m1} \cdot (r_{o2} \parallel r_{o4})$$
    The highest gain circuit, potentially reaching **>90 V/V** with these biasing conditions.

> ****

---

## 5. Comparison Table (Final Analysis)
*Comparison for $L = 360\text{ nm}$, $P = 1.5\text{ mW}$, $V_{GS} = 0.5\text{ V}$, and $V_{SS} = -0.9\text{ V}$.*


| Parameter | Circuit 1 (Resistive) | Circuit 2 (Active) | Circuit 3 (CMOS Mirror) |
| :--- | :--- | :--- | :--- |
| **Tail Current ($I_{SS}$)** | $0.833\text{ mA}$ | $0.833\text{ mA}$ | $0.833\text{ mA}$ |
| **Voltage Gain** | ~13.5 V/V | ~45 V/V | >90 V/V |
| **Headroom ($V_{DS3}$)** | $0.4\text{ V}$ (High) | $0.4\text{ V}$ | $0.4\text{ V}$ |
| **Output Swing** | $2.16\text{ V}$ range | High | Best |
| **Linearity** | Best | Moderate | Narrowest |

---
**Final Inference:**
- **Vss = -0.9V impact:** This change improves the design significantly by providing $400\text{ mV}$ of headroom for the tail current source while reducing power-related heat dissipation by lowering the current.
- **Circuit 1** remains the most linear.
- **Circuit 3** remains the industry standard for high-gain applications like Op-Amps.


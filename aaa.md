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

Calculated from the power budget $$P = (V_{DD} - V_{SS}) \cdot I_{SS}$$:

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

  By graph :

  Gain = 22.1857 dB 

  Bandwidth (Frequency at (Gain-3dB)) = 8.1283MHz

  Unity Gain Bandwidth = 92.138MHz 


  
---

## 3. Circuit 2: Active Load (Current Mirror Load)

### Step 1: DC Analysis

**1. Tail Current Source ($M_3$):**

$M_3$ is biased to provide $I_{D3} = 0.833\text{ mA}$.

With $V_p = -0.7\text{ V}$

The drain-source voltage is $V_{DS3} = V_p - V_{SS} = 0.2\text{ V}$.

**2. PMOS Active Load ($M_4, M_5$):**

$R_D$ is replaced by PMOS transistors. Since $V_{OCM} = 0\text{ V}$, the PMOS must support $0.4165\text{ mA}$ each.

<img width="502" height="751" alt="DA2c" src="https://github.com/user-attachments/assets/1ea12b82-031d-4ea5-afb9-f2035260758c" />


**3. Differential Gain ($A_v$):**

$$A_v = g_{m1} \cdot (r_{o1} \parallel r_{o4})$$

Since $r_o \gg R_D$, the gain increases significantly.

### Step 2: Transient Analysis

 **Linear Region ($V_{id} < \sqrt{2}V_{ov}$):**

   $$\sqrt{2} \cdot 0.1336 \approx \mathbf{0.189\text{ V}}$$

  If $V_{id} < 0.189\text{ V}$, the output is an amplified sine wave.

   <img width="1918" height="860" alt="image" src="https://github.com/user-attachments/assets/a2283f6b-8c49-41db-9ca7-127f560b5550" />


*   **Clipped Region ($V_{id} > 0.189\text{ V}$):** One transistor cuts off, steering all $I_{SS}$ to one branch, causing the output to flatline at $V_{DD}$.

 <img width="1914" height="854" alt="image" src="https://github.com/user-attachments/assets/673e6e75-336b-42a0-b00d-47b18ba0f5dc" />


*   **Inference:** The high output resistance ($r_o$) leads to much higher gain but reduces the input swing range. Output swing is restricted by $V_{DS(sat)}$ of the NMOS and PMOS devices.

  

### Step 3: AC Analysis

<img width="1919" height="858" alt="image" src="https://github.com/user-attachments/assets/10b5c9b8-8905-4633-a4a6-0747ceea0914" />

*   **Gain ($A_v$):** Typically ranging to **~3-4 V/V** due to the active load.

  By graph : Gain = 11.671 dB = 3.833 V/V
  
*   **Bandwidth:** Lower than Circuit 1 because $R_{out} \approx (r_{o1} \parallel r_{o4})$ is high, creating a dominant pole at a lower frequency with $C_L = 10\text{ pF}$.

  Bandwidth (frequency at (Gain -3dB)) = 26.813 MHz

  Unity Gain Bandwidth = 87.908 MHz 

> ****

---

## 4. Circuit 3: CMOS Current Mirror (Differential to Single-Ended)

### Step 1: DC Analysis
**1. Configuration:**
$M_4$ and $M_5$ are a current mirror. This forces $I_{D4}$ to equal $I_{D1}$, which is then mirrored to $M_5$ to combine with $I_{D2}$ at the output node.
**2. Power:**
Tail current $I_{SS}$ remains **$0.833\text{ mA}$** for the same $1.5\text{ mW}$ budget.

<img width="516" height="827" alt="DA3a" src="https://github.com/user-attachments/assets/ccd79d71-3023-42f4-8861-e4a9a5c3f28b" />


### Step 2: Transient Analysis

 **Linear Region ($V_{id} < \sqrt{2}V_{ov}$):**

   $$\sqrt{2} \cdot 0.1336 \approx \mathbf{0.189\text{ V}}$$

  If $V_{id} < 0.189\text{ V}$, the output is an amplified sine wave.

  <img width="1917" height="858" alt="image" src="https://github.com/user-attachments/assets/88868d34-6c46-40fa-80e6-11710fa1ddbc" />



*   **Clipped Region ($V_{id} > 0.189\text{ V}$):** One transistor cuts off, steering all $I_{SS}$ to one branch, causing the output to flatline at $V_{DD}$.
  

 <img width="1919" height="860" alt="image" src="https://github.com/user-attachments/assets/3dbd0986-63f4-4219-b063-23c8477ee4ae" />



*   **Inference:** This is the industry standard for Op-Amp input stages. It effectively doubles the transconductance at the output node, providing excellent differential-to-single-ended conversion.

### Step 3: AC Analysis

*   **Gain ($A_v$):**
  
    $$A_v = g_{m1} \cdot (r_{o2} \parallel r_{o4})$$
    
    With $V_{GS} = 0.5\text{ V}$ increasing $g_m$, this circuit reaches the **highest gain (>70 V/V)**.
    
<img width="1919" height="860" alt="image" src="https://github.com/user-attachments/assets/9d98a3bd-8b8a-406d-98c6-4648e42e5693" />

    
*   **GBP:** Optimized for high-gain analog signal processing.

    By graph :

  Gain = 37.092347 dB = 71.5512 V/V

  Bandwidth (Frequency at (Gain-3dB)) = 1.429 MHz

  Unity Gain Bandwidth = 91.354 MHz 


> ****

---

## 5. Comparison Table (Final Analysis)
*Comparison for $$L = 360\text{ nm}$$, $$V_{th} = 0.3664\text{ V}$$, $P = 1.5\text{ mW}$, and $V_{GS} = 0.5\text{ V}$.*


| Parameter | Circuit 1 (Resistive) | Circuit 2 (Active) | Circuit 3 (CMOS Mirror) |
| :--- | :--- | :--- | :--- |
| **Voltage Gain** | ~13.5 V/V (Moderate) | ~4 V/V (Lowest) | >70 V/V (Highest) |
| **Power Consumption** | $1.5\text{ mW}$ | $1.5\text{ mW}$ | $1.5\text{ mW}$ |
| **Area Efficiency** | Low (Large $R_D$) | High | Excellent (All MOS) |
| **Output Swing** | Limited by $R_D$ | Good | Best |
| **Linearity** | Best | Moderate | Narrowest |

---
**Final Inference:**
- **Circuit 1** is best for applications needing high linearity and high speed where area is not a constraint.
- **Circuit 2** provides a balanced trade-off between gain and complexity.
- **Circuit 3** is the most area-efficient and provides the highest gain, making it ideal for the input stage of integrated Operational Amplifiers.






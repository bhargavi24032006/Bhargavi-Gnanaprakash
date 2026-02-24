# **LAB 1**
## CS Amplifier Design & Analysis (180nm Technology)
### Experiment Overview:

A common-source amplifier is a type of FET amplifier where the input signal is applied to the gate, and the output is taken from the drain. The source is typically grounded. It provides high voltage gain and **180-degree phase shift** (inversion) between the input and output. It’s widely used for amplifying weak signals in analog circuits, with the voltage gain determined by the load resistor and the transconductance of the FET.
This experiment involves the design and simulation of a Common Source (CS) Amplifier using an CMOSN transistor in LTspice. The objective is to analyze the amplifier's performance specifically Gain, Bandwidth, and Gain-Bandwidth Product (GBW) under two conditions:

1. Without a Load Capacitor (C<sub>L</sub>)
2. With a Load Capacitor (C<sub>L</sub> = 10pF)

### <u>Key Components and their roles</u>:
1. **R1(Drain Resistor):** Provides the required voltage drop to amplify the signal.
2. **W (Transistor Width):** Affects current ID and transconductance (gm), influencing gain and bandwidth.
3. **V<sub>DD</sub> (Drain Supply Voltage):** Provides DC biasing for the NMOS transistor.
4. **AC Input (SINE source):** The test signal used to analyze circuit response.

### **Circuit diagram:**

<img width="600" height="400" alt="LAB 1 g" src="https://github.com/user-attachments/assets/11fa5f22-ffec-4dd5-8465-82cd591cd64d" />


This report presents the analysis of Q point,Transfer characteristics(DC analysis), Transient analysis, AC analysis of a common-source NMOS amplifier.

The objective of this analysis is to determine the DC biasing conditions, gain using transient analysis and to find frequency response using AC analysis.

## **Component Details:**
The circuit consists of a TSMC 180nm NMOS transistor (CMOSN), a drain resistor and two voltage sources. The drain resistor limits the current through the transistor and affects the small-signal gain. The NMOS transistor operates in saturation region, making it suitable for amplification
**Model:** **CMOSN**

**Technology Node:** 180nm (tsmc018.lib)

**Channel Length:**   180nm

**Channel Width:**   1.53065µm

**Threshold Voltage:**   0.366V

**Resistor:**   4500ohm

**DC Voltage (V<sub>DD</sub>):**   1.8V

**Supply Voltage:**   0.9V

**Amplitude:**   10mV

**Frequency:**   1kHz

**Load capaitance:**  10pF

## Procedure:

1. Create a new folder and name it, copy the tsmc018.lib in the same folder and save the LT spice draft in the same folder and start working on the draft this is done as the .lib has to be included in the draft to access CMOSN features.

2. Start building the circuit and name the mosfet as CMOSN and the length as 180nm and width as 1.5µm initially.

3. **DC Analysis**: Set up the circuit as per the circuit diagram with proper connections. Provide DC voltage of V<sub>DD</sub> = 1.8V and V<sub>GS</sub> = 0.9 V . Go to SPICE directive (.t) option in the tab and edit simulation command, type .op Click on OK and place it anywhere on the draft nd RUN to get the DC operating point 

4. **Transient Analysis:** Apply a sine wave input of V<sub>GS</sub>=0.9V with an amplitude of 10mV and frequency of 1kHz by going to advanced menu in the voltage setting option.go to simulate option in tab ,edit simulation command , click on transient analysis and give the stop time as 5m and click OK. Now Run to visualise the response of the circuit to a time varying signal.

5. **AC Analysis:** Go to Configure Analysis and click on AC analysis and mention the time of sweep as decade , no of points as 10 and frequency as 0.1Hz to 100GHz and click on ok. Now Run to analyze the gain and frequency response of the circuit

6.Repeat with a 10pF load capacitor 

## **Performance Without Load Capacitor (C<sub>L</sub>= 0):**

### **DC Analysis & Q-Point:**

The first step is establishing a stable Operating Point (Q-Point) to ensure the MOSFET remains in the Saturation Region for amplification.

<img width="400" height="400" alt="LAB 1 b" src="https://github.com/user-attachments/assets/7898913a-c640-42d6-abe4-f6a864e2c015" />

For Power dissipation <= 1mW across the resistor, then the current through the resistor is given by:

**Power** <= V x I<sub>D</sub>

**Id** >= Power/Voltage 

**I<sub>D</sub>** >= 1m / 1.8

**I<sub>D</sub>** >= **0.5555 µA**

So let the selected I<sub>D</sub> be 200µA

**Vov = V<sub>GS</sub> - V<sub>th</sub> = 0.9 - 0.366 = 0.534 V**.

As 'L' is 180nm and 'W' is 1.5µm the Id value will be 196.875µA. Keeping the L constant and start varying the width to get the required current I<sub>D</sub> value from the simulation.

| Width     | Current(I<sub>D</sub>) |
|:---------|:---:|
| 1.5µm   | 196.875µA|
| 1.52µm     | 198.916 µA |
| 1.53µm | 199.934µA|
|1.531µm  | 200.036µA |
|1.53056µm. | 200µA|

<img width="400" height="250" alt="LAB 1 a" src="https://github.com/user-attachments/assets/46cd74ae-e34c-4812-8bbc-b1d2259732b8" />

From the simulation result we got the exact current value of **I<sub>D</sub> = 200µA** and **V<sub>out</sub> = 0.9 V**

The load line equation for output is given by 

**V<sub>out</sub> = V<sub>DD</sub> - (I<sub>D</sub> * R<sub>D</sub>)** which is used to calculate R<sub>D</sub>

   R<sub>D</sub> = (V<sub>DD</sub> - V<sub>out</sub>) / I<sub>D</sub>

   = (1.8 - 0.9)/200µA

   = 4500 Ω

Therefore **R<sub>D</sub> = 4500 Ω**

The DC operating point analysis confirms that the NMOS transistor operates in the saturation region with I<sub>D</sub>= 200µA.

**V<sub>DS</sub> = V<sub>out</sub> =  1.8 V** (source is grounded)

Vov = V<sub>GS</sub> - V<sub>th</sub> = 0.9 - 0.366 = 0.534V

i.e **V<sub>Ds</sub> > ( V<sub>GS</sub> - V<sub>th</sub>)**

   **V<sub>D</sub> > V<sub>G</sub> - V<sub>th</sub>**

**Theoriticall gain Av:**  

gm = 2I<sub>D</sub> / Vov

gm = (2 x 200µ) / (0.9 - 0.36)

gm = 0.666 mA/V

Av = gm x RD

Av = 0.66 m x 4500

Av = 3

Av = 9.542425dB

 ### **Transient Analysis :**

<img width="800" height="450" alt="LAB 1 c" src="https://github.com/user-attachments/assets/cc3490c6-65a9-4393-a137-e8a16e32165e" />

A sine wave input (10mV peak, 1kHz) was applied to measure time-domain gain.

**Input Peak (Vin,pk):** Input swing of 19.143mV

**Output Peak (Vout,pk):** Output swing of 51.639mV

**Voltage Gain (Av):**  

**Vin(peak−to−peak)/ Vout(peak−to−peak)** = 2.6975

**Gain in dB:** 20log10(2.6975)=8.61922dB ≈ theoritical value

### **AC Analysis & Bandwidth:**

<img width="450" height="400" alt="LAB 1 d" src="https://github.com/user-attachments/assets/d69a7075-7c7b-4cb7-9313-d02dcd9ad495" />

Without a load capacitor, the bandwidth is primarily limited by the internal parasitic capacitances between drain and gate of the MOSFET.

**Mid-band Gain:** 8.61922dB (as seen in the simulation plot).

**Bandwidth (frequency at (Gain - 3dB) ) :** 52.069GHz

**Bandwidth:** The frequency at which the gain drops by 3dB is exceptionally high (in the GHz range) due to the lack of external CL.

## **Performance With Load Capacitor (C<sub>L</sub> = 10pF):**

Adding a 1fF capacitor at the Vout node introduces a dominant pole, which affects high-frequency performance.

<img width="600" height="350" alt="image" src="https://github.com/user-attachments/assets/5f19ed47-2e37-4306-be08-1db0444c3945" />

### **Transient Analysis (With C<sub>L</sub>):**

<img width="900" height="450" alt="LAB 1 f wc" src="https://github.com/user-attachments/assets/c9673e63-575c-43ca-a7b6-2578e865484d" />

The gain remains largely the same at low frequencies (1kHz), as the capacitor acts as an open circuit.

**Observation:** The output signal maintains its 180 phase shift relative to the input.

### **AC Analysis & Bandwidth with C<sub>L</sub> = 10pF :**

<img width="950" height="450" alt="image" src="https://github.com/user-attachments/assets/e3184a48-e6fe-40f9-836b-ae2ec8e08cd1" />

A sine wave input (10mV peak, 1kHz) was applied to measure time-domain gain.

**Input Peak (Vin,pk):** Input swing of 19.14mV

**Output Peak (Vout,pk):** Output swing of 51.431mV

**Voltage Gain (Av):**  

**Vin(peak−to−peak)/ Vout(peak−to−peak)** = 2.68709

**Gain in dB:** 20log10(2.6971) = 8.58566dB ≈ theoritical value

**Bandwidth (frequency at (Gain - 3dB) ) :** 4.007MHz

**Bandwidth:** The frequency at which the gain drops by 3dB is comparitively lower (in the MHz range) due to the presence of external CL.

## Gain-Bandwidth Product (GBW) Bandwidth (f 3dB): With and without C<sub>L</sub>

The Gain-Bandwidth Product (GBW) is significant because it represents the fundamental limit of the amplifier. It shows that there is a constant trade-off: to get more speed (Bandwidth), we must sacrifice Gain, and vice versa. 

The most important thing about GBW is that it is a constant number for a specific design.

1. If you want to make the amplifier twice as loud (double the gain), the circuit will naturally become half as fast (half the bandwidth).

2. If you want it to be super fast, you have to accept a lower gain.

It is the ultimate 'Figure of Merit' for our 180nm NMOS design

**Gain-Bandwidth Product: Calculated as GBW = Gain(linear)×Bandwidth.**

1. Without capacitor:
   
   GBW = Gain(linear) × Bandwidth
   
   GBW = 2.6975 × 52.069GHz
   
   GBW = 140.4561GHz
   
2. With capacitor C<sub>L</sub> = 10pF:
 
   GBW = Gain(linear) × Bandwidth
   
   GBW = 2.68709 × 4.007MHz
   
   GBW = 10.7671MHz

## Inference: 

The simulation results provide several key insights into the behavior of the Common Source (CS) amplifier in 180nm technology:

Operating Point Stability: The precise tuning of the transistor width (W=1.53056μm) to achieve I<sub>D</sub> =200μA and Vout=0.9V confirms that the gain is highly sensitive to device geometry. Setting V out at 
V<sub>DD</sub>/2 successfully maximized the output swing, preventing signal clipping during transient analysis.

The Impact of Capacitive Loading: The most significant observation is the drastic shift in bandwidth. Without an external capacitor, the bandwidth is 52.069 GHz, limited only by internal parasitics. Adding a 10pF load capacitor reduced the bandwidth to 4.007 MHz. This demonstrates that the output node’s RC time constant (τ = R<sub>D</sub> × C<sub>L</sub>) becomes the dominant factor in speed. Adding even a tiny capacitance (10pF) begins to pull the "pole" inward, demonstrating how capacitive loading limits the speed of the amplifier, meaning the amplifier is faster without the capacitor.

Gain-Bandwidth Product (GBW) Trade-off: The calculation shows a massive drop in GBW when the load is added. This infers that while the NMOS is intrinsically capable of high-speed operation (High GBW), real-world performance is bottlenecked by the capacitance of the next stage or interconnects.

Phase Inversion: The transient waveforms confirm a 180-degree phase shift. This occurs because an increase in Gate voltage (V<sub>GS</sub> ) increases Drain current (I<sub>D</sub>), which in turn increases the voltage drop across R1 , pulling Vout downward.

## Result:

The CS amplifier was successfully designed, biased, and analyzed using the TSMC 180nm library. The final performance metrics are summarized below:

| Parameter | Theoretical | ValueSimulated (No C<sub>L</sub>​) | Simulated (C<sub>L</sub> ​= 10pF) |
| :---------| :-----------| :----------------------| :-------------------|
| Drain Current (I<sub>D</sub>) | 200μA | 200μA | 200μA |
| Voltage Gain (Av) | 3.0 (9.54dB) | 2.697 (8.62dB) | 2.697 (8.62dB) |
| 3dB Bandwidth (I<sub>D</sub>) | - | 52.069 GHz | 4.007MHz |
| GBW | - | 140.45 GHz | 10.76MHz |

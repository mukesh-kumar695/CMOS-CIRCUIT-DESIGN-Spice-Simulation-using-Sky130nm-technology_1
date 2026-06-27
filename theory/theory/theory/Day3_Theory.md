Day 3 — CMOS Switching Threshold and Dynamic Simulations
Voltage Transfer Characteristics — SPICE Simulations
L1 SPICE Deck Creation for CMOS Inverter
Now let's simulate the VTC of a CMOS inverter using a SPICE deck — a connectivity information (Netlist) which contains information about components of the CMOS inverter.
Component Connectivity:
M1 is PMOS
M2 is NMOS
![Component connectivity](../n2.jpg)
Component Values:
Next, we define W/L ratios and voltage values. Equal sizing means balanced PMOS and NMOS strength.
![Component values](../n5.jpg)
Identify Nodes:
Nodes are points where two components connect to each other. SPICE runs simulations based on these nodes.
![Identify nodes](../n6.jpg)
Name Nodes:
Naming nodes ensures proper simulation, as we can see them in the model file.
![Name nodes](../n7.jpg)
Writing the SPICE deck:
SPICE syntax for MOSFET → Drain Gate Source Body (DGSB)
![SPICE deck](../n8.jpg)
---
L2 SPICE Simulation for CMOS Inverter
![SPICE simulation](../n9.jpg)
Load Capacitance C_L:
This can be a simple MOSFET, another CMOS inverter, or a logic gate.
![Load cap](../n10.jpg)
To find the VTC, we sweep input voltage and measure output voltage:
Sweep Vin from 0 → Vdd (2.5V) with step size 0.05
![Sweep](../n13.jpg)
Model Files Library:
All information about technological parameters is inside the model files library.
![Model files](../n14.jpg)
Simulations for different W/L ratios:
For Wn/Ln = Wp/Lp = 1.5 (equal sizing):
![Equal sizing VTC](../n18.jpg)
For Wn/Ln = 1.5, Wp/Lp = 2.5 (PMOS width 2.5× NMOS):
![Unequal sizing VTC](../n19.jpg)
![Unequal sizing VTC 2](../n22.jpg)
Observation: When PMOS strength = NMOS strength, the VTC shifts slightly to the left. Increasing PMOS width:
Makes PMOS stronger
Output stays high longer
---
Static Behaviour Evaluation — CMOS Inverter Robustness — Switching Threshold
L1 Switching Threshold, Vm
CMOS logic can be used in logic gate designing and the CMOS inverter is a robust device. Comparing two CMOS inverters with different W/L ratios of PMOS and NMOS:
Shape of VTC is the same
Switching threshold is different — this shows the robustness of the CMOS inverter
![Switching threshold comparison](../a2.jpg)
![Switching threshold comparison 2](../a4.jpg)
We find the Switching Threshold (Vm) in both cases by drawing a 45-degree line.
At Vin = 0 and Vout = Vdd (and vice versa) → No current flows
At Vin = Vout = Vm → Maximum current flows, both transistors enter Saturation
![Vm point](../a6.jpg)
At the operating region Vm:
V_gs >> Vt
Possibility of leakage current as current flows directly from Power to Load
![Leakage](../a7.jpg)
---
L2 Analytical Expression of Vm as a Function of (W/L)n and (W/L)p
Calculating Switching Voltage (Vm) w.r.t width and lengths of NMOS and PMOS. Ignoring Vt since V_gs is far greater:
![Vm derivation](../a8.jpg)
![Vm derivation 2](../a9.jpg)
![Vm derivation 3](../a10.jpg)
![Vm derivation 4](../a13.jpg)
Vm depends on:
Mobility (μn, μp)
Kn', Kp'
(W/L)n and (W/L)p
Vdsat_n, Vdsat_p
---
L3 Analytical Expression of (W/L)n and (W/L)p as a Function of Vm
Calculating W/L of NMOS and PMOS w.r.t Switching Voltage (Vm). We choose W/L such that Vm ≈ Vdd/2 — making CMOS act as a symmetrical inverter.
From current equation: Ids_n = −Ids_p
![W/L derivation](../a.16jpg)
![W/L derivation 2](../a17.jpg)
![W/L derivation 3](../a18.jpg)
![W/L derivation 4](../a19.jpg)
---
L4 Static and Dynamic Simulation of CMOS Inverter
(Refer to lab snapshots in main README for simulation outputs)
---
L5 Static and Dynamic Simulation with Increased PMOS Width
(Refer to lab snapshots in main README for simulation outputs)
---
L6 Applications of CMOS Inverter in Clock Network and STA
The switching threshold and delay of a CMOS inverter directly impact Clock Tree Synthesis (CTS) and Static Timing Analysis (STA). Proper sizing of W/L ratios ensures balanced rise and fall delays in clock networks.

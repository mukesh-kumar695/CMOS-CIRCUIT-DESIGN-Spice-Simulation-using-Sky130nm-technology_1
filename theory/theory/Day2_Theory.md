Day 2 — Velocity Saturation and Basics of CMOS Inverter VTC
SPICE Simulation for Lower Nodes and Velocity Saturation Effect
L1 SPICE Simulation for Lower Nodes
We observed the curve for Id vs Vds for different values of V_gs.
![Id vs Vds](../v2.jpg)
In the above graph:
Left side (Vds = V_gs − Vt) → Linear region
Right side → Saturation region
Bottom → Cut-off region (Device OFF)
This behavior is for long channel devices. At a certain transition point of Vds, the region is not completely saturated nor completely linear.
Now, we take different values of W and L while keeping W/L constant. Ideally Id should remain the same, but practically it does not.
Below is the SPICE deck where only W and L are changed while everything else remains the same:
![SPICE deck W/L](../v3.jpg)
![SPICE deck W/L 2](../v4.jpg)
![SPICE deck W/L 3](../v10.jpg)
---
L2 Drain Current vs Gate Voltage for Long and Short Channel Device
Plot Id at different values of V_gs and Vds:
![Id vs Vgs](../v12.jpg)
Comparing the two simulations:
![Comparison](../v13.jpg)
Observations:
Long channel devices (L = 1.2µm): At Vds = 2.5V → Id has quadratic dependency on V_gs
Short channel devices (L = 0.25µm): For lower Vds → quadratic behaviour; at Vds = 2.5V → Id shows linear behavior due to velocity saturation
For Long Channel Device (L = 1.2µm) — Id vs V_gs sweeping Vds to 2.5V:
![Long channel](../v14.jpg)
For Short Channel Device (L = 0.25µm):
![Short channel](../v24.jpg)
> Any device with L ≤ 0.25µm is a **short channel device**
---
L3 Velocity Saturation at Lower and Higher Electric Fields
For short channel devices, Id vs V_gs shows more linear behaviour as V_gs increases. This is due to the velocity saturation effect.
![Velocity sat](../v24.jpg)
Higher values of V_gs → Linear function of Id
Lower values of V_gs → Quadratic function of Id
Velocity Saturation is a Short Channel Effect that becomes significant at lower technology nodes.
![VS effect](../v25.jpg)
![VS effect 2](../v26.jpg)
For lower nodes, we have 4 regions of operation:
Cut Off
Linear
Saturation
Velocity Saturation ← new region
Velocity Saturation explained:
We know that velocity and electric field are related: v = μE
Low E field: velocity increases linearly
High E field: velocity saturates (due to scattering — mobility decreases)
![V sat physics](../v27.jpg)
![V sat physics 2](../v30.jpg)
![V sat physics 3](../v31.jpg)
Re-deriving Id:
![Id re-derive](../v31.jpg)
![Id re-derive 2](../v32.jpg)
Velocity saturation happens at higher values of V_gs:
![Higher Vgs](../v34.jpg)
---
L4 Velocity Saturation Drain Current Model
Considering large values of V_gs. Let V_gs − Vt = Vgt. For small values of Vds, we neglect the (1 + λVds) term:
![Vdsat model](../v35.jpg)
![Vdsat model 2](../v36.jpg)
> **Vdsat** is a technology parameter — it defines at what voltage the device enters velocity saturation.
Cut-off Region: Id = 0 (Device OFF)
Saturation Region
When Vgt is minimum (Vds is maximum):
![Saturation eq](../v38.jpg)
![Saturation eq 2](../v39.jpg)
Resistive Region
When Vds is minimum:
![Resistive eq](../v41.jpg)
Velocity Saturation Region
When Vdsat is minimum:
![VS eq](../v44.jpg)
![VS eq 2](../v45.jpg)
In the equation, it seems that lowering L (with constant W) should increase Id, but practically it does not:
![Practical note](../v46.jpg)
> **Observation:** The saturation current for lower nodes is **low** instead of high, because velocity saturation tends to saturate the device early, limiting peak current. Peak current of lower nodes is smaller than higher nodes.
---
CMOS Voltage Transfer Characteristics (VTC)
L1 MOSFET as a Switch
From the device point of view, a simple MOSFET acts as a Switch:
![MOSFET switch](../s3.jpg)
![MOSFET switch 2](../s4.jpg)
PMOS — on the top of CMOS — source connected to VDD
NMOS — on the bottom of CMOS — source connected to VSS (ground)
The Load Capacitor C_L at the drain can be connected as input to the next inverter, wire, or logic gate.
Biasing of CMOS inverter:
When |V_gs| < Vt → Device OFF (open switch)
When |V_gs| > Vt → Device ON (closed switch)
Conditions for PMOS:
V_gs_p < −Vt → Turn ON
V_gs_p > −Vt → Turn OFF
Conditions for NMOS:
V_gs_n > +Vt → Turn ON
V_gs_n < +Vt → Turn OFF
---
L2 Introduction to Standard MOS Voltage Current Parameters
By varying Boundary Conditions at Vin = Vdd (high) and Vin = 0 (low), we calculate individual equivalent circuits and merge them to get the VTC.
Let Vdd = 5V:
When Vin = Vdd:
V_gs_n = 5 − 0 = 5V → NMOS ON (closed switch)
V_gs_p = 5 − 5 = 0V → PMOS OFF (open switch)
![Vin=Vdd](../s7.jpg)
When Vin = 0:
V_gs_n = 0 − 0 = 0V → NMOS OFF
V_gs_p = 0 − 5 = −5V → PMOS ON
![Vin=0](../s12.jpg)
Output Capacitor Behaviour:
When Vin = Vdd → C_L discharges through NMOS resistor
When Vin = 0 → C_L charges through PMOS
![Cap behaviour](../s13.jpg)
Naming Convention:
![Naming](../s15.jpg)
Observation:
![Observation](../s16.jpg)
---
L3 PMOS/NMOS Drain Current vs Drain Voltage
Since the direction of current is reversed: Ids_p = −Ids_n
We apply reverse potential to PMOS and get curves for Ids_n vs Vds_n and Ids_p vs Vds_p:
![PMOS NMOS curves](../s18.jpg)
---
L4 Step 1 — Convert PMOS Gate-Source-Voltage to Vin
We have internal voltages (V_gs, Vds, V_gd...) but from a logic block perspective, we only have Vin and Vout. We need to convert every node voltage into a function of these two.
Assume long channel device with Vdd = 2V.
We know: V_gs_p = Vin − Vdd → therefore Vin = V_gs_p + Vdd
Ids_n = −Ids_p
![Step 1](../s21.jpg)
![Step 1 result](../s22.jpg)
---
L5 Step 2 & Step 3 — Convert PMOS and NMOS Drain-Source-Voltage to Vout
Step 2 — Convert Vds_p to Vout
We know: Vds_p = Vout − Vdd → therefore Vout = Vds_p + Vdd
There is a shift of Vdd towards the left-hand side:
![Step 2](../s23.jpg)
Observations:
When Vout = 2V → Vds_p = 0V → current is zero (capacitor discharged)
When Vout = 0V → Vds_p = −2V → finite current exists (charging current)
Load curve for PMOS:
![PMOS load curve](../s25.jpg)
Step 3 — Convert NMOS to Vout
For NMOS:
V_gs_n = Vin
Vds_n = Vout
![Step 3](../s27.jpg)
![Step 3 result](../s28.jpg)
![Step 3 result 2](../s29.jpg)
---
L6 Step 4 — Merge PMOS-NMOS Load Curves and Plot VTC
Superimpose both load curves — the intersection points give the VTC:
![Merge curves](../s30.jpg)
![VTC result](../s31.jpg)
Operating Regions (Vdd = 2V):
Vin	Vout	NMOS	PMOS
0V	2V	Cut-Off	Linear
0.5V	1.5V–2V	Saturation	Linear
1V	0.5V–1.5V	Saturation	Saturation
1.5V	0V–0.5V	Linear	Saturation
2V	0V	Linear	Cut-Off
> The slope gives **high gain** at the sharp transition region — any small change in Vin causes a huge change in Vout.
![VTC final](../VTC.png)

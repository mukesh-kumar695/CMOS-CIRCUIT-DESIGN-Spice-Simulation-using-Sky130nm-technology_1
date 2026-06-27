Day 1 — Basics of NMOS Drain Current (Id) vs Drain-to-Source Voltage (Vds)
Introduction to Circuit Design and SPICE Simulations
L1 Why do we need SPICE Simulations?
A CMOS circuit design has both PMOS and NMOS transistors connected together in a specific fashion to form logic gates such as NAND, NOR, AND, OR, etc. These basic gates are the building blocks of all digital circuits. A standard CMOS inverter is built using a PMOS connected to V_DD and an NMOS connected to V_SS driving a load capacitance (C_L).
![Inverter Circuit](../CMOS-1(30775193327552).jpg)
The above inverter circuit has certain electrical characteristics. To understand its behaviour, we perform SPICE simulations which help us analyze important parameters such as delay, switching behavior, and performance. Based on these results, we can determine the proper W/L (Width/Length) ratio of the transistors.
VTC Circuit and Waveform Plot
![CMOS Inverter VTC Characteristics](../CMOS-2(30775566694972).jpg)
Voltage Transfer Characteristics (VTC): By plotting V_out against V_in, we observe how the circuit switches between PMOS and NMOS.
Operating Regions:
When V_in = 0V → PMOS is in Linear, NMOS is Off (V_out = V_DD = 2V)
When V_in = 1V → both transistors enter Saturation simultaneously
When V_in = 2V → PMOS is Off, NMOS is in Linear (V_out = 0V)
Why do we need SPICE?
Clock Tree Synthesis (CTS), crosstalk, and timing analysis are completely dependent on SPICE. Without SPICE, it would not be possible to calculate delays, and without delay information, physical design and timing verification would not be meaningful.
![Clock Network](../CMOS-4(30775650902025).jpg)
Suppose we perform CTS on a circuit using buffers connected with different capacitive loads at their outputs. By performing SPICE simulation, we get a Delay Table for these buffer cells.
Buffer Trees: Buffering is used across multiple levels (Level 1, Level 2) to maintain a clean clock signal and balance capacitive loads.
Delay Tables (Look-up Tables): In Static Timing Analysis (STA), circuit delays are calculated based on:
Input Slew: The transition speed of the incoming signal
Output Load: The total capacitance (fF) the node needs to drive
![Delay Table](../CMOS-5(30775710287972).jpg)
![Delay Table 2](../CMOS-6(30775811277372).jpg)
---
L2 Introduction to Basic Element in Circuit Design — NMOS
An NMOS is a 4-terminal device composed of Gate (G), Source (S), Drain (D), and Body/Substrate (B), built over a P-substrate with n+ diffusion regions (source and drain). Above the substrate there is a thin oxide layer, and on top of it a metal layer acts as the Gate terminal.
![(30775901979921)](../(30775901979921).jpg)
Threshold Voltage
Threshold voltage (Vt) is a very important parameter in MOSFET operation — all characteristics of the device depend on this value.
At V_gs = 0V:
Source, drain, and body terminals are grounded
P-substrate and n+ doped regions act as reverse-biased PN junction diodes
No channel formation — device remains Off
![Vgs=0](../CMOS-10(30776008616005).jpg)
Applying +ve V_gs > 0:
Positive charge on gate repels holes in substrate and attracts electrons below the gate oxide
This is the beginning of channel formation
![Channel forming](../CMOS-11(30776084500038).jpg)
![Channel forming 2](../CMOS-12(30776129719787).jpg)
---
L3 Strong Inversion and Threshold Voltage
Due to accumulation of negative charges, a Depletion Region forms, depleting the substrate's majority carriers (positive holes). As V_gs increases further:
More positive carriers are repelled
Depletion region width increases
![Depletion](../CMOS-12(30776129719787).jpg)
Inversion Layer: At some point, the semiconductor surface completely converts from p-type to n-type — this is called Strong or Surface Inversion
The gate voltage at which strong inversion happens is called the Threshold Voltage
![Strong Inversion](../CMOS-13(30776190348334).jpg)
What happens if we further increase V_gs > Vt?
Negative charges from n+ region get attracted, opening a conducting channel
However, since there is no drain voltage, current cannot flow
![Channel open](../CMOS-14(30776279997966).jpg)
Now observe what happens when we change the body (substrate) potential. The depletion region between source and body increases due to reverse bias at the source terminal.
![Body effect](../CMOS-15(30776344977812).jpg)
---
L4 Threshold Voltage with Positive Substrate Potential
If we increase V_gs, the depletion region increases in both cases. But with a positive V_sb, some charges from the channel are pulled toward the source:
Results in slower inversion
Increases threshold voltage due to +ve V_sb
![Vsb effect](../CMOS-16(30776429513540).jpg)
![Vsb effect 2](../CMOS-17(30776499522357).jpg)
![Vsb effect 3](../CMOS-18(30776561651865).jpg)
The relation between threshold voltage and substrate bias is given by the parameter Gamma (γ), obtained from the fabrication process.
![Gamma equation](../CMOS-19(30776633170989).jpg)
> **Body Effect Conclusion:** When reverse bias voltage (V_sb) is applied between source and body, the depletion layer width broadens near the source, which directly increases the device threshold voltage (V_th).
---
NMOS Resistive Region and Saturation Region of Operation
L1 Resistive Region of Operation with Small Drain-Source Voltage
As the gate voltage (V_gs) increases:
The width of channel increases
More charge carriers are available for conduction
![Resistive region](../CMOS-21(30776790474539).jpg)
![Resistive region 2](../CMOS-22(30776846132191).jpg)
The induced charge in the channel is proportional to (V_gs - Vt)
Assume: Vds = 0.05V, Vt = 0.45V, V_gs slightly greater than Vt
![Voltage gradient](../CMOS-23(30776913061288).jpg)
Since source is grounded and drain is at some potential, there is a voltage gradient along the channel. The Effective Channel Width is slightly smaller than the actual channel width due to fabrication factors.
![Channel width](../CMOS-24(30776987423290).jpg)
---
L2 Drift Current Theory
The effective channel voltage (V_eff) varies with x:
At x = 0 → V_gs - V(x) = 1V
At x = Vds → V_gs - V(x) = 0.95V
![Drift current](../sky-3(386973625413597).jpg)
The induced charge equation is proportional to the effective channel voltage and depends on position x.
Types of current:
Drift current (dominates due to electric field)
Diffusion current
![Drift current 2](../sky-4(386973653148953).jpg)
To calculate drain current, we consider the top view of the transistor:
![Top view](../sky-5(386973679111348).jpg)
---
L3 Drain Current Model for Linear Region of Operation
Velocity depends on:
Mobility (μ)
Electric field (E)
![Velocity equation](../sky-7(386973715675750).jpg)
By integrating (limits: dV from 0 to Vds, dx from 0 to L):
![Integration](../sky-8(386973733585404).jpg)
![Id linear](../sky-9(386973753458695).jpg)
Technology Parameters:
Oxide Capacitance (Cox)
Width and Length (W/L) ratio
Mobility (μn)
Threshold voltage (Vt)
![Tech params](../sky-10(386973772798949).jpg)
The device behaves as linear when: (V_gs - Vt) ≥ Vds
---
L4 SPICE Conclusion to Resistive Operation
To analyze the impact of V_gs and Vds on drain current, consider different values with condition for linear region: (V_gs - Vt) > Vds
![SPICE conclusion](../sky-11(386973790176363).jpg)
![SPICE conclusion 2](../sky-12(386973828538815).jpg)
Calculating Id for different values of V_gs while sweeping Vds is complex manually, so we use SPICE simulation.
---
L5 Pinch-Off Region Condition
When Vds exceeds (V_gs - Vt), the region of operation is called the Saturation Region.
When V_gs - Vds > Vt → conducting channel exists
![Pinch-off 1](../sky-17(386973910069199).jpg)
When V_gs - Vds = Vt → channel starts disappearing at drain side — beginning of Pinch-off
![Pinch-off 2](../sky-20(386973965146073).jpg)
![Pinch-off 3](../sky-23(386974024666750).jpg)
![Pinch-off 4](../sky-25(386974063189743).jpg)
When V_gs - Vds < Vt → channel has disappeared at drain side → Saturation Region
![Saturation](../sky-24(386974047396548).jpg)
---
L6 Drain Current Model for Saturation Region of Operation
At saturation, the channel voltage is constant (V_gs - Vt), and drain current does not depend on Vds. Replace Vds with (V_gs - Vt):
![Saturation Id](../x21.png)
According to the equation, the MOSFET acts as a perfect current source. But practically:
Increasing Vds also increases the depletion region at drain, reducing effective channel length
This causes a slight increase in current → Channel Length Modulation
![CLM 1](../x22.png)
![CLM 2](../x23.png)
---
Introduction to SPICE
L1 Basic SPICE Setup
![SPICE setup](../sky-27(386974101833700).jpg)
Some parameters are fixed and provided by the foundry — pre-defined, no manual calculation needed.
![SPICE params](../sky-28(386974118249374).jpg)
![SPICE params 2](../sky-29(386974133925966).jpg)
By providing SPICE model parameters and SPICE netlist into the SPICE software, we obtain device characteristics such as Id vs Vds for different V_gs values.
SPICE Netlist defines the MOSFET equivalent circuit for simulation:
![SPICE netlist](../sky-32(386974184789352).jpg)
---
L2 Circuit Description in SPICE Syntax
To write a SPICE netlist:
Define nodes
Assign names to nodes
Write component connections
![SPICE nodes](../sky-33(386974202624791).jpg)
A MOSFET has 4 terminals written in order: D G S B
![MOSFET syntax](../sky-34(386974220741196).jpg)
![MOSFET syntax 2](../sky-35(386974238402619).jpg)
![MOSFET syntax 3](../sky-36(386974257266820).jpg)
![MOSFET syntax 4](../sky-37(386974278015499).jpg)
![MOSFET syntax 5](../sky-38(386974294815899).jpg)
![MOSFET syntax 6](../sky-39(386974311765303).jpg)
![MOSFET syntax 7](../sky-40(386974335407732).jpg)
![MOSFET syntax 8](../sky-41(386974359259653).jpg)
SPICE syntax for a Resistor:
![Resistor syntax](../sky-42(386974370958253).jpg)
![Resistor syntax 2](../sky-43(386974384667844).jpg)
![Resistor syntax 3](../sky-44(386974398454968).jpg)
![Resistor syntax 4](../sky-45(386974420193147).jpg)
SPICE syntax for a Voltage Source:
![Vsource syntax](../sky-46(386974444587193).jpg)
![Vsource syntax 2](../sky-47(386974462009678).jpg)
![Vsource syntax 3](../sky-48(386974480144889).jpg)
![Vsource syntax 4](../sky-49(386974505627060).jpg)
![Vsource syntax 5](../sky-50(386974523962873).jpg)
![Vsource syntax 6](../sky-51(386974542141209).jpg)
![Vsource syntax 7](../sky-52(386974557448142).jpg)
---
L3 Define Technology Parameters
Each MOSFET requires a model file containing technology parameters. The models for the NMOS will be found in the file with a similar attribute name.
![Model file](../sky-53(386974572430679).jpg)
These parameters are defined inside model libraries:
![Model library](../sky-54(386974588670374).jpg)
We include this packaged file in a .mod file and call it in the SPICE netlist:
![Include model](../sky-55(386974609440467).jpg)
![Include model 2](../sky-56(386974630418326).jpg)
In SPICE, lines starting with `*` represent comments:
![Comments](../sky-57(386974649025313).jpg)
![Comments 2](../sky-58(386974673603024).jpg)
To analyze MOSFET behavior, we sweep V_gs and Vds:
![Sweep](../sky-60(386974706706238).jpg)
![Sweep 2](../sky-61(386974722335694).jpg)

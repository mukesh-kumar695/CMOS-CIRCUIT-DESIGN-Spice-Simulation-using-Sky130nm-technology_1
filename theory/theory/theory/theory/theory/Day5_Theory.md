Day 5 — CMOS Power Supply and Device Variation Robustness Evaluation
Static Behaviour Evaluation — CMOS Inverter Robustness — Power Supply Variation
L1 Smart SPICE Simulations for Power Supply Variations
One of the key robustness metrics for a CMOS inverter is how well it performs under varying supply voltages (Vdd). In real-world circuits, Vdd can fluctuate due to IR drop, decoupling capacitor effects, or intentional low-power modes.
Why study supply variation?
Vdd directly affects switching threshold (Vm), noise margins, and delay
As Vdd scales down (lower technology nodes), gain and noise margins are impacted
Understanding this helps design circuits that work reliably across a range of operating voltages
SPICE Simulation Approach:
Simulate VTC for multiple Vdd values (e.g., 0.5V, 1.0V, 1.5V, 1.8V, 2.5V)
Observe how Vm, NM_H, NM_L change with Vdd
Use Sky130 PDK models for realistic results
Key Observation from Simulation:
At lower Vdd, the VTC transition region becomes less sharp → lower gain
At very low Vdd (near Vt), the inverter barely switches → degraded performance
Normalized gain (Vout swing / Vdd) tends to remain reasonable until very low voltages
---
L2 Advantages and Disadvantages of Using Low Supply Voltage
Advantages of Low Vdd:
Lower dynamic power: P_dynamic = α × C × Vdd² × f → power scales quadratically with Vdd
Lower static leakage power (indirectly)
Reduced electric field stress on gate oxide → better reliability
Essential for battery-powered / IoT devices
Disadvantages of Low Vdd:
Reduced noise margin: NM_H and NM_L shrink as Vdd decreases
Increased delay: Drive current reduces → slower charging/discharging of C_L
Reduced gain at the transition region
Increased sensitivity to Vt variations — as Vdd approaches Vt, small Vt changes cause large current variations
Harder timing closure in STA at lower voltages
> **Design Trade-off:** Lower Vdd saves power but compromises speed, noise margin, and robustness. The optimal Vdd is a balance between power and performance requirements.
---
Static Behaviour Evaluation — CMOS Inverter Robustness — Device Variation
L1 Sources of Variation — Etching Process
During CMOS fabrication, various process steps introduce device variations — unintended differences between the designed and actual transistor parameters.
Etching Process Variation:
In lithography + etching, the gate length (L) is patterned using light exposure
Variations in light intensity, focus, and chemical etching rates cause L to vary across the wafer
Effect: If L is smaller than designed → device has shorter channel → higher Id, lower Vt → faster but leakier
Effect: If L is larger than designed → lower Id, higher Vt → slower but less leakage
This is called Critical Dimension (CD) variation and is one of the most significant sources of device mismatch.
---
L2 Sources of Variation — Oxide Thickness
Gate Oxide Thickness (t_ox) Variation:
The gate oxide (SiO₂ or High-K dielectric) is grown to a precisely controlled thickness
Non-uniformities in the oxidation process cause t_ox to vary across the wafer
Effect on Cox: Cox = ε_ox / t_ox → thinner oxide → higher Cox → higher drive current
Effect on Vt: Vt depends on Cox → variation in t_ox directly shifts Vt
Combined Effect of Variations:
Process corners are used to model worst-case and best-case scenarios:
Corner	NMOS	PMOS	Meaning
TT	Typical	Typical	Nominal conditions
FF	Fast	Fast	Both transistors faster than nominal
SS	Slow	Slow	Both transistors slower than nominal
FS	Fast	Slow	NMOS fast, PMOS slow
SF	Slow	Fast	NMOS slow, PMOS fast
---
L3 Smart SPICE Simulation for Device Variations
Simulation Approach:
Simulate the CMOS inverter VTC under different process corners (TT, FF, SS, FS, SF)
Observe the shift in Vm, NM_H, NM_L, and delay across corners
Use Sky130 PDK corner model files
What we observe:
FF corner: Vm shifts slightly, faster switching, potentially reduced noise margin
SS corner: Vm shifts opposite direction, slower switching, larger noise margin range
FS / SF corners: VTC becomes asymmetric — rise and fall delays differ significantly
Design Requirement: A robust design must meet timing and noise margin specifications across all process corners.
---
L4 Conclusion
Summary of CMOS Inverter Robustness:
Parameter	Robust CMOS Inverter Behaviour
Switching Threshold (Vm)	Remains near Vdd/2 across W/L variations
Noise Margin	NM_H ≈ NM_L, both maximize as PMOS width is tuned
Supply Variation	Maintains logic function across a range of Vdd
Device Variation	Acceptable timing and functionality across all process corners
The CMOS inverter's robustness — its ability to work correctly despite variations in supply voltage and manufacturing process — is one of the key reasons CMOS technology dominates modern digital IC design.
---
L5 Sky130 Device Variations Labs
(Refer to lab snapshots in main README for Sky130 device variation simulation outputs)
In the Sky130 technology lab:
SPICE simulations are run under multiple process corners using Sky130 PDK model files
VTC, Vm, noise margins, and delay are measured for each corner
Results confirm the robustness analysis covered in the theory above

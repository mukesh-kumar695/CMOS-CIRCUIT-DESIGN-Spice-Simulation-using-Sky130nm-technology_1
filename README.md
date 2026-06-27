CMOS Circuit Design & SPICE Simulation using Sky130nm Technology
A 5-day hands-on workshop covering CMOS circuit design, SPICE simulations, and Sky130nm PDK.
---
📚 Theory Notes
Day	Topic	Link
Day 1	Basics of NMOS, Threshold Voltage, SPICE Setup	📖 Day 1 Theory
Day 2	Velocity Saturation, CMOS VTC Derivation	📖 Day 2 Theory
Day 3	Switching Threshold, Dynamic Simulations	📖 Day 3 Theory
Day 4	Noise Margin Robustness	📖 Day 4 Theory
Day 5	Power Supply & Device Variation Robustness	📖 Day 5 Theory
---
🔬 Lab Snapshots
Day 1 — NMOS Id vs Vds Simulation
Output: Id vs Vds curves for different Vgs values
![Day 1 Output](day_1_output.jpeg)
Sky130 all.spice file (W and L values in microns)
![Day 1 All SPICE](day_1_allspice.jpeg)
---
Day 2 — Velocity Saturation Simulation
Output: Id vs Vds for different Vgs — showing linear behaviour at high Vgs (short channel)
![Day 2 Output](day_2_output.jpeg)
---
Day 3 — VTC and Transient Analysis
Model description file (W/L ratio of PMOS is 2.33× NMOS, Vin swept 0 to 1.8V)
![Day 3 Model Description](day_3modeldescription.jpeg)
Simulation run in Oracle VirtualBox
![Day 3 Simulation Run](day3_jpeg)
VTC Output — Switching Threshold (Vm) = 0.876V
![Day 3 VTC Output](day3_3.jpeg)
Transient Analysis — Rise and Fall Delay
![Day 3 Transient](day_3_2_transient.jpeg)
> - Rise Delay = 2.484ns − 2.149ns = **0.335ns**
> - Fall Delay = 4.335ns − 4.052ns = **0.284ns**
---
Day 4 — Noise Margin (Sky130 Lab)
<!-- Add your Day 4 lab screenshot below -->
<!-- ![Day 4 Noise Margin Output](your_day4_screenshot.jpeg) -->
Add your Sky130 noise margin simulation screenshot here.
---
Day 5 — Power Supply & Device Variation (Sky130 Lab)
<!-- Add your Day 5 lab screenshots below -->
<!-- ![Day 5 Supply Variation](your_day5_supply.jpeg) -->
<!-- ![Day 5 Device Variation](your_day5_device.jpeg) -->
Add your Sky130 supply variation and device variation simulation screenshots here.
---
🛠 Tools Used
SPICE Simulator: ngspice
Technology PDK: SkyWater Sky130nm
Environment: Oracle VirtualBox (Linux)
---
📁 Repository Structure
```
├── README.md                  ← Lab snapshots (this file)
├── theory/
│   ├── Day1_Theory.md         ← NMOS basics, threshold voltage, SPICE intro
│   ├── Day2_Theory.md         ← Velocity saturation, VTC derivation
│   ├── Day3_Theory.md         ← Switching threshold, dynamic simulations
│   ├── Day4_Theory.md         ← Noise margin theory
│   └── Day5_Theory.md         ← Power supply & device variation theory
├── *.jpg / *.jpeg / *.png     ← All image assets
└── *.spice                    ← SPICE netlist files
```

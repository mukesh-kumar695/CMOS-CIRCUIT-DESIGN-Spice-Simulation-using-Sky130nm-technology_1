Day 4 — CMOS Noise Margin Robustness Evaluation
Static Behaviour Evaluation — CMOS Inverter Robustness — Noise Margin
L1 Introduction to Noise Margin
Noise Margin is a measure of the robustness of a CMOS inverter against noise in digital circuits. It defines how much noise a logic gate can tolerate at its input while still producing the correct output logic level.
In any real digital system, signals are subject to noise (from power supply fluctuations, crosstalk, etc.). The CMOS inverter must correctly interpret noisy signals — Noise Margin quantifies this ability.
Why Noise Margin Matters:
Ensures reliable logic level interpretation even with noisy signals
Critical for multi-stage digital designs where output of one gate drives input of another
Determines the safe operating range of a digital circuit
---
L2 Noise Margin Voltage Parameters
From the VTC (Voltage Transfer Characteristic) curve, four key parameters are defined:
Parameter	Definition
V_OH	Output High Voltage — minimum voltage the gate outputs for logic '1'
V_OL	Output Low Voltage — maximum voltage the gate outputs for logic '0'
V_IH	Input High Voltage — minimum input voltage recognized as logic '1'
V_IL	Input Low Voltage — maximum input voltage recognized as logic '0'
These parameters are found from the VTC where the slope = −1 (i.e., the unity gain points):
V_IL → point on VTC where slope = −1 on the rising side
V_IH → point on VTC where slope = −1 on the falling side
---
L3 Noise Margin Equation and Summary
From the VTC parameters, two noise margins are defined:
Noise Margin High (NM_H):
```
NM_H = V_OH - V_IH
```
→ Ability to tolerate noise when output is HIGH
Noise Margin Low (NM_L):
```
NM_L = V_IL - V_OL
```
→ Ability to tolerate noise when output is LOW
Ideal Case:
NM_H = NM_L = Vdd/2 (symmetrical inverter with Vm = Vdd/2)
Key Insight:
Larger Noise Margin → More robust design
NM_H and NM_L should both be positive and as large as possible
Affected by transistor sizing (W/L ratios), supply voltage, and process variations
---
L4 Noise Margin Variation with Respect to PMOS Width
As PMOS width (Wp) changes relative to NMOS width (Wn):
When Wp = Wn (equal sizing):
VTC is slightly asymmetric (because μn > μp — electron mobility > hole mobility)
NM_H and NM_L are not exactly equal
When Wp ≈ 2.5× Wn:
VTC becomes symmetric
Vm shifts to Vdd/2
NM_H ≈ NM_L → optimal noise margins
When Wp >> Wn:
PMOS becomes much stronger
VTC shifts right
NM_H decreases, NM_L increases → unbalanced
Design Rule: For balanced noise margins and symmetric switching, size PMOS approximately 2–3× the NMOS width (to compensate for lower hole mobility).
---
L5 Sky130 Noise Margin Labs
(Refer to lab snapshots in main README for Sky130 noise margin simulation outputs)
In the Sky130 technology lab:
VTC is plotted using Sky130 PDK models
V_IL and V_IH are extracted from the unity-gain points of the VTC
NM_H and NM_L are calculated from the above parameters
Effect of varying PMOS width on noise margins is observed and plotted

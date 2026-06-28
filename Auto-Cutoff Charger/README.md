# ⚡ Auto Cutoff Battery Charger

> A smart, relay-controlled battery charger with automatic cutoff using an LM358 op-amp comparator — simulated in KiCad/LTSpice with full LED status indication.

---

## 📸 Circuit Overview

<img width="1369" height="376" alt="schematicjpeg" src="https://github.com/user-attachments/assets/66379292-62a5-47b2-85f1-739f0f565a9b" />


## 🔥 What Does It Do?

This circuit charges a battery and **automatically cuts off power** when the battery reaches its target voltage. No more overcharging. No more babysitting. Just plug it in and let the circuit handle it.

| State | Indicator | What's Happening |
|---|---|---|
| 🟢 **Charging** | Green LED ON | Battery voltage below threshold — relay closed, current flowing |
| 🔴 **Charged / Cutoff** | Red LED ON | Battery voltage reached setpoint — relay opens, charging stops |

---

## 🗂️ Schematic States

### Charging ON — Green LED Active

<img width="1264" height="358" alt="Charging On" src="https://github.com/user-attachments/assets/9f444146-1bf3-4732-b448-015f3412024f" />

*Relay RL1 is energized. Q1 (BC547) is saturated. Green LED (D3) is lit. Battery is actively receiving charge current.*

---

### Charging OFF — Red LED Active (Cutoff Triggered)

<img width="1600" height="403" alt="Charging Off" src="https://github.com/user-attachments/assets/3310b3d1-cd58-4a1b-912e-cbd7e8eae2e0" />

*Relay RL1 has opened. Q1 is cut off. Red LED (D2) is lit. Battery has reached target voltage — charging halted.*

---

## 🔧 How It Works — Stage by Stage

### Stage 1: AC Input & Rectification
```
V1 (VSINE) → BR1 (Bridge Rectifier) → C1 (1000µF Filter Cap)
```
- **V1** provides the AC mains simulation (see VSINE config below)
- **BR1** is a full-wave bridge rectifier converting AC to pulsating DC
- **C1 (1000µF)** smooths the ripple into clean DC

---

### Stage 2: Voltage Regulation
```
Rectified DC → U1 (7812 Regulator) → +12V Stable Rail
```
- **U1 (LM7812)** is a 3-terminal linear voltage regulator
- Provides a rock-solid **+12V** supply to the comparator and control circuitry
- The voltmeter probe (RV1 side) confirms the regulated 12V rail

---

### Stage 3: Voltage Sensing & Comparison (The Brain)
```
Battery Voltage → Voltage Divider (R5/R6) → LM358 Comparator (U2:A)
Reference Voltage → RV1 (Potentiometer) → LM358 Non-Inverting Input
```
- **RV1** sets your cutoff threshold (the reference voltage on pin 3 `+`)
- **R5 (10k) + R6 (10k)** form a voltage divider sampling the battery/output voltage feeding pin 2 `−`
- **U2:A (LM358)** compares the two:
  - If battery voltage < setpoint → output HIGH → transistor ON → relay ON → **charging**
  - If battery voltage ≥ setpoint → output LOW → transistor OFF → relay OFF → **cutoff**

---

### Stage 4: Transistor Switch
```
LM358 Output → R1 (1kΩ) → Q1 (BC547 NPN) Base
```
- **R1 (1kΩ)** limits base current into Q1
- **Q1 (BC547)** acts as a switch:
  - Saturated (ON) → drives relay coil
  - Cut off (OFF) → de-energizes relay

---

### Stage 5: Relay & Flyback Protection
```
Q1 Collector → RL1 Coil (12V Relay) + D1 (1N4007 Flyback Diode)
```
- **RL1** is a 12V SPDT relay — its contacts connect/disconnect the charging path
- **D1 (1N4007)** is the flyback/freewheel diode across the relay coil, protecting Q1 from inductive voltage spikes when the relay switches off

---

### Stage 6: LED Status Indicators
```
Relay NO/NC contacts → D2 (Red LED) + D3 (Green LED) via R2/R3 (330Ω)
```
- **D3 (Green)** — "Charging On" — lights when relay is closed and charging is active
- **D2 (Red)** — "Charging Off / Full" — lights when relay opens (cutoff triggered)
- **R2 & R3 (330Ω each)** limit current through the LEDs safely

---

### Stage 7: Battery / Load Simulation
```
V2 (VPULSE) → D4 (1N5408) → Load/Battery
```
- **V2 (VPULSE)** simulates the battery being charged — it ramps from a lower voltage up to the cutoff point, triggering the comparator
- **D4 (1N5408)** is a high-current rectifier diode blocking reverse current into the charger
- **R4** provides a small series resistance for the simulation path

---

## ⚙️ Simulation Source Configurations

### V1 — VSINE (AC Mains Simulation)

<img width="715" height="582" alt="VSINE Configuration" src="https://github.com/user-attachments/assets/4fa10eb1-4490-406d-87ed-04492bcf1c05" />


| Parameter | Value | Notes |
|---|---|---|
| Part Reference | V1 | |
| Part Value | VSINE | Sinusoidal AC source |
| DC Offset | (Default) | 0V DC offset |
| Amplitude | **35V** | Peak voltage (~24.7V RMS — suitable for 12V charging after rectification) |
| Frequency | **50 Hz** | Standard mains frequency |
| Time Delay | (Default) | Starts at t=0 |
| Damping Factor | (Default) | No damping |

> **Why 35V peak?** After full-wave rectification and filtering, the peak ripple is approximately `35V - 1.4V (bridge drop) = 33.6V`. The 7812 regulator then clamps this cleanly to 12V.

---

### V2 — VPULSE (Battery Voltage Simulation)

<img width="712" height="637" alt="VPULSE Configuration" src="https://github.com/user-attachments/assets/93a9c65f-f858-4461-9360-b67461df3505" />


| Parameter | Value | Notes |
|---|---|---|
| Part Reference | V2 | |
| Part Value | VPULSE | Pulsed voltage source |
| Initial Value | **8V** | Simulates discharged/low battery |
| Pulse Value | **12.1V** | Simulates fully charged battery voltage |
| Delay Time | 0 | Starts immediately |
| Rise Time | **8s** | Slow ramp — simulates battery charging up gradually |
| Fall Time | 0.1s | Fast fall back |
| Pulse Width | **5s** | Time at peak voltage |
| Period | **20s** | Full charge/discharge cycle period |

> **What this simulates:** V2 ramps from 8V (dead battery) up to 12.1V (full battery) over 8 seconds. When it crosses the RV1 threshold, the LM358 comparator flips, cutting off the relay. This lets you observe the auto-cutoff behavior in a single simulation run.

---

## 🧩 Bill of Materials

| Reference | Component | Value / Part | Function |
|---|---|---|---|
| V1 | AC Source | VSINE, 35V pk, 50Hz | Mains simulation |
| V2 | Pulse Source | VPULSE, 8→12.1V | Battery simulation |
| BR1 | Bridge Rectifier | BRIDGE | Full-wave rectification |
| C1 | Electrolytic Cap | 1000µF | Ripple filtering |
| U1 | Voltage Regulator | LM7812 | +12V regulated rail |
| U2:A | Op-Amp | LM358 | Voltage comparator |
| RV1 | Potentiometer | 10kΩ | Cutoff voltage setpoint |
| R1 | Resistor | 1kΩ | Q1 base current limiter |
| R2 | Resistor | 330Ω | Red LED current limiter |
| R3 | Resistor | 330Ω | Green LED current limiter |
| R4 | Resistor | (sim) | Series load resistance |
| R5 | Resistor | 10kΩ | Voltage divider (upper) |
| R6 | Resistor | 10kΩ | Voltage divider (lower) |
| Q1 | NPN Transistor | BC547 | Relay driver switch |
| RL1 | Relay | 12V coil | Charging path switch |
| D1 | Rectifier Diode | 1N4007 | Relay flyback protection |
| D2 | LED | Red | "Charging Off / Full" indicator |
| D3 | LED | Green | "Charging On" indicator |
| D4 | Rectifier Diode | 1N5408 | Reverse current block |

---

## 🎛️ Setting the Cutoff Voltage

1. Power up the circuit with a known voltage source on V2
2. Adjust **RV1** until the relay just trips at your desired cutoff voltage (e.g., 12.0V for a sealed lead-acid battery)
3. The system will now automatically cut off at that threshold every charge cycle

> **Tip:** For Li-ion cells, set cutoff at ~4.2V per cell. For 12V lead-acid, ~14.4V is the typical absorption voltage. Scale your voltage divider (R5/R6) and RV1 accordingly.

---

## 📐 Simulation Tips

- Run a **transient simulation** from 0 to 25 seconds to observe the full charge → cutoff cycle
- Probe the LM358 output (pin 1) to watch the comparator flip
- Probe the relay coil node (Q1 collector) to confirm switching
- Watch both LED nodes to verify the indicator logic is correct

---

## 🛡️ Design Notes & Protections

- **Flyback diode (D1)** is mandatory — without it, relay turn-off spikes can destroy Q1
- **D4 (1N5408)** rated for higher current than 1N4007 — good for actual charging currents
- The **LM358** operates on a single supply, making it ideal for this application (output swings to near-ground)
- **BC547** is rated for 100mA collector current — more than sufficient to drive a standard 12V relay coil (~50–80mA)

---


## 📜 License

MIT License — fork it, build it, charge things with it.

---

*Built with Proteus  · Powered by too much tea ☕*

# 🔲 Square Wave Generator of Variable Frequency
## Using NE555 Timer IC — Astable Mode

> ⏱️ *Harnessing the classic NE555 to generate precision variable-frequency square waves — from blinking LEDs to high-speed pulses.*

[![Domain](https://img.shields.io/badge/Domain-Analog%20Electronics-yellow?style=flat-square)]()
[![IC](https://img.shields.io/badge/IC-NE555%20Timer-orange?style=flat-square)]()
[![Mode](https://img.shields.io/badge/Mode-Astable%20Multivibrator-purple?style=flat-square)]()
[![Board](https://img.shields.io/badge/Implementation-Vero%20Board-brown?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

---

## 📌 Objective

Design and simulate a **variable frequency square wave generator** using the **NE555 Timer IC** in astable mode. A potentiometer controls the oscillation frequency in real time, while an LED provides visual confirmation of the output waveform.

---

## 🧩 Components

| Component | Value / Spec | Purpose |
|-----------|-------------|---------|
| `NE555 Timer IC` | DIP-8 | Main IC — generates square wave |
| `Potentiometer R2` | 5 kΩ | Adjusts oscillation frequency |
| `Resistor R1` | 10 kΩ | Controls charging time with R2 |
| `Capacitor C1` | 147 µF (100µF ∥ 47µF) | Main timing capacitor |
| `Control Capacitor` | 0.1 µF | Noise filtering at Pin 5 |
| `LED` | Red | Visual waveform indicator |
| `LED Resistor` | 330 Ω | Current limiting for LED |
| `Diodes` | 1N4148 × 2 | Reverse current prevention |
| `Vero Board` | — | Permanent circuit assembly |
| `DC Power Supply` | 5–12 V | System power |

---

## ⚙️ Working Principle

The NE555 in **astable mode** continuously oscillates without any external trigger:

```
┌─────────────────────────────────────────────────────┐
│               ASTABLE OPERATION CYCLE               │
│                                                     │
│  C1 charges via R1 + R2                             │
│  Voltage rises: 1/3 Vcc → 2/3 Vcc                  │
│         ↓                                           │
│  Output Pin 3 = HIGH  →  LED ON 💡                  │
│         ↓                                           │
│  Voltage hits 2/3 Vcc                               │
│  Internal discharge transistor fires                │
│         ↓                                           │
│  C1 discharges through R2 only                      │
│  Voltage falls: 2/3 Vcc → 1/3 Vcc                  │
│         ↓                                           │
│  Output Pin 3 = LOW  →  LED OFF 🌑                  │
│         ↓                                           │
│  Cycle repeats indefinitely ↺                       │
└─────────────────────────────────────────────────────┘
```

---

## 📐 Frequency Formula & Calculations

**Time Period Formula:**
```
T = 0.693 × (R1 + 2×R2) × C1
```

### Case 1 — Maximum Potentiometer (R2 = 5 kΩ)

```
T = 0.693 × (10,000 + 2×5,000) × 147×10⁻⁶
T = 0.693 × 20,000 × 0.000147
T ≈ 2.038 seconds
```

| | Value |
|-|-------|
| High Time | ~1.02 seconds |
| Low Time | ~1.02 seconds |
| LED Behavior | **Clearly visible blink** |

### Case 2 — Minimum Potentiometer (R2 = 0 Ω)

```
T = 0.693 × 10,000 × 147×10⁻⁶
T ≈ 1.02 seconds
```

| | Value |
|-|-------|
| High Time | ~0.5 seconds |
| Low Time | ~0.5 seconds |
| LED Behavior | **Appears constantly ON** (too fast for eye) |

---

## 💡 Why the LED Appears Constant at Minimum R2

> When R2 → 0 Ω, switching speed exceeds the **human eye's persistence of vision threshold (~50ms)**. The LED is still switching — it just appears continuously lit.

---

## 🔇 Noise Prevention (Pin 5)

A **0.1 µF capacitor** on Pin 5 (Control Voltage) stabilizes the internal comparator reference levels, preventing false triggering from electrical noise.

---

## 📊 Results Summary

| Condition | Frequency | LED Behavior |
|-----------|-----------|-------------|
| R2 = 5 kΩ (max) | ~0.49 Hz | 🟢 Visible slow blink |
| R2 = 2.5 kΩ (mid) | ~0.65 Hz | 🟡 Medium blink |
| R2 = 0 Ω (min) | ~0.98 Hz | 🔴 Appears always ON |

**Simulation confirmed:**
- ✅ Square wave output at Pin 3
- ✅ Charging/discharging waveform across C1
- ✅ Frequency variation through potentiometer
- ✅ LED brightness behavior matches theory

---

## 🚀 Applications

This circuit can be used in:
- 🕐 Clock generation
- 📡 Pulse generation
- 💡 LED drivers
- ⏱️ Timing circuits
- 🔧 Digital system testing

---

## ✅ Conclusion

The variable-frequency square wave generator using the **NE555 timer** was successfully designed, simulated, and implemented on a Vero board. Frequency control through the potentiometer was verified, and the LED behavior matched theoretical calculations at all resistance values.

---

## 🛠️ Tools & Technologies

`NE555 Timer` · `Astable Multivibrator` · `Analog Circuit Design` · `Vero Board` · `Circuit Simulation` · `Oscilloscope Analysis`

---

## 👤 About

| | |
|-|---|
| 👨‍💻 **Student** | Amir Rehman |
| 🏛️ **Institution** | NUST — PNEC, Karachi |
| 🌐 **GitHub** | [@amirrehman19](https://github.com/amirrehman19) |

---

⬅️ *Back to [University Projects Portfolio](../README.md)*

# ⚙️ DC Motor Speed Control System Using Arduino
## Microprocessor Systems (EE-222)

> 🤖 *Precision PWM-based motor control — smooth ramps, step-wise speed patterns, and real-time simulation verification.*

[![University](https://img.shields.io/badge/University-NUST%20PNEC-darkblue?style=flat-square)](https://www.nust.edu.pk)
[![Course](https://img.shields.io/badge/Course-EE--222%20Microprocessor%20Systems-blue?style=flat-square)]()
[![MCU](https://img.shields.io/badge/MCU-Arduino%20Uno-00979D?style=flat-square&logo=arduino)](https://www.arduino.cc)
[![Driver](https://img.shields.io/badge/Driver-L293N%20H--Bridge-red?style=flat-square)]()
[![Simulation](https://img.shields.io/badge/Simulation-Proteus-blueviolet?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

---

## 📌 Project Overview

A **microcontroller-based DC motor speed control system** using **PWM (Pulse Width Modulation)** with an Arduino Uno and L293N motor driver. The system executes two predefined speed patterns simulating real industrial motor control behavior — including smooth acceleration/deceleration and step-wise speed transitions.

> 📍 *Department of Electronics & Power Engineering — Pakistan Navy Engineering College (PNEC), NUST, Karachi*

---

## 🎯 Objectives

- ✅ PWM-based motor speed control
- ✅ Embedded programming using Arduino
- ✅ Implementation of timed speed variation patterns
- ✅ Simulation and hardware verification of motor behavior

---

## 🧩 System Components

| Component | Specification | Qty | Role |
|-----------|--------------|-----|------|
| `Arduino Uno` | ATmega328P, 5V logic, 6× PWM | 1 | Central controller |
| `L293N Motor Driver` | Dual H-Bridge | 1 | Motor interface & power |
| `DC Motor` | 12V, 0.3A, Brushed | 1 | Load / actuator |
| `Power Supply` | 12V Adapter | 1 | Motor power |
| Wires & Resistors | As required | — | Connections |

---

## 🔌 Circuit Pin Connections

| Arduino Pin | Motor Driver Pin | Function |
|-------------|-----------------|---------|
| **D9** | ENA | PWM speed control signal |
| **D13** | IN1 | Motor direction control |
| **D12** | IN2 | Motor direction control |
| **GND** | GND | Common ground reference |
| **5V** | VCC | Logic level supply |

> ⚡ Motor runs on **12V external supply** — L293N safely interfaces the 5V Arduino logic with the 12V motor power domain.

---

## 📋 Speed Patterns

### 🔁 Pattern 1 — Smooth Ramp Up / Ramp Down

```
Speed
100% │                    ▲▲▲▲▲▲▲▲▲▲▲
     │               ▲▲▲▲           ▼▼▼▼
     │          ▲▲▲▲                    ▼▼▼▼
     │     ▲▲▲▲                             ▼▼▼▼
  0% │▲▲▲▲                                      ▼▼▼▼▼▶ OFF
     └────────────────────────────────────────────────▶ Time
          |←── 1.5 min ──→|←──── 1.5 min ────→|
```

- Gradually increase to **maximum speed** over 1.5 minutes
- Gradually decrease to **zero** over next 1.5 minutes
- Motor turns **OFF**

---

### 🔁 Pattern 2 — Step-Wise Speed Control

```
Speed
100% │              ████████████
     │              █           █
 50% │     █████████            █████████
     │     █                             █
 25% │█████                               █████▶ OFF
     └────────────────────────────────────────▶ Time
       |30s |  30s  |   30s   |  30s  | 30s |
```

| Step | Duration | Speed Level |
|------|----------|------------|
| 1 | 30 seconds | 🐢 Slow |
| 2 | 30 seconds | 🚶 Double |
| 3 | 30 seconds | 🏃 Maximum |
| 4 | 30 seconds | 🚶 Halved |
| 5 | 30 seconds | 🐢 Slow → OFF |

---

## 💻 Key Code Concepts

```cpp
// PWM Speed Control
analogWrite(ENA, speed);   // 0–255 maps to 0–100% speed

// Direction Control
digitalWrite(IN1, HIGH);
digitalWrite(IN2, LOW);

// Pattern 1 — Gradual ramp
for (int spd = 0; spd <= 255; spd++) {
    analogWrite(ENA, spd);
    delay(352); // ~1.5 min total ramp
}

// Pattern 2 — Step-wise
int steps[] = {64, 128, 255, 128, 64};
for (int i = 0; i < 5; i++) {
    analogWrite(ENA, steps[i]);
    delay(30000); // 30 seconds each
}
```

---

## 🛠️ Software Tools

| Tool | Purpose |
|------|---------|
| `Arduino IDE` | Programming & code upload |
| `Proteus` | Circuit simulation & pattern verification |
| `Serial Monitor` | Real-time speed value debugging |

---

## ⚠️ Engineering Considerations

| Challenge | Solution Applied |
|-----------|----------------|
| ⏱️ Timing Precision | `delay()` for basic; `millis()` for non-blocking future use |
| ⚡ Voltage Mismatch | L293N bridges 5V logic ↔ 12V motor safely |
| 🔧 Speed Resolution | `analogWrite()` gives 256 PWM levels (0–255) |
| 🧪 Pre-build Testing | Proteus simulation validated both patterns before hardware |

---

## 📊 Simulation Results

**Pattern 1:**
- ✅ Smooth speed ramp-up over 1.5 minutes confirmed
- ✅ Smooth ramp-down to zero confirmed
- ✅ Clean motor stop at end of cycle

**Pattern 2:**
- ✅ Step-wise speed changes verified at correct 30s intervals
- ✅ Speed doubling/halving confirmed at each step
- ✅ Final motor OFF state verified

---

## 🚀 Future Applications

This system can be extended for:
- 🤖 Robotics & automation
- 🏭 Conveyor belt systems
- 🔧 Automated machinery
- 🌀 Smart fan / pump controllers
- 🚗 RC vehicle motor control

---

## ✅ Conclusion

The Arduino-based DC motor speed control system **successfully demonstrated both speed patterns** using PWM techniques. Simulation results confirmed correct timing, speed transitions, and motor behavior — validating the embedded design before hardware implementation.

> *"From microcontroller pulse to motor revolution — embedded control in action."*

---

## 🛠️ Tools & Technologies

`Arduino IDE` · `Proteus Simulation` · `PWM Control` · `L293N H-Bridge` · `ATmega328P` · `Embedded C` · `DC Motor Control` · `Serial Monitor`

---

## 👤 About

| | |
|-|---|
| 👨‍💻 **Student** | Amir Rehman |
| 🏛️ **Institution** | NUST — PNEC, Karachi |
| 📘 **Course** | EE-222 Microprocessor Systems |
| 🌐 **GitHub** | [@amirrehman19](https://github.com/amirrehman19) |

---

⬅️ *Back to [University Projects Portfolio](../README.md)*

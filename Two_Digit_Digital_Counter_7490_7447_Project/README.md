# 🔢 Two-Digit Digital Counter
## Using 7490 & 7447 ICs — Count 00 to 99

> 🔟 *From push-button to 7-segment display — a complete BCD counting system built from classic digital logic ICs.*

[![Domain](https://img.shields.io/badge/Domain-Digital%20Electronics-blue?style=flat-square)]()
[![ICs](https://img.shields.io/badge/ICs-7490%20%26%207447-darkblue?style=flat-square)]()
[![Range](https://img.shields.io/badge/Count%20Range-00%20→%2099-green?style=flat-square)]()
[![Display](https://img.shields.io/badge/Display-7--Segment%20Common%20Anode-orange?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

---

## 📌 Project Overview

Design and implementation of a **two-digit digital counter** that counts from **00 to 99** using BCD decade counters, decoder ICs, and 7-segment displays. Each press of a push-button increments the count by one, and the circuit **automatically resets to 00** after reaching 99.

This project illustrates core digital electronics concepts including binary-coded decimal counting, IC cascading, decoder operation, and display interfacing.

---

## 🧩 Key ICs & Their Roles

### 7490 — BCD Decade Counter

| Feature | Detail |
|---------|--------|
| Count Range | 0 → 9 (auto-reset) |
| Output | 4-bit BCD (0000 → 1001) |
| Cascading | Carry output feeds next counter |
| Usage in Circuit | 2× — one for units, one for tens |

### 7447 — BCD to 7-Segment Decoder

| Feature | Detail |
|---------|--------|
| Input | 4-bit BCD from 7490 |
| Output | 7-segment drive signals |
| Display Type | Common-Anode (active LOW) |
| Extra Pins | LT (Lamp Test), BI (Blanking Input) |

---

## ⚙️ Circuit Operation

```
┌──────────────────────────────────────────────────────────┐
│                 COUNTER OPERATION FLOW                   │
│                                                          │
│  🔘 Push Button Press                                    │
│          ↓                                               │
│     Clock Pulse Generated                               │
│          ↓                                               │
│  ┌───────────────────┐    ┌───────────────────┐         │
│  │  7490 Counter #1  │    │  7490 Counter #2  │         │
│  │   (Units Digit)   │───▶│   (Tens Digit)    │         │
│  │    0 → 9 → 0      │    │    0 → 9 → 0      │         │
│  └────────┬──────────┘    └────────┬──────────┘         │
│           ↓                        ↓                    │
│  ┌────────────────┐      ┌────────────────┐             │
│  │  7447 Decoder  │      │  7447 Decoder  │             │
│  │  BCD → 7-Seg   │      │  BCD → 7-Seg   │             │
│  └────────┬───────┘      └────────┬───────┘             │
│           ↓                       ↓                     │
│     ┌──────────┐           ┌──────────┐                 │
│     │ Display 1│           │ Display 2│                 │
│     │  (Units) │           │  (Tens)  │                 │
│     └──────────┘           └──────────┘                 │
│                                                          │
│           Shows:  [ 0 0 ] → [ 9 9 ] → [ 0 0 ]          │
└──────────────────────────────────────────────────────────┘
```

---

## 📟 7-Segment Display Specs

| Parameter | Detail |
|-----------|--------|
| Display Type | Common-Anode |
| Segments | 7 LEDs per digit |
| Current Range | **12 mA – 20 mA** |
| Current Limiting | Resistor on each segment |
| Digits Used | 2 (Units + Tens) |

---

## 🔘 Push-Button Clock Input

| Action | Result |
|--------|--------|
| Button Press | Generates one clock pulse |
| Each Pulse | Increments counter by 1 |
| After 99 | Auto-resets to 00 |

---

## 🔄 Auto-Reset Logic

```
Units Counter: 0→1→2→3→4→5→6→7→8→9→0 (carry out)
                                          ↓
                              Tens Counter increments
                              
Tens Counter:  0→1→2→3→4→5→6→7→8→9→0 (full reset)
```

When both counters reset → Display returns to **00** ✅

---

## 📏 Expandability

> The modular design makes expansion trivially simple:

| Digits | Counter ICs | Decoder ICs | Range |
|--------|------------|-------------|-------|
| 2 | 2× 7490 | 2× 7447 | 00–99 |
| 3 | 3× 7490 | 3× 7447 | 000–999 |
| 4 | 4× 7490 | 4× 7447 | 0000–9999 |

Simply connect the **carry output** of one 7490 to the **clock input** of the next!

---

## 🧪 Simulation & Hardware

**Simulation verified:**
- ✅ Correct counting sequence (00 → 99 → 00)
- ✅ Accurate BCD decoding on both displays
- ✅ Proper counter transition timing
- ✅ Auto-reset functionality

**Hardware implementation using:**
- 2× 7490 ICs + 2× 7447 ICs
- 2× Common-anode 7-segment displays
- Current-limiting resistors
- Push-button switch
- Breadboard / PCB

---

## ✅ Conclusion

This project successfully demonstrates a **modular two-digit BCD counter** using classic TTL digital ICs. It reinforces fundamental digital electronics principles including decade counting, BCD decoding, display interfacing, and cascaded counter design.

> *"Classic digital logic — simple building blocks creating powerful counting systems."*

---

## 🛠️ Tools & Technologies

`7490 BCD Counter` · `7447 Decoder` · `7-Segment Display` · `TTL Logic ICs` · `Digital Circuit Simulation` · `Breadboard Implementation`

---

## 👤 About

| | |
|-|---|
| 👨‍💻 **Student** | Amir Rehman |
| 🏛️ **Institution** | NUST — PNEC, Karachi |
| 🌐 **GitHub** | [@amirrehman19](https://github.com/amirrehman19) |

---

⬅️ *Back to [University Projects Portfolio](../README.md)*

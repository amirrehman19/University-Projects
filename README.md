# 🎓 University Projects Portfolio
### Electronics & Embedded Systems Engineering

> 📚 *A collection of academic projects covering digital electronics, signal processing, embedded systems, biomedical engineering, and PCB design.*

[![University](https://img.shields.io/badge/University-NUST%20PNEC-darkblue?style=flat-square)](https://www.nust.edu.pk)
[![Department](https://img.shields.io/badge/Department-Electronics%20%26%20Power%20Engineering-blue?style=flat-square)]()
[![GitHub](https://img.shields.io/badge/GitHub-amirrehman19-black?style=flat-square&logo=github)](https://github.com/amirrehman19)
[![Platform](https://img.shields.io/badge/Platform-Upwork-14a800?style=flat-square&logo=upwork)](https://www.upwork.com)
[![Status](https://img.shields.io/badge/All%20Projects-Completed-success?style=flat-square)]()

---

## 📁 Projects Index

| # | Project | Domain | Tools |
|---|---------|--------|-------|
| 1 | [🔊 Noise Reduction in Audio Signal Using Digital Filtering](#-project-1--noise-reduction-in-audio-signal-using-digital-filtering) | Signal Processing | MATLAB |
| 2 | [❤️ ECG Front-End Design](#%EF%B8%8F-project-2--ecg-front-end-design) | Biomedical Electronics | Circuit Design |
| 3 | [🔲 Square Wave Generator Using NE555 Timer](#-project-3--square-wave-generator-using-ne555-timer) | Analog Electronics | Vero Board |
| 4 | [🔢 Two-Digit Digital Counter Using 7490 & 7447](#-project-4--two-digit-digital-counter-using-7490--7447) | Digital Electronics | Simulation + Hardware |
| 5 | [⚙️ DC Motor Speed Control Using Arduino](#%EF%B8%8F-project-5--dc-motor-speed-control-using-arduino) | Embedded Systems | Arduino + Proteus |

---
---

## 🔊 Project 1 — Noise Reduction in Audio Signal Using Digital Filtering

[![Domain](https://img.shields.io/badge/Domain-Signal%20Processing-blue?style=flat-square)]()
[![Tool](https://img.shields.io/badge/Tool-MATLAB-orange?style=flat-square&logo=mathworks)]()
[![Filter](https://img.shields.io/badge/Filter-IIR%20Notch-purple?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

### 📌 Overview

This project focuses on removing **6 kHz electronic interference** from a noisy audio signal using a **digital IIR notch filter** implemented in MATLAB. The goal was to suppress narrowband noise while fully preserving the natural characteristics of the speech signal.

> 🎯 **Goal:** Reduce a 6 kHz interference tone using a digital notch filter while maintaining speech spectrum integrity.

---

### 🧠 Theory & Background

| Parameter | Detail |
|-----------|--------|
| 🎙️ Voice Frequency Range | 300 Hz – 3400 Hz |
| 🔴 Interference Frequency | 6000 Hz |
| 🔧 Filter Type | IIR Notch (Band-Stop) |
| 📐 Quality Factor (Q) | 60 |

> A **high Q factor** produces a narrower notch — removing only the unwanted frequency with minimal impact on surrounding content.

---

### ⚙️ Methodology

```
Load Audio → Identify Noise (6kHz) → Design IIR Notch Filter
     → Apply filtfilt() → FFT Analysis → Compare Spectra → Save Output
```

**Key MATLAB Functions Used:**

| Function | Purpose |
|----------|---------|
| `audioread()` | Load noisy audio file |
| `iirnotch()` | Design notch filter coefficients |
| `filtfilt()` | Zero-phase filtering (no distortion) |
| `fft()` | Frequency domain analysis |
| `audiowrite()` | Save cleaned audio output |

---

### 📊 Results

| Measurement | Before Filtering | After Filtering |
|-------------|-----------------|----------------|
| 6 kHz Peak | ✅ Strong spike visible | ✅ Peak eliminated |
| Speech Clarity | ✅ Intact | ✅ Fully preserved |
| Phase Distortion | — | ✅ Zero (filtfilt used) |

---

### 🛠️ Tools
`MATLAB` · `IIR Notch Filter` · `FFT Analysis` · `Digital Signal Processing` · `Audio Processing`

---
---

## ❤️ Project 2 — ECG Front-End Design
### Low-Noise Amplifier, Filtering & Signal Acquisition

[![Domain](https://img.shields.io/badge/Domain-Biomedical%20Electronics-red?style=flat-square)]()
[![Signal](https://img.shields.io/badge/Signal-ECG%20Bio--Potential-crimson?style=flat-square)]()
[![Display](https://img.shields.io/badge/Display-OLED%20128x64-green?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

### 📌 Overview

Design and implementation of a complete **ECG front-end signal acquisition system** capable of capturing extremely weak bio-potential signals from the human body and converting them into a clean, real-time observable waveform.

> ECG signals range from just **0.05 mV to 5 mV** — making precise amplification and filtering absolutely critical.

---

### 🔗 Signal Processing Chain

```
Electrodes → Instrumentation Amp → High-Pass Filter
          → Notch Filter → Low-Pass Filter
          → Microcontroller (ADC) → OLED Display
```

---

### 🧩 Analog Filter Stages

| Filter | Cutoff Frequency | Purpose |
|--------|-----------------|---------|
| 🔼 High-Pass | 0.5 Hz | Remove baseline drift from breathing |
| 🚫 Notch | 50 Hz | Remove power-line interference |
| 🔽 Low-Pass | 100 Hz | Remove high-frequency EMG noise |

---

### ⚡ Instrumentation Amplifier

| Feature | Detail |
|---------|--------|
| 📐 Gain Formula | G = 1 + (49.4 kΩ / RG) |
| 🔇 CMRR | High — rejects common-mode noise |
| 🎚️ Gain Control | External resistor (RG) |
| 🎯 RG Value Used | 49.9 kΩ |

---

### 📟 Display & Visualization

| Parameter | Specification |
|-----------|--------------|
| Display Type | 0.96" I2C OLED |
| Resolution | 128 × 64 pixels |
| Output | Real-time ECG waveform |
| Power | Low consumption |

---

### 🔧 Key Design Parameters

| Component | Value |
|-----------|-------|
| High-Pass Filter | R = 330 kΩ, C = 1 µF → ~0.5 Hz |
| Low-Pass Filter | R = 16 kΩ, C = 0.1 µF → ~100 Hz |
| Output Buffer | R = 10 kΩ (unity gain) |
| Reference Bias | R = 10 kΩ |

---

### 🛠️ Tools
`Instrumentation Amplifier` · `Analog Filter Design` · `OLED Display` · `Biomedical Signal Processing` · `ECG Acquisition`

---
---

## 🔲 Project 3 — Square Wave Generator Using NE555 Timer
### Astable Mode — Variable Frequency

[![Domain](https://img.shields.io/badge/Domain-Analog%20Electronics-yellow?style=flat-square)]()
[![IC](https://img.shields.io/badge/IC-NE555%20Timer-orange?style=flat-square)]()
[![Mode](https://img.shields.io/badge/Mode-Astable-purple?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

### 📌 Overview

Design and implementation of a **variable frequency square wave generator** using the **NE555 Timer IC** in astable mode. A potentiometer allows real-time frequency adjustment, with an LED providing visual confirmation of the output waveform.

---

### 🧩 Components

| Component | Value | Purpose |
|-----------|-------|---------|
| `NE555 Timer IC` | DIP-8 | Main oscillator IC |
| `Potentiometer R2` | 5 kΩ | Variable frequency control |
| `Resistor R1` | 10 kΩ | Charging time control |
| `Capacitor C1` | 147 µF (100µF ∥ 47µF) | Timing capacitor |
| `Control Capacitor` | 0.1 µF | Noise filtering at Pin 5 |
| `LED` | Red | Visual waveform indicator |
| `LED Resistor` | 330 Ω | Current limiting |
| `Diodes` | 1N4148 × 2 | Reverse current prevention |

---

### ⚙️ Working Principle

```
Capacitor charges through R1 + R2  →  Output HIGH  →  LED ON
        ↓
Voltage reaches 2/3 Vcc
        ↓
Internal transistor fires  →  Capacitor discharges through R2
        ↓
Output LOW  →  LED OFF  →  Cycle repeats
```

---

### 📐 Frequency Calculations

**Formula:** `T = 0.693 × (R1 + 2R2) × C1`

| Condition | R2 Value | Period (T) | High Time | Low Time |
|-----------|----------|-----------|-----------|---------|
| Max Potentiometer | 5 kΩ | ~2.04 sec | ~1.02 sec | ~1.02 sec |
| Min Potentiometer | 0 Ω | ~1.02 sec | ~0.5 sec | ~0.5 sec |

> 💡 At minimum R2, switching is too fast for the human eye — LED appears **constantly ON** even though it's still switching.

---

### 🛠️ Tools
`NE555 Timer` · `Astable Multivibrator` · `Vero Board` · `Circuit Simulation` · `Analog Circuit Design`

---
---

## 🔢 Project 4 — Two-Digit Digital Counter Using 7490 & 7447
### BCD Counter with 7-Segment Display (00–99)

[![Domain](https://img.shields.io/badge/Domain-Digital%20Electronics-blue?style=flat-square)]()
[![ICs](https://img.shields.io/badge/ICs-7490%20%26%207447-darkblue?style=flat-square)]()
[![Range](https://img.shields.io/badge/Count%20Range-00%20to%2099-green?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

### 📌 Overview

Design and implementation of a **two-digit digital counter** counting from **00 to 99** using BCD counter ICs, decoder ICs, and 7-segment displays. Each push-button press increments the count by one, and the circuit automatically resets to 00 after reaching 99.

---

### 🧩 Key ICs

| IC | Type | Function |
|----|------|----------|
| `7490` | BCD Decade Counter | Counts 0–9, produces 4-bit BCD output |
| `7447` | BCD to 7-Seg Decoder | Converts BCD to 7-segment drive signals |

---

### ⚙️ Circuit Operation

```
Push Button Press → Clock Pulse Generated
        ↓
Units Counter (7490 #1) counts 0→9
        ↓
On overflow → Tens Counter (7490 #2) increments
        ↓
BCD Output → 7447 Decoder → 7-Segment Display
        ↓
Display shows 00 → 99 → Resets to 00
```

---

### 📟 Display Specifications

| Parameter | Detail |
|-----------|--------|
| Display Type | Common-Anode 7-Segment |
| Current Range | 12 mA – 20 mA |
| Current Limiting | Resistors on each segment |
| Digits | 2 (Units + Tens) |

---

### 🔄 Expandability

> Adding another **7490 + 7447 + display** extends the counter to **000–999**, simply by connecting the carry output of one counter to the clock input of the next.

---

### 🛠️ Tools
`7490 BCD Counter` · `7447 Decoder` · `7-Segment Display` · `Digital Logic` · `Circuit Simulation` · `Hardware Implementation`

---
---

## ⚙️ Project 5 — DC Motor Speed Control Using Arduino
### Microprocessor Systems (EE-222) — NUST PNEC

[![Domain](https://img.shields.io/badge/Domain-Embedded%20Systems-teal?style=flat-square)]()
[![MCU](https://img.shields.io/badge/MCU-Arduino%20Uno-00979D?style=flat-square&logo=arduino)](https://www.arduino.cc)
[![Driver](https://img.shields.io/badge/Driver-L293N%20H--Bridge-red?style=flat-square)]()
[![Simulation](https://img.shields.io/badge/Simulation-Proteus-blue?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

### 📌 Overview

A **microcontroller-based DC motor speed control system** using **PWM (Pulse Width Modulation)** via an Arduino Uno and L293N motor driver. The system executes two predefined speed patterns simulating industrial motor control — including gradual ramp-up/down and step-wise speed changes.

---

### 🔌 Pin Connections

| Arduino Pin | Motor Driver Pin | Function |
|-------------|-----------------|---------|
| D9 | ENA | PWM speed control |
| D13 | IN1 | Motor direction |
| D12 | IN2 | Motor direction |
| GND | GND | Common ground |
| 5V | VCC | Logic supply |

---

### 📋 Speed Patterns

**Pattern 1 — Smooth Ramp:**
```
0% Speed ──── gradually ────▶ 100% (1.5 min)
           then
100% Speed ── gradually ────▶ 0% (1.5 min) ──▶ Motor OFF
```

**Pattern 2 — Step-Wise:**
```
Slow (30s) → Double (30s) → Max (30s)
          → Double down (30s) → Slow (30s) → OFF
```

---

### 🧩 Components

| Component | Specification | Qty |
|-----------|--------------|-----|
| `Arduino Uno` | ATmega328P, 5V logic | 1 |
| `DC Motor` | 12V, 0.3A | 1 |
| `L293N Driver` | Dual H-Bridge | 1 |
| `Power Supply` | 12V Adapter | 1 |

---

### 💡 Key Engineering Considerations

| Challenge | Solution |
|-----------|---------|
| ⏱️ Timing Precision | `delay()` for basic timing; `millis()` for non-blocking |
| ⚡ Voltage Mismatch | L293N bridges 5V logic ↔ 12V motor safely |
| 🔧 Speed Control | `analogWrite()` generates PWM duty cycle |
| 🧪 Verification | Proteus simulation before hardware build |

---

### 🛠️ Tools
`Arduino IDE` · `Proteus Simulation` · `PWM Control` · `L293N H-Bridge` · `Embedded C` · `Motor Control`

---
---

## 👤 About

| | |
|-|---|
| 👨‍💻 **Student** | Amir Rehman |
| 🏛️ **Institution** | NUST — Pakistan Navy Engineering College (PNEC) |
| 🏢 **Department** | Electronics & Power Engineering |
| 🌐 **GitHub** | [@amirrehman19](https://github.com/amirrehman19) |
| 💼 **Upwork** | [amirrehman19](https://www.upwork.com) |
| 📅 **Year** | 2026 |

---

> *These projects reflect hands-on learning across signal processing, biomedical electronics, analog & digital circuit design, and embedded systems — forming the foundation of a practical electronics engineering education.*

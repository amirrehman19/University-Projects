# ❤️ ECG Front-End Design
## Low-Noise Amplifier, Filtering & Signal Acquisition

> 🫀 *Capturing the heartbeat — from µV bio-potential signals to real-time OLED waveforms.*

[![Domain](https://img.shields.io/badge/Domain-Biomedical%20Electronics-red?style=flat-square)]()
[![Signal](https://img.shields.io/badge/Signal-ECG%20Bio--Potential-crimson?style=flat-square)]()
[![Amp](https://img.shields.io/badge/Amplifier-Instrumentation-orange?style=flat-square)]()
[![Display](https://img.shields.io/badge/Display-OLED%20128x64-green?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

---

## 📌 Project Overview

This project covers the complete design of an **ECG front-end signal acquisition system** — capturing extremely weak bio-potential signals produced by the heart and converting them into a clean, real-time waveform on an OLED display.

ECG signals are among the most challenging to acquire in electronics:

| ECG Signal Property | Value |
|--------------------|-------|
| ⚡ Amplitude | 0.05 mV – 5 mV |
| 📡 Frequency Range | 0.05 Hz – 100 Hz |
| 🔴 Main Threats | EMG noise, 50Hz powerline, baseline drift, motion artifacts |

> The signal is often **completely buried under noise** — making precision amplification and multi-stage filtering absolutely essential.

---

## 🔗 Complete Signal Processing Chain

```
┌──────────────────────────────────────────────────────────────┐
│                  ECG SIGNAL CHAIN                            │
│                                                              │
│  👤 Body  →  🔌 Electrodes  →  🔬 Inst. Amplifier           │
│                                        ↓                     │
│                              🔼 High-Pass Filter (0.5Hz)     │
│                                        ↓                     │
│                              🚫 Notch Filter (50Hz)          │
│                                        ↓                     │
│                              🔽 Low-Pass Filter (100Hz)      │
│                                        ↓                     │
│                              🧠 Microcontroller (ADC)        │
│                                        ↓                     │
│                              📟 OLED Display (Real-Time)     │
└──────────────────────────────────────────────────────────────┘
```

---

## 🔌 ECG Electrodes

**Standard Silver–Chloride biomedical electrodes** convert ionic body currents into electrical signals.

| Electrode | Placement | Role |
|-----------|-----------|------|
| RA | Right Arm | Positive input |
| LA | Left Arm | Negative input |
| RL | Right Leg | Reference / Ground |

---

## 🔬 Instrumentation Amplifier Stage

The **Instrumentation Amplifier** is the heart of the front-end — amplifying the tiny differential ECG signal while rejecting noise.

| Feature | Detail |
|---------|--------|
| 📐 Gain Formula | **G = 1 + (49.4 kΩ / RG)** |
| 🔇 CMRR | High — rejects common-mode interference |
| 🎚️ Gain Resistor (RG) | 49.9 kΩ |
| 🎯 Key Advantage | Amplifies differential signal, ignores noise on both lines |

---

## 🎛️ Analog Filter Stages

Three filter stages work together to clean the amplified signal:

| Filter | Cutoff | Removes | Components |
|--------|--------|---------|------------|
| 🔼 High-Pass | **0.5 Hz** | Baseline drift from breathing | R = 330 kΩ, C = 1 µF |
| 🚫 Notch | **50 Hz** | Power-line interference | — |
| 🔽 Low-Pass | **100 Hz** | EMG muscle noise | R = 16 kΩ, C = 0.1 µF |

---

## 📟 OLED Visualization

The processed ECG signal is displayed in real-time on a compact OLED screen:

| Parameter | Specification |
|-----------|--------------|
| Display Size | 0.96 inch |
| Interface | I2C |
| Resolution | **128 × 64 pixels** |
| Output | Live ECG waveform |
| Power | Low consumption |

---

## 🔧 Full Design Parameters

| Component | Value | Purpose |
|-----------|-------|---------|
| Gain Resistor (RG) | 49.9 kΩ | Sets instrumentation amp gain |
| HP Filter | R = 330 kΩ, C = 1 µF | ~0.5 Hz cutoff |
| LP Filter | R = 16 kΩ, C = 0.1 µF | ~100 Hz cutoff |
| Output Buffer | R = 10 kΩ | Unity gain buffering |
| Reference Bias | R = 10 kΩ | Centers signal at reference voltage |

---

## ⚠️ Design Challenges

| Challenge | Consideration |
|-----------|--------------|
| 🔬 Weak Signals | µV-level signals require ultra-low noise amplification |
| ⚡ Noise Sensitivity | EMF, EMG, motion all corrupt signal easily |
| 🛡️ Safety | Biomedical circuits must ensure electrical isolation from body |
| 🔋 Power | Low-power design critical for wearable/portable use |

---

## ✅ Conclusion

This project demonstrates how **extremely weak biological signals** (µV range) can be successfully acquired, amplified, filtered, and displayed in real time. The design highlights the importance of precision analog design in biomedical electronics.

> *"From heartbeat to waveform — the complete journey of an ECG signal."*

---

## 🛠️ Tools & Technologies

`Instrumentation Amplifier` · `IIR Filter Design` · `Analog Signal Conditioning` · `OLED Display` · `I2C Protocol` · `Biomedical Signal Processing` · `ECG Acquisition`

---

## 👤 About

| | |
|-|---|
| 👨‍💻 **Student** | Amir Rehman |
| 🏛️ **Institution** | NUST — PNEC, Karachi |
| 🌐 **GitHub** | [@amirrehman19](https://github.com/amirrehman19) |

---

⬅️ *Back to [University Projects Portfolio](../README.md)*

# ⚡ Full Wave Precision Rectifier | Op-Amp + Diode | Proteus Simulation

<p align="center">
<img width="589" height="314" alt="diagram" src="https://github.com/user-attachments/assets/42fe3bef-a795-491d-bb11-5f65009b6a80" />

</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tool-Proteus%208-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Op--Amp-General%20Purpose-red?style=flat-square"/>
  <img src="https://img.shields.io/badge/Type-Full%20Wave%20Precision-yellow?style=flat-square"/>
  <img src="https://img.shields.io/badge/Status-Simulated%20%26%20Working-brightgreen?style=flat-square"/>
  <img src="https://img.shields.io/badge/Domain-Analog%20Electronics-orange?style=flat-square"/>
</p>

---

## 📌 Overview

This project presents a fully simulated **Full Wave Precision Rectifier** built using two **op-amps** and two **diodes** in Proteus 8 Professional. Unlike a conventional diode rectifier that suffers from a 0.7V forward voltage drop, a precision rectifier uses op-amp feedback to eliminate this limitation — making it capable of rectifying signals as small as a few millivolts with near-perfect accuracy.

The circuit takes an AC sinusoidal input and converts it into a full-wave rectified output, where both the positive and negative half-cycles appear as positive at the output — verified on the Proteus digital oscilloscope.

---

## ⚡ Theory of Operation

A standard diode rectifier fails for small signals because it requires ~0.7V to turn on. A **precision rectifier** places the diode inside the op-amp feedback loop, which forces the op-amp to compensate for the diode drop automatically — effectively making it an ideal diode with **0V forward voltage drop**.

### How It Works — Stage by Stage

**Stage 1 — Inverting Half-Wave Rectifier (U1)**
- U1 operates as an inverting amplifier
- D1 conducts during the negative half-cycle, feeding back through R2
- D2 blocks during positive half-cycles
- Output of Stage 1: inverted negative half-cycles (now positive)

**Stage 2 — Summing Amplifier (U2)**
- U2 sums the Stage 1 output with the original input signal
- R3, R4, R5 are scaled to produce the correct weighted sum
- Result: both half-cycles reconstructed as positive → **full wave rectification**

### Key Advantage Over Conventional Rectifier

| Feature | Conventional Rectifier | Precision Rectifier |
|---------|----------------------|-------------------|
| Min. input voltage | ~0.7V | Near 0V |
| Forward voltage drop | 0.7V per diode | ~0V (compensated) |
| Accuracy | Low for small signals | High across all amplitudes |
| Use case | Power supplies | Instrumentation, measurement |

---

## 🛠️ Circuit Components

| Ref | Component | Value | Description |
|-----|-----------|-------|-------------|
| U1 | Op-Amp | — | Inverting half-wave rectifier stage |
| U2 | Op-Amp | — | Summing amplifier stage |
| D1 | Diode | — | Feedback diode (negative half-cycle path) |
| D2 | Diode | — | Output diode (positive half-cycle path) |
| R1 | Resistor | 6.4 kΩ | Input resistor |
| R2 | Resistor | 6.4 kΩ | Feedback resistor (Stage 1) |
| R3 | Resistor | 3.2 kΩ | Input resistor (Stage 2) |
| R4 | Resistor | 6.4 kΩ | Feedback resistor (Stage 2) |
| R5 | Resistor | 6.4 kΩ | Summing resistor (Stage 2) |

### Gain Analysis

**Stage 1 gain** (inverting):

$$A_1 = -\frac{R2}{R1} = -\frac{6.4k}{6.4k} = -1$$

**Stage 2 summing output:**

$$V_{out} = -\left(\frac{R4}{R3} \cdot V_{stage1} + \frac{R4}{R5} \cdot V_{in}\right) = -\left(2 \cdot V_{stage1} + V_{in}\right)$$

The resistor ratio R4/R3 = 2 ensures the negative half-cycles are scaled correctly so the final output is a true full-wave rectified signal.

---

## 📊 Simulation Results

The oscilloscope output captured in Proteus confirms successful full-wave rectification.

<p align="center">
  <img width="690" height="443" alt="output" src="https://github.com/user-attachments/assets/c8afabb5-cd3e-4582-a8be-0070c304fba5" />

</p>

**Observed Output:**
- ✅ Channel A (Yellow) — Original AC sine wave input
- ✅ Channel B (Blue) — Full wave rectified output
- ✅ Both negative half-cycles correctly flipped to positive
- ✅ No 0.7V diode drop visible — precision rectification confirmed
- ✅ Stable, consistent waveform across all cycles

---

## 📁 Project Structure

```
full-wave-precision-rectifier/
│
├── docs/
│   ├── schematic.png                  # Circuit schematic screenshot
│   └── oscilloscope.png               # Oscilloscope output screenshot
│
├── simulation/
│   └── precision_rectifier.pdsprj     # Proteus project file
│
└── README.md
```

---

## 🚀 How to Run

1. **Clone this repo**
   ```bash
   git clone https://github.com/amirrehman19/University-Projects.git
   ```

2. **Open Proteus 8**
   - Launch Proteus 8 Professional
   - Open `simulation/precision_rectifier.pdsprj`

3. **Run the simulation**
   - Press the **Play** button
   - Open the **Digital Oscilloscope** from virtual instruments
   - Observe Channel A (input sine wave) vs Channel B (rectified output)

---

## 📚 Key Concepts Covered

- Ideal diode model using op-amp feedback
- Inverting amplifier configuration
- Summing amplifier with weighted resistor network
- Half-wave vs full-wave precision rectification
- Effect of resistor ratios on gain and output scaling
- Proteus analog simulation and multi-channel oscilloscope

---

## 🔁 Comparison: Half Wave vs Full Wave Precision Rectifier

| Feature | Half Wave | Full Wave |
|---------|-----------|-----------|
| Rectified cycles | Positive only | Both positive & negative |
| Output ripple | High | Low |
| Efficiency | 50% | 100% |
| Circuit complexity | Simple (1 op-amp) | Moderate (2 op-amps) |
| This project | ❌ | ✅ |

---

## 🌍 Real-World Applications

- **AC signal measurement** in digital multimeters
- **Audio signal processing** and envelope detection
- **Biomedical instrumentation** (ECG, EMG signal conditioning)
- **Power metering** and RMS conversion circuits
- **Signal demodulation** in communication systems

---

## 🎓 About

This project was built as part of **Electronic Circuit Design (ECD)** coursework at NUST PNEC. It demonstrates practical understanding of precision analog circuit design using simulation-based verification.

> 📺 **YouTube Channel** — EE concepts, circuit simulations, and numericals explained in Urdu/English for Pakistani engineering students.
> 🔗 [github.com/amirrehman19](https://github.com/amirrehman19)

---

## 📜 License

This project is open-source under the [MIT License](LICENSE).

---

<p align="center">Built with precision — because 0.7V matters when your signal is 0.8V.</p>

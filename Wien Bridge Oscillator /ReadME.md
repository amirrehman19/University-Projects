# 🔁 Wien Bridge Oscillator — LM358N Op-Amp | Proteus Simulation

<p align="center">
  <img src="docs/schematic.png" alt="Wien Bridge Oscillator Schematic" width="800"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tool-Proteus%208-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/Op--Amp-LM358N-red?style=flat-square"/>
  <img src="https://img.shields.io/badge/Status-Simulated%20%26%20Working-brightgreen?style=flat-square"/>
  <img src="https://img.shields.io/badge/Domain-Analog%20Electronics-orange?style=flat-square"/>
</p>

---

## 📌 Overview

This project presents a fully simulated **Wien Bridge Oscillator** built using the **LM358N dual op-amp** in Proteus. The Wien Bridge Oscillator is a classic RC-based sinusoidal oscillator that generates a stable, low-distortion sine wave without any external input signal.

The oscillation frequency is set by the RC network and the gain is controlled by a feedback resistor network — making it widely used in audio signal generation, function generators, and instrumentation.

---

## ⚡ Theory of Operation

The Wien Bridge Oscillator works on the principle of **positive feedback** through a frequency-selective RC bridge, balanced against **negative feedback** through a resistor divider to control gain.

### Oscillation Condition (Barkhausen Criterion)

For sustained oscillation, two conditions must be met:

1. **Loop Gain = 1** → `|Aβ| = 1`
2. **Phase Shift = 0°** → net phase around the loop must be 0° (or 360°)

### Oscillation Frequency

$$f_0 = \frac{1}{2\pi RC}$$

With the values used in this design:

| Component | Value     |
|-----------|-----------|
| R1, R2    | 39 kΩ     |
| C1, C3    | 0.01 µF   |
| RG        | 10 kΩ     |
| RF        | 100 kΩ    |
| Op-Amp    | LM358N    |

**Calculated Frequency:**

$$f_0 = \frac{1}{2\pi \times 39k \times 0.01\mu} \approx 408 \ \text{Hz}$$

### Gain Condition

For stable sinusoidal output, the non-inverting amplifier gain must equal exactly **3**:

$$A_v = 1 + \frac{R_F}{R_G} = 1 + \frac{100k}{10k} \approx ... $$

> ⚠️ In practice, gain is set slightly above 3 to ensure startup, then amplitude stabilizes due to soft limiting.

---

## 🛠️ Circuit Components

| Ref | Component | Value    | Description                         |
|-----|-----------|----------|-------------------------------------|
| U1  | LM358N    | —        | Dual general-purpose op-amp         |
| R1  | Resistor  | 39 kΩ    | RC network (frequency-setting)      |
| R2  | Resistor  | 39 kΩ    | RC network (frequency-setting)      |
| C1  | Capacitor | 0.01 µF  | RC network (frequency-setting)      |
| C3  | Capacitor | 0.01 µF  | RC network (frequency-setting)      |
| RG  | Resistor  | 10 kΩ    | Gain resistor (negative feedback)   |
| RF  | Resistor  | 100 kΩ   | Feedback resistor (controls gain)   |

---

## 📊 Simulation Results

The oscilloscope output (captured in Proteus) confirms clean sinusoidal oscillation at the expected frequency.

<p align="center">
  <img src="docs/oscilloscope.png" alt="Oscilloscope Output" width="700"/>
</p>

**Observed Output:**
- ✅ Stable sinusoidal waveform with no clipping
- ✅ Consistent amplitude across time
- ✅ Frequency matches theoretical calculation (~408 Hz)
- ✅ Low distortion output

---

## 📁 Project Structure

```
wien-bridge-oscillator/
│
├── docs/
│   ├── schematic.png          # Circuit schematic screenshot
│   └── oscilloscope.png       # Oscilloscope output screenshot
│
├── simulation/
│   └── wien_bridge.pdsprj     # Proteus project file
│
└── README.md
```

---

## 🚀 How to Run

1. **Clone this repo**
   ```bash
   git clone https://github.com/yourusername/wien-bridge-oscillator.git
   ```

2. **Open Proteus**
   - Launch Proteus 8 Professional (or compatible version)
   - Open `simulation/wien_bridge.pdsprj`

3. **Run the simulation**
   - Press the **Play** button
   - Open the **Digital Oscilloscope** from instruments
   - Observe the sinusoidal waveform on the output

---

## 📚 Key Concepts Covered

- RC phase-shift networks and frequency selectivity
- Barkhausen Criterion for sustained oscillations
- Op-amp gain configuration (non-inverting amplifier)
- Positive vs. negative feedback in oscillator design
- Proteus analog simulation and virtual oscilloscope

---

## 🎓 About

This project was built as part of an **Electrical Engineering** coursework/lab exercise. It's intended to demonstrate practical understanding of analog oscillator design using simulation tools.

> **YouTube Channel:** Coming soon — EE concepts explained in Urdu/English for Pakistani engineering students.

---

## 📜 License

This project is open-source under the [MIT License](LICENSE).

---

<p align="center">Made with ❤️ by an EE student who actually understands the math behind it.</p>

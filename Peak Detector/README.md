# Peak Detector Circuit — Proteus Simulation

A complete simulation of a **precision peak detector circuit** built in Proteus, using an audio `.wav` file (noise generator) as input to produce a real-world varying-amplitude signal. The circuit captures and holds the positive peak voltage of the input signal.

---

## Table of Contents

- [Overview](#overview)
- [Circuit Variants](#circuit-variants)
  - [1. Simple Diode-Capacitor Peak Detector](#1-simple-diode-capacitor-peak-detector)
  - [2. Precision Peak Detector (Op-Amp + Diode)](#2-precision-peak-detector-op-amp--diode)
  - [3. Buffered Peak Detector](#3-buffered-peak-detector)
  - [4. Improved Peak Detector (Anti-Saturation)](#4-improved-peak-detector-anti-saturation)
- [Simulation Setup](#simulation-setup)
- [Oscilloscope Results](#oscilloscope-results)
- [Key Design Considerations](#key-design-considerations)
- [Components Used](#components-used)
- [How It Works — Theory](#how-it-works--theory)
- [References](#references)

---

## Overview

A **peak detector circuit** measures and holds the maximum (peak) voltage of an input signal. This is useful in applications such as:

- Audio signal processing
- Envelope detection
- Power monitoring
- Data acquisition systems

This project simulates the circuit in **Proteus** using:
- A `.wav` audio file fed through a noise/signal generator as input (random amplitudes)
- An oscilloscope to compare input vs. detected peak output
- Diodes, capacitors, op-amps, and a buffer stage

---

## Circuit Variants

### 1. Simple Diode-Capacitor Peak Detector

<img width="915" height="421" alt="WhatsApp Image 2026-06-29 at 4 37 45 PM" src="https://github.com/user-attachments/assets/27803ee0-ef65-4a9f-b621-1a471579f4fd" />


The most basic form of the peak detector. It uses just a **diode** and a **capacitor**:

- When the input voltage rises, the diode conducts and charges the capacitor up to the peak voltage.
- Once the input starts falling, the diode becomes reverse-biased, and the capacitor **holds** the peak value.
- The diode conducts again only when the input exceeds the previously stored peak.

**Limitation:** The actual diode has a forward voltage drop (~0.7V for silicon), so the output is slightly less than the true peak. This circuit is suitable only for rough approximations.

> To detect the **negative peak**, reverse the diode direction.

---

### 2. Precision Peak Detector (Op-Amp + Diode)

<img width="768" height="520" alt="WhatsApp Image 2026-06-29 at 4 40 07 PM" src="https://github.com/user-attachments/assets/c1ee5e7d-6b6f-4eb8-bee8-d83a815fbb68" />


To eliminate the diode voltage drop, a **precision rectifier (super diode)** is used — an op-amp with a diode in its feedback loop. This makes the circuit behave like an **ideal diode** with zero forward voltage drop.

- Adding a capacitor at the output of the precision rectifier creates a **precision peak detector**.
- The output accurately tracks and holds the true peak of the input signal.

---

### 3. Buffered Peak Detector

<img width="928" height="492" alt="WhatsApp Image 2026-06-29 at 4 42 12 PM" src="https://github.com/user-attachments/assets/64c66ba1-37f0-47cf-8c90-b9689a49e698" />


When the output is connected to a load (external resistor or the input impedance of another circuit), the capacitor slowly discharges through it — causing the held peak voltage to droop over time.

**Solution:** Insert a **buffer (voltage follower op-amp)** between the capacitor and the load.

- The buffer provides **very high input impedance**, preventing the capacitor from discharging through the load.
- A **reset switch** (or transistor controlled by a microcontroller) can be connected across the capacitor to manually discharge it when needed.

**RC Time Constant Rules:**
| Condition | Requirement |
|-----------|------------|
| Discharging (diode OFF) | RC ≥ 10 × signal period |
| Charging (diode ON) | RC ≤ (1/10) × signal period |

Where `Rd` is the forward resistance of the diode during charging.

---

### 4. Improved Peak Detector (Anti-Saturation)

<img width="931" height="503" alt="WhatsApp Image 2026-06-29 at 4 42 44 PM" src="https://github.com/user-attachments/assets/85858d6a-ca09-4578-8c71-02b495d432a7" />


**Problem with the buffered circuit:** When the diode is reverse-biased (not conducting), the op-amp operates in **open-loop** with no feedback. This drives it into **negative saturation**. When the input rises again, the op-amp takes time to recover (limited by its slew rate), restricting the circuit's ability to track **fast-changing signals**.

**Solution:** Add a **second diode (D2)** in a feedback path:

- When the input is below the peak → D1 (main diode) is reverse-biased.
- The op-amp output momentarily goes negative → **D2 becomes forward-biased**, providing local feedback.
- This keeps the op-amp output clamped near the input voltage, **preventing saturation**.
- The op-amp can now respond quickly when the input rises again.

> For **very high-speed** peak detection, use **Schottky diodes** — they have much faster switching times than standard signal diodes.

---

## Simulation Setup

### Proteus Schematic
<img width="2131" height="2131" alt="schematic" src="https://github.com/user-attachments/assets/0fcbbb1c-8552-4863-855e-48d746c02f12" />


**Schematic components:**

| Label | Component | Value |
|-------|-----------|-------|
| U1 | Op-Amp (main) | LM741 or equivalent |
| U2 | Op-Amp (buffer) | LM741 or equivalent |
| D1 | Diode (main) | 1N4148 |
| D2 | Diode (feedback) | 1N4148 |
| R1 | Resistor | 10 kΩ |
| RL | Load Resistor | 10 kΩ |
| C1 | Capacitor | 10 µF |

**Input Signal:**  
A `.wav` audio file is used as the input source via Proteus's signal generator, producing a **noise-like signal with random amplitudes** — ideal for testing peak detection under real-world conditions.

**Oscilloscope Channels:**
| Channel | Signal |
|---------|--------|
| A (Yellow) | Input signal (audio/noise) |
| B | Input reference |
| C | Peak detector output |
| D | Additional monitoring |

---

## Oscilloscope Results

<img width="689" height="439" alt="output" src="https://github.com/user-attachments/assets/2219339b-2ecc-480e-9cca-5c03616afcc1" />


The oscilloscope display shows:

- **Yellow trace (Channel A):** The raw input signal from the `.wav` / noise generator — note the irregular, varying amplitude waveform.
- **Red trace (Channel C):** The peak detector output — a slowly decaying DC level that **tracks and holds the highest amplitude** seen so far in the input.

**Observations:**
- The output voltage rises with each new peak in the input.
- Between peaks, the output slowly decays (capacitor discharge through load).
- The buffer stage significantly reduces the discharge rate.
- The circuit correctly ignores input drops below the current held peak.

---

## Key Design Considerations

### 1. Diode Forward Voltage Drop
- Standard diodes introduce ~0.7V error.
- Use a **precision rectifier (op-amp + diode)** to eliminate this.

### 2. Capacitor Discharge
- Load resistance causes the capacitor to discharge between peaks.
- Use a **buffer** (unity-gain op-amp follower) to isolate the load.
- Choose **large RC time constant** relative to the signal period.

### 3. Op-Amp Saturation
- Without a feedback diode (D2), the op-amp saturates when the input drops below the peak.
- The saturation recovery time (governed by slew rate) limits the maximum detectable signal frequency.
- The **improved circuit with D2** prevents saturation and enables detection of fast signals.

### 4. Speed / High-Frequency Operation
- For fast signals, use **Schottky diodes** (lower forward voltage, faster switching).
- Choose op-amps with high **slew rate** and **bandwidth**.

### 5. Circuit Reset
- Connect a switch or transistor across C1 to discharge the capacitor on demand.
- A microcontroller can automate this reset using a GPIO pin.

---

## Components Used

- **Op-Amps:** 2× (e.g., LM741, TL071, or OP07 for precision)
- **Diodes:** 2× 1N4148 signal diodes (or Schottky for high speed)
- **Capacitor:** 10 µF electrolytic
- **Resistors:** 10 kΩ × 2
- **Signal Source:** `.wav` audio file via Proteus signal generator
- **Oscilloscope:** Proteus virtual oscilloscope (4-channel)

---

## How It Works — Theory

```
           D1
Vin ──────►|──────┬──────── Vout
                  │
                 [C]
                  │
                 GND
```

1. **Charging phase:** When `Vin > Vcap`, diode D1 conducts and C charges to `Vin`.
2. **Holding phase:** When `Vin < Vcap`, D1 reverse-biases and C holds the peak voltage.
3. **New peak:** If `Vin` rises above the stored value, D1 conducts again and C charges to the new peak.

In the precision version, the op-amp compensates for the diode drop by placing the diode **inside the feedback loop**, so the virtual ground principle ensures zero net drop at the output.

---

## References

- Video: *Peak Detector Circuit Design* — ALL ABOUT ELECTRONICS (YouTube)
- Proteus Design Suite simulation
- Sedra & Smith — *Microelectronic Circuits*
- Texas Instruments — Op-Amp application notes

---

## License

This project is for educational purposes. Feel free to use, modify, and share.

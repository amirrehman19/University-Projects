# Square Wave Generator of Variable Frequency Using NE555 Timer (Astable Mode)

## Project Report

Electronic Circuit Design

---

## Objective

The objective of this project is to design and simulate a **variable frequency square wave generator** using the **NE555 Timer IC configured in astable mode**.

A potentiometer is used to adjust the oscillation frequency of the circuit. An LED is connected at the output to visually verify the generation of the square waveform.

---

## Equipment / Components

| Component          | Value / Specification   | Purpose                                    |
| ------------------ | ----------------------- | ------------------------------------------ |
| NE555 Timer IC     | DIP-8                   | Main IC used to generate square wave       |
| Potentiometer (R2) | 5 kΩ                    | Variable resistor used to adjust frequency |
| Resistor (R1)      | 10 kΩ                   | Determines charging time with R2           |
| Capacitor (C1)     | 147 µF (100 µF ∥ 47 µF) | Timing capacitor                           |
| Control Capacitor  | 0.1 µF                  | Noise filtering at Pin 5                   |
| LED                | Red                     | Visual indicator of output waveform        |
| LED Resistor       | 330 Ω                   | Limits current through LED                 |
| Diodes             | 1N4148 (×2)             | Prevent reverse current / waveform shaping |
| Vero Board         | —                       | Permanent circuit assembly                 |
| Connecting Wires   | —                       | Circuit connections                        |
| DC Power Supply    | 5–12 V                  | Power source                               |

---

## Description

The **NE555 timer** is configured in **astable multivibrator mode**, meaning it continuously generates square waves without requiring any external triggering signal.

### Working Process

### 1. Charging Phase

The capacitor **C1 charges through R1 and R2**.
The voltage across the capacitor rises from **1/3 Vcc to 2/3 Vcc**.

During this time:

* Output at **Pin 3 becomes HIGH**
* The **LED turns ON**

### 2. Discharging Phase

When the capacitor voltage reaches **2/3 Vcc**, the internal discharge transistor of the NE555 turns ON.

The capacitor **discharges through R2 only**.

During this time:

* Output becomes **LOW**
* The **LED turns OFF**

### 3. Frequency Control

The potentiometer **R2** allows adjustment of the oscillation frequency by changing:

• Charging time
• Discharging time
• Overall oscillation period

This makes the output square wave **variable in frequency**.

### 4. Noise Prevention

A **0.1 µF capacitor** is connected to **Pin 5 (Control Voltage)** to stabilize the internal comparator reference levels and prevent false triggering due to electrical noise.

---

## Why the LED Blinks

The LED is used only as a **visual indicator** to confirm that the circuit is producing a square wave.

At **low frequencies**, the LED visibly turns ON and OFF.

At **higher frequencies**, the switching occurs too rapidly for the human eye to perceive, causing the LED to appear continuously ON.

---

## Why the LED Appears Constant When the Potentiometer Is at Minimum

When the potentiometer **R2 is set close to 0 Ω**, the time period of the waveform becomes very short.

The LED switching occurs very quickly, approximately:

* ON time ≈ 0.5 seconds
* OFF time ≈ 0.5 seconds

Because this switching becomes too fast to detect visually, the LED appears continuously ON even though it is still switching.

---

## Calculations

The time period for the NE555 in astable mode is given by:

**T = 0.693 (R1 + 2R2) C1**

### Given Values

R1 = 10 kΩ
R2 = 5 kΩ
C1 = 147 µF

---

### Case 1: Maximum Potentiometer Value (R2 = 5 kΩ)

T = 0.693 (10,000 + 2 × 5,000) (147 × 10⁻⁶)

T = 0.693 (20,000) (147 × 10⁻⁶)

T ≈ **2.038 seconds**

Therefore:

High Time ≈ **1.02 seconds**
Low Time ≈ **1.02 seconds**

---

### Case 2: Minimum Potentiometer Value (R2 = 0 Ω)

T = 0.693 (10,000) (147 × 10⁻⁶)

T ≈ **1.02 seconds**

---

## Observation

• At maximum potentiometer value, the LED clearly blinks with approximately **1 second ON and 1 second OFF** timing.

• At minimum potentiometer value, blinking becomes very fast and is no longer visible to the human eye, confirming that the **frequency increases as resistance decreases**.

• Circuit simulation confirmed:

* Square wave output at **Pin 3**
* Charging and discharging waveform across the capacitor
* Frequency variation through the potentiometer
* LED brightness behavior changes with frequency

---

## Results

The variable-frequency square wave generator using the **NE555 timer IC** was successfully designed and implemented.

Key results include:

• Frequency control achieved through a **5 kΩ potentiometer**
• Stable waveform generation using the **NE555 astable configuration**
• Improved signal stability through the **0.1 µF noise filtering capacitor**
• Visual verification of output waveform using an LED

This circuit can be used in various applications including:

• Clock generation
• Pulse generation
• LED drivers
• Timing circuits
• Digital system testing

---

## Circuit Design, Simulation, and Implementation

The project involved the following stages:

1. Circuit schematic design
2. Simulation of the circuit behavior
3. Hardware implementation using a Vero board

The physical circuit assembly verified the successful operation of the design and matched the simulated results.

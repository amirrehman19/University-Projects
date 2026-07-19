# Automatic Light Lamp Using LDR (Light Dependent Resistor) — Auto ON/OFF Street Light Circuit

An **automatic street light / lamp control circuit** built using an **LDR (Light Dependent Resistor)** and **LM358 comparator IC**. The circuit automatically switches LEDs/lamps **ON at night** (low ambient light) and **OFF during the day** (bright ambient light) — a classic **dusk-to-dawn light sensor project** for electronics, embedded systems, and IoT enthusiasts.

![Platform](https://img.shields.io/badge/platform-Proteus-blue)
![Language](https://img.shields.io/badge/type-Analog%20Circuit-orange)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📌 Overview

This project demonstrates a **fully automatic LDR-based light control circuit** that senses ambient light intensity and drives a lamp/LED load accordingly, without any manual switching or microcontroller. It's an ideal beginner-to-intermediate **analog electronics project** for:

- Automatic street light systems
- Smart home / garden lighting
- Energy-saving lighting automation
- Electronics lab / academic mini-projects
- Learning comparator (LM358) and transistor switching circuits

---

## ⚙️ How It Works

1. **AC to DC Power Supply**: Mains AC (`V2`) is converted to DC using a **bridge rectifier (BR2)**, filtered by capacitor `C3` (1000µF), and regulated to a stable **+12V** using the `7812` linear voltage regulator (`U1`).
2. **Light Sensing**: The `LDR2` (photoresistor) forms a **voltage divider** with resistor `R1`. Its resistance drops in bright light and rises in the dark, changing the voltage at the divider node.
3. **Reference Voltage**: Resistors `R7` and `R8` form a fixed reference voltage divider connected to the comparator's inverting input.
4. **Comparator Stage**: The `LM358` op-amp (`U2:A`) compares the LDR voltage against the reference voltage.
   - **Daytime** (bright light → low LDR resistance): comparator output stays LOW → transistor OFF → LEDs OFF.
   - **Nighttime** (darkness → high LDR resistance): comparator output goes HIGH → turns `Q2` (BC547 NPN transistor) ON via base resistor `R3` → LEDs turn ON.
5. **Switching Stage**: Transistor `Q2` acts as an electronic switch, driving the LED load (can be scaled up to relay + bulb/lamp for real street light applications).

---

## 🧩 Components Used

| Component | Designator | Value / Part | Function |
|---|---|---|---|
| AC Source | V2 | VSINE | Mains input simulation |
| Bridge Rectifier | BR2 | Diode Bridge | AC to DC conversion |
| Filter Capacitor | C3 | 1000µF | Ripple filtering |
| Voltage Regulator | U1 | 7812 | Regulated +12V DC output |
| LDR (Photoresistor) | LDR2 | TORCH_LDR | Ambient light sensing |
| Resistors | R1, R7, R8 | 10kΩ | Voltage divider / reference network |
| Comparator | U2:A | LM358 | Light-level comparison |
| Base Resistor | R3 | 1kΩ | Transistor biasing |
| Switching Transistor | Q2 | BC547 | LED/lamp driver switch |
| Load | LED1–LED3 | LED | Output indicator lamps |
| Buzzer (optional) | — | — | Optional audible indicator |

---

## 🖼️ Circuit Simulation States

| Condition | LDR Resistance | Comparator Output | Lamp State |
|---|---|---|---|
| 🌞 Daytime (bright light) | Low | LOW | OFF |
| 🌙 Nighttime (dark) | High | HIGH | ON |

<img width="906" height="399" alt="night" src="https://github.com/user-attachments/assets/e678b803-d211-47de-86ce-c9ffdf3f695b" />


## 🛠️ Tools & Software

- **Proteus Design Suite** — schematic capture & simulation
- Standard analog components (resistors, LDR, LM358, BC547, 7812 regulator)

---

## 🚀 Getting Started

1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/automatic-ldr-light-lamp.git
   ```
2. Open the `.pdsprj` / schematic file in **Proteus**.
3. Run the simulation and cover/uncover the LDR to observe the lamp switching automatically.
4. For a real hardware build, replace the LED array with a **relay module** to control an actual AC lamp/street light.

---

## 🔋 Real-World Applications

- Automatic **street light controllers**
- **Solar garden lights**
- Automatic **staircase/porch lighting**
- Energy-efficient **outdoor lighting systems**
- Base circuit for **IoT-enabled smart lighting** (can be extended with ESP32/Arduino for remote monitoring)

---

## 📈 Possible Enhancements

- Add a **relay + real AC bulb** for practical deployment
- Integrate **ESP32/Arduino** for IoT-based remote monitoring and logging
- Add **PWM dimming** based on ambient light intensity instead of ON/OFF switching
- Add **hysteresis** to the comparator to prevent flickering at threshold light levels

---

## 📄 License

This project is open-sourced under the **MIT License** — free to use, modify, and distribute for educational and commercial purposes.

---

## 👤 Author

Developed by **[GenXi Tech Solutions](https://genxitechsolutions.com)** — Engineering & Technology Project Services (PCB Design, Embedded Systems, IoT, Automation).

---

### 🔍 Keywords
`LDR circuit` `automatic light control` `LM358 comparator` `dusk to dawn switch` `automatic street light project` `light sensor circuit` `Proteus simulation` `BC547 transistor switch` `7812 voltage regulator circuit` `electronics mini project`

# Two-Digit Digital Counter Using 7490 and 7447 ICs

## Project Overview

This project demonstrates the design and implementation of a **two-digit digital counter** capable of counting from **00 to 99**. The circuit uses **BCD counters, decoder ICs, and 7-segment displays** to visually represent the count.

Each press of a push-button generates a clock pulse that increments the counter by one. The circuit automatically resets after reaching **99**, returning the display to **00**.

The design illustrates fundamental concepts of **digital electronics**, including binary-coded decimal counting, decoder operation, and display interfacing.

---

# 1. Objective

The objective of this project is to design and implement a **2-digit digital counter** that counts from **00 to 99** using BCD counters and 7-segment displays.

The system uses two BCD counters for the units and tens positions, with decoder ICs translating binary outputs into signals suitable for driving the displays.

---

# 2. Components and Their Functions

## 7490 IC – Binary Coded Decimal Counter

The **7490** is a decade counter that produces a **4-bit Binary Coded Decimal (BCD) output**.

### Key Features

• Counts from **0 to 9**
• Produces BCD outputs from **0000 to 1001**
• Automatically resets to **0 after 9**
• Supports cascading with other counters for multi-digit counting

### Function in the Circuit

Two 7490 counters are used:

• The **first counter** controls the **units digit**
• The **second counter** controls the **tens digit**

When the units counter completes a full cycle from **0 to 9**, it triggers the tens counter to increment by one.

---

## 7447 IC – BCD to 7-Segment Decoder

The **7447 decoder** converts the **4-bit BCD output** from the 7490 counter into signals that drive a **7-segment display**.

### Key Features

• Converts BCD inputs to segment control signals
• Designed for **common-anode 7-segment displays**
• Uses **active LOW outputs** to illuminate segments
• Includes additional control inputs such as:

Lamp Test (LT) – activates all display segments for testing
Blanking Input (BI) – disables the display when required

---

## 7-Segment Displays

A **7-segment display** consists of seven LEDs arranged in a pattern capable of displaying digits from **0 to 9**.

### Features

• Used to visually display the counter output
• The project uses **common-anode displays**
• Each segment requires a **current-limiting resistor** to protect the LED

### Current Limiting

Resistors are selected to limit current between:

**12 mA – 20 mA**

This ensures:

• Proper brightness
• Protection against LED damage
• Consistent illumination across segments

---

## Push-Button Switch

The **push-button switch** acts as the **clock input** for the counter circuit.

### Function

• Each press generates a pulse
• The pulse increments the counter by **one digit**

The switching configuration determines whether the counter advances on the **press** or **release** of the button.

---

# 3. Circuit Functionality

The circuit begins counting from **00**.

Each press of the push-button produces a clock pulse that increments the count.

### Units Counter

The first 7490 counter counts from **0 to 9**, representing the **units digit**.

### Tens Counter

When the units counter completes its cycle and resets, the **tens counter increments by one**.

### Display Conversion

The BCD outputs from each counter are fed into **7447 decoder ICs**, which convert the binary values into signals for the **7-segment displays**.

The displays then show the decimal representation of the count.

---

# 4. Expandability

One advantage of this design is its **modular structure**.

Additional counters and displays can easily be added to extend the counting range.

For example:

Adding another **7490 counter and 7447 decoder** creates a **three-digit counter** capable of counting from:

**000 to 999**

This is achieved by connecting the **carry output** of one counter to the **clock input** of the next counter.

---

# 5. Simulation

Before hardware implementation, the circuit can be simulated using digital circuit simulation software.

Simulation allows verification of:

• Proper counting sequence
• Correct display decoding
• Accurate timing of counter transitions

This helps ensure the circuit functions correctly before building the physical hardware.

---

# 6. Hardware Implementation

After successful simulation, the circuit can be implemented using:

• Digital ICs (7490 and 7447)
• Two 7-segment displays
• Current-limiting resistors
• A push-button switch
• Breadboard or PCB connections

The physical implementation demonstrates the real-world behavior of the digital counter.

---

# 7. Conclusion

This project demonstrates the design of a **two-digit digital counter using BCD counters and decoder circuits**. The system provides a clear visual representation of numerical counting using 7-segment displays.

The design highlights important concepts in digital electronics, including:

• Binary coded decimal counting
• Decoder operation
• Display interfacing
• Modular circuit expansion

Because of its flexible structure, the design can easily be extended to create larger counters for various digital electronics applications.

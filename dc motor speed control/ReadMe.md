# DC Motor Speed Control System Using Arduino

## Microprocessor Systems (EE-222)

**Department of Electronics and Power Engineering**
**Pakistan Navy Engineering College (PNEC)**
**National University of Sciences and Technology (NUST), Karachi**

---

# Table of Contents

1. Introduction
2. Objectives
3. Problem Description
4. System Description
5. Circuit Design
6. Code Implementation
7. Simulation Results
8. Hardware Design
9. Components Used
10. Challenges and Engineering Considerations
11. Conclusion

---

# 1. Introduction

This project focuses on designing a **microcontroller-based system for controlling the speed of a DC motor**. The system is implemented using an Arduino-based platform and a motor driver module to regulate motor speed through **Pulse Width Modulation (PWM)**.

The motor operates according to two predefined patterns that simulate **industrial motor control behavior**, including gradual acceleration, deceleration, and step-wise speed changes. The project demonstrates practical concepts in **embedded programming, motor control, and circuit design**.

The system was tested through simulation to verify correct speed variations and timing behavior.

---

# 2. Objectives

The primary objective of this project is to design and implement a **microcontroller-controlled DC motor system** capable of operating under defined speed patterns.

The system demonstrates:

• PWM-based motor speed control
• Embedded programming using a microcontroller platform
• Implementation of timed speed variations
• Simulation and verification of motor control behavior

This type of system is commonly used in **industrial automation, robotics, and motion control applications**.

---

# 3. Problem Description

The DC motor must operate according to **two predefined patterns**.

## Pattern 1

• Gradually increase motor speed to maximum within **1.5 minutes**
• Gradually decrease speed to zero within the next **1.5 minutes**
• Finally **turn OFF the motor**

This pattern demonstrates **smooth acceleration and deceleration control**.

---

## Pattern 2

• Motor runs at **slow speed for 30 seconds**
• Speed **doubles for the next 30 seconds**
• Speed **doubles again for the next 30 seconds**
• Then the speed **reduces in reverse order with the same time intervals**
• Motor finally **turns OFF**

This pattern demonstrates **step-wise motor speed control**.

---

# 4. System Description

The system consists of a **microcontroller, motor driver, DC motor, and power supply** working together to control motor speed and direction.

---

## Microcontroller

**Arduino Uno (ATmega328P)**

The Arduino Uno serves as the central controller responsible for generating PWM signals to regulate motor speed.

Key features:

• 8-bit microcontroller
• Multiple digital I/O pins
• 6 PWM output channels
• Easy programming using Arduino IDE

---

## Motor Driver

**L293N Dual H-Bridge Motor Driver**

The motor driver acts as an interface between the Arduino and the DC motor.

Functions:

• Allows higher current control
• Enables bidirectional motor control
• Accepts PWM signals for speed regulation

---

## DC Motor

A **12V brushed DC motor** is used in this system.

Characteristics:

• Continuous rotation
• PWM speed controllable
• Suitable for simulation and small automation systems

---

## Power Supply

The system uses:

• **12V external supply** for the motor
• **5V regulated supply** for the microcontroller logic

This ensures proper operation without damaging the controller.

---

## Software Tools

The following software tools were used:

• **Arduino IDE** – for programming and uploading code
• **Proteus Simulation Software** – for testing the circuit and verifying system behavior

---

# 5. Circuit Design

The circuit consists of the Arduino Uno connected to the motor driver module.

### Pin Connections

| Arduino Pin | Motor Driver Pin | Function          |
| ----------- | ---------------- | ----------------- |
| D9          | ENA              | PWM speed control |
| D13         | IN1              | Motor direction   |
| D12         | IN2              | Motor direction   |
| GND         | GND              | Common ground     |
| 5V          | VCC              | Logic supply      |

The PWM signal from Arduino controls the **duty cycle**, which directly affects motor speed.

---

# 6. Code Implementation

The motor control logic is implemented using Arduino code.

The program performs the following operations:

• Initializes motor control pins
• Generates PWM signals
• Executes Pattern 1 and Pattern 2
• Prints speed values to the serial monitor for monitoring

Key features of the implementation include:

• PWM-based speed control
• Timed delays for pattern execution
• Serial output for debugging and monitoring

---

# 7. Simulation Results

The system was simulated using **Proteus simulation software** to verify motor behavior.

## Pattern 1 Result

• Motor speed gradually increases to maximum during the first **1.5 minutes**
• Speed gradually decreases during the next **1.5 minutes**
• Motor stops after the cycle completes

This demonstrates **smooth ramp-up and ramp-down motor control**.

---

## Pattern 2 Result

The motor follows a step-based speed variation:

• Initial slow speed for **30 seconds**
• Speed doubles after **30 seconds**
• Maximum speed reached after **60 seconds**
• Speed then decreases step-by-step
• Motor turns **OFF at the end**

This pattern verifies the **correct implementation of timed speed levels**.

---

# 8. Hardware Design

The hardware implementation includes:

• Arduino Uno microcontroller
• L293N motor driver module
• 12V DC motor
• External power supply
• Connecting wires and supporting components

The design ensures safe interfacing between the **microcontroller logic (5V)** and **motor power (12V)**.

---

# 9. Components Used

| Component           | Specification           | Quantity |
| ------------------- | ----------------------- | -------- |
| Arduino Uno         | ATmega328P, 5V logic    | 1        |
| DC Motor            | 12V, 0.3A               | 1        |
| L293N Motor Driver  | Dual H-Bridge           | 1        |
| Power Supply        | 12V Adapter             | 1        |
| Wires and Resistors | As required             | —        |
| Simulation Tools    | Proteus and Arduino IDE | —        |

---

# 10. Challenges and Engineering Considerations

Several engineering considerations were addressed during the design process.

### Timing Precision

The system uses the `delay()` function to maintain timing intervals. For more advanced applications, **millis() based timing** could be implemented to enable non-blocking operation.

### PWM Speed Control

Arduino’s **analogWrite()** function provides PWM signals that control the duty cycle applied to the motor driver, allowing effective speed regulation.

### Voltage Compatibility

The DC motor requires **12V**, while the microcontroller operates at **5V logic levels**. The motor driver ensures proper interfacing between these two voltage domains.

### Simulation Debugging

Proteus simulation enabled visual verification of motor behavior, helping validate the timing patterns before hardware implementation.

---

# 11. Conclusion

The designed system successfully demonstrates **microcontroller-based DC motor speed control** using PWM techniques.

The project achieved the required operational patterns, including:

• Gradual acceleration and deceleration
• Step-wise speed variation
• Accurate timing control

Simulation results confirmed that the system performs as intended. This project provides practical experience in **embedded system design, motor control, and industrial automation concepts**.

The design can be further expanded for applications such as **robotics, conveyor systems, automated machinery, and smart motor control systems**.

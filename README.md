# VEX Robotics Team 1082U - Uforia

Welcome to the official repository for VEX Robotics Team 1082U "Uforia". This repository contains our custom C++ source code optimized for the VEX V5 ecosystem, featuring an updated chassis configuration, fully defined software limits, and optimized drivetrain motor operations.

---

## Robot Configuration

Our robot maps essential hardware inputs to specific ports and gear ratios on the V5 Brain:

| Subsystem | Component | Smart Port | Gear Ratio | Direction / Details |
| :--- | :--- | :--- | :--- | :--- |
| Drivetrain (Left) | leftMotorA / leftMotorB | Port 3 / Port 9 | 18:1 | Normal |
| Drivetrain (Right) | rightMotorA / rightMotorB | Port 11 / Port 17 | 18:1 | Inverted |
| Lift System | lift | Port 5 | 18:1 | Target control |
| Claw System | claw | Port 6 | 18:1 | Soft-limit constraints |

### Drivetrain Physical Specifications
* Wheel Track Width: 295 mm
* Wheel Circumference: 319.19 mm
* Wheel Base: 40 mm
* External Gear Ratio: 1:1

---

## Driver Controls & Mapping

The controls utilize standard Arcade Drive parameters paired with custom hardware logic triggers:

### Primary Movement
* Forward / Backward: Axis 3 (Left Joystick - Y-Axis)
* Turning: Axis 1 (Right Joystick - X-Axis)
* Speed Boost Mode: Hold Button L1. This scales up your base forward velocity inputs (`front`) and triggers a continuous rumble alert ("-") on the controller for physical driver feedback.

### Subsystem Manipulation
* Lift Up: Hold Button R1 (Stops automatically at a safe software cap of 90°)
* Lift Down: Hold Button R2 (Stops automatically at a safe software cap of 0°)
* Claw Actuate Open/Close: Button X (Forward spin up to 90°) / Button Y (Reverse spin down to 0°)

---

## Code Features & Architecture

* Direct Motor Spin Control: Utilizes explicit `.spin()` commands driven by raw RPM targets rather than relying on velocity setters, improving instantaneous drive response times.
* Initialized Boundary Limits: Explicitly resolves physical strain risks via software-defined limits (`minLiftDegree`, `maxLiftDegree`, `minClawDegree`, `maxClawDegree`) ensuring safe motor operation ranges.
* Dynamic Random Seed Generation: Leverages raw system uptime high-resolution metrics combined with battery current/voltage anomalies to create unpredictable `srand()` values on every boot.
* Custom V5 Macro Packaging: Integrated legacy support for `waitUntil` loops and structural iterative `repeat` triggers.

---

## Tech Stack & Environment

* Language: C++ (VEX C++ API)
* Target Hardware: VEX V5 Brain (1st Gen)
* SDK Version: 20240802.15.00.00
* VEXcode Application Version: 4.68.0

# ESP32 Stepper Motor Control

A self-contained prototype for a hanging kinetic sculpture. Five suspended wooden balls rise and fall through a phase-offset sine wave pattern, each driven by an independent NEMA 17 stepper motor and custom spool winch.

## Overview

The motion is generated directly on the ESP32 using the `AccelStepper` library. A sine function with phase offsets across the five motors creates a coordinated wave pattern. The system runs without a connected computer after the sketch is uploaded.

The winch mechanism uses off-the-shelf plastic thread spools attached to NEMA 17 motor shafts via flange couplings. No custom 3D printing required.

[YouTube Demo](https://youtu.be/g7hZ9SLusAE)

## Signal Flow

```
[ESP32] ---> (STEP/DIR) ---> [5x TMC2209] ---> (Phase Current) ---> [5x NEMA 17] ---> (Braided Line) ---> [5x Suspended Wooden Balls]
```

**Controller-generated motion.** The ESP32 computes the sine wave pattern directly and drives the motors through the TMC2209 drivers. No external software runs during operation.

**Quiet, continuous movement.** TMC2209 drivers run the motors with lower noise and smoother motion than basic stepper drivers. That matters for a sculpture meant to run continuously.

## Hardware

**ESP32-DevKitC-32E** microcontroller

**NEMA 17** stepper motors (one per winch)

**TMC2209** stepper drivers (one per motor)

**12 V power supply** (Mean Well LRS-100-12 recommended)

**Custom winch mechanisms** (see Winch Mechanism section below)

## Software

- **Arduino IDE** with the ESP32 board manager installed
- **Arduino library:** `AccelStepper` by Mike McCauley

## Setup

1. Connect each stepper motor to a TMC2209 driver. Connect STEP/DIR pins to the GPIO pins specified in the `.ino` file. Power the motors from the 12 V supply.
2. Open the `.ino` file in the Arduino IDE and upload it to the ESP32.
3. After a 10-second startup delay, the motors run a brief settling movement, then begin the continuous sine wave sequence.

## Winch Mechanism

Each winch uses a plastic thread spool attached to a NEMA 17 motor shaft via a 5mm flange coupling. The coupling bolts to the flat face of the spool with M3 screws. Braided fishing line ties to the spool, and a small eye hook attaches the wooden ball to the other end.

The goal was a mechanism that could be built and replicated without custom fabrication. These parts are all available off the shelf.

![Winch Components](winch-1.jpg)
![Winch Components](winch-2.jpg)
![Assembled Winch](winch-3.jpg)

### Bill of Materials (per winch)

| Part | Product Link | Notes |
| --- | --- | --- |
| **Stepper Motor** | NEMA 17 | Standard 5mm D-shaft |
| **Motor Shaft Coupler** | [5mm Flange Coupling](https://www.amazon.com/dp/B092Z7Q3X9) | Connects motor to spool |
| **Spool** | [2.64" Plastic Wire Spools](https://www.amazon.com/dp/B07X3Y2Z8J) | Winch drum |
| **Suspended Object** | [2-inch (50mm) Wooden Ball](https://www.amazon.com/dp/B089Q7XJ6Y) | Kinetic element |
| **Line** | [15lb Braided Fishing Line](https://www.amazon.com/dp/B07D37T6Y8) | Low stretch, high strength |
| **Fasteners** | M3 Screws & Nuts (included with coupler), [Small Eye Hooks](https://www.amazon.com/dp/B09C1Y2Z7X) | Assembly and line attachment |

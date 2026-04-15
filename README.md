# ELEVATOR-PROJECT
A fully automated, 3-story industrial elevator control system programmed with ladder logic on an Omron PLC, featuring selective collective control and hardware safety interlocks.

# Omron PLC Elevator Control System

## Overview
This project is a fully automated, industrial-grade ladder logic program designed to control a 3-story De Lorenzo elevator simulator using an Omron PLC. The software features selective collective control, dynamic memory routing, and hardware-integrated safety interlocks.

## Hardware & Software Stack
* **PLC:** Omron (Programmed via CX-Programmer)
* **Plant:** De Lorenzo Elevator Training Panel
* **I/O Voltage:** 24V DC (Sourcing Inputs / Sinking Outputs)

## Key Engineering Features
* **Selective Collective Control:** Utilizes memory latches (Channel 20) to store multiple simultaneous floor requests. The algorithm evaluates the current physical floor sensor against latched targets to determine motor direction, intelligently skipping lower-priority calls to service top-level calls first.
* **Master Arrival Flag:** A mathematically isolated stopping gate (Address 21.00) that fires the exact millisecond the target floor sensor is reached, cutting motor power instantly for perfect mechanical leveling.
* **Cross-Motor Safety Interlocks:** Normally-closed gates prevent the UP and DOWN contactors from ever firing simultaneously.
* **Hardware Safety Daisy-Chain:** The software monitors physical limit switches on all shaft and cabin doors. If any door is forced open, the software instantly drops the emergency brake and kills motor power.

## I/O Allocation
### Inputs (Sensors & Buttons)
* `0.00` - `0.02`: Floor 1-3 Call Buttons
* `0.03` - `0.05`: Floor 1-3 Proximity Sensors
* `0.06` - `0.07`: Cabin Door Limit Switches (Open/Closed)

### Outputs (Motors & Brakes)
* `11.00` / `11.02`: Main Hoist Motors (UP/DOWN)
* `10.02`: Emergency Mechanical Brake
* `10.03` - `10.10`: Cabin and Shaft Door Automated Actuators

## Viewing the Code
Since `.cxp` files require Omron CX-Programmer to view, I have included a full `Ladder_Logic_Printout.pdf` in the repository for easy reading of the network rungs.

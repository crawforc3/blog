---
title: Autonomous Rover Build
tags: [project, robotics, ardupilot]
---

# Autonomous Ground Vehicle

An ongoing project building an autonomous ground vehicle capable of GPS waypoint navigation across varied suburban terrain.

![CAD render of the rover design](images/2025-11-final-rover-assembly-perspective.png)

## Skills Demonstrated

- **Mechanical Design:** CAD modeling, Ackerman steering geometry, drivetrain layout, 3D printed component design
- **Fabrication:** Aluminum frame construction, 3D printing (PLA/TPU), wiring harness assembly
- **Embedded Systems:** ArduPilot configuration, ESC/servo integration, RC systems
- **Software:** Onshape CAD, QGroundControl, ArduPilot firmware

## Project Requirements

| Requirement | Specification |
|-------------|---------------|
| Payload capacity | 10 lbs |
| Target speed | ~3 mph |
| Terrain | Paved surfaces, sidewalks, curbs, grass, mild grades |
| Navigation | GPS waypoint autonomy via ArduPilot |
| Operating range | Multi-kilometer |

## Technical Specifications

| System | Component | Details |
|--------|-----------|---------|
| Frame | 2020 aluminum extrusion | 24" x 18" bolted frame |
| Drivetrain | Brushed DC motors | Dual HOBBYWING QUICRUN 1080 G2 ESCs, 540 40T motors |
| Steering | Ackerman geometry | Zoskay DS3235 servo (35kg-cm torque) |
| Flight controller | SpeedyBee F405 WING | STM32F405 @ 168MHz, ArduPilot Rover firmware |
| GPS | Matek M10Q-5883 | GPS + magnetometer module |
| Power | Dual 3S LiPo | 15000mAh each, 333Wh total capacity |
| Wheels | Custom 3D-printed | 17cm diameter, 6.5cm width, 6000RS bearings |
| RC | ExpressLRS | Radiomaster TX12 MKII transmitter, BetaFPV SuperD receiver |

## Design Decisions

### Ackerman Steering Geometry

Selected Ackerman steering over skid-steer to provide proper turning geometry where the inside wheel turns at a sharper angle than the outside wheel. This reduces tire scrub, improves low-speed maneuverability, and integrates cleanly with ArduPilot's rover steering control (GroundSteering servo function).

### Brushed vs Brushless Motors

Selected brushed DC motors for this application. At the target speed of 3 mph, brushed motors provide adequate performance with simpler control characteristics and better low-speed torque control compared to sensored brushless alternatives.

### Wheel Design

Custom 17cm diameter wheels designed to clear standard curbs while maintaining a low center of gravity. 6000RS bearings selected for their deeper groove profile, providing better radial load capacity than standard 608 skateboard bearings.

## Build Progress

### Frame and Body

![Completed aluminum frame](images/2025-11-11-complete-2020-aluminum-frame-assembly.jpg)

24" x 18" frame constructed from 2020 T-slot aluminum extrusion. T-slot provides a modular, adjustable platform for mounting components and iterating on layout. Joints use M6 tapped holes and T-nuts for secure fastening.

### Powertrain

Dual HOBBYWING QUICRUN 1080 G2 ESCs driving 540 40T brushed motors. Power transmission uses flexible couplers from motor shafts to 10mm aluminum axles. Wheel assemblies use 6000RS bearings with optimized clearance fits (9.98mm shafts in 10mm bore) for smooth rotation.

### Steering

3D-printed steering knuckles implement Ackerman geometry with a Zoskay DS3235 waterproof servo providing 35kg-cm torque. The servo mount required multiple design iterations to achieve proper fit, accounting for servo body dimensions, screw hole tolerances, and wire routing clearance.

### Wheels and Tires

![All four wheels and tires](images/2025-09-21-multiple-wheels-and-tires-laid-out.jpg)

Custom 3D-printed wheels (17cm diameter, 6.5cm width) with hex hub mounting. Wheels printed in PLA, tires in TPU for flexibility. 6000RS bearings press-fit into wheel hubs.

### Electronics

SpeedyBee F405 WING flight controller running ArduPilot Rover firmware. Matek M10Q-5883 provides GPS and compass. ExpressLRS protocol via BetaFPV SuperD receiver for RC control. Power from dual 3S LiPo batteries (15000mAh each, 166.5Wh per battery).

ArduPilot configuration uses SERVO functions: throttle (70) for both drive motors, GroundSteering (26) for the steering servo. Roll channel on the transmitter maps to steering input in rover mode.

## Current Status

![Current rover state](images/current-status.jpg)

<video controls width="100%">
  <source src="images/VID_20251209_151820062.mp4" type="video/mp4">
</video>

Current focus is on electronics integration and validating RC control before implementing autonomous navigation. Components are subject to iteration as testing reveals needed improvements.

## Tools & Software

- **CAD:** Onshape
- **Slicing:** PrusaSlicer
- **Mission Planning:** QGroundControl
- **Firmware:** ArduPilot Rover

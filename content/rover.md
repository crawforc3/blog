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
| Frame | 2020 aluminum extrusion | 24" x 18" custom welded/bolted frame |
| Drivetrain | Brushed DC motors | Dual HOBBYWING QUICRUN 1080 G2 ESCs, 540 40T motors |
| Steering | Ackerman geometry | Zoskay DS3235 servo (35kg-cm torque) |
| Flight controller | SpeedyBee F405 WING | STM32F405 @ 168MHz, ArduPilot Rover firmware |
| GPS | Matek M10Q-5883 | GPS + magnetometer module |
| Power | Dual 3S LiPo | 15000mAh each, 333Wh total capacity |
| Wheels | Custom 3D-printed | 17cm diameter, 6.5cm width, 6000RS bearings |
| RC | ExpressLRS | Radiomaster TX12 MKII transmitter, BetaFPV SuperD receiver |

<!-- TODO: Add measured specs once available:
- Total vehicle weight
- Ground clearance
- Turning radius
- Estimated runtime at cruise speed
- Max grade capability
-->

## Design Decisions

### Ackerman Steering Geometry

<!-- TODO: Add rationale - why Ackerman over skid steer or differential?
Likely: better tire wear, more natural turning, works well with ArduPilot rover mode -->

Selected Ackerman steering to provide proper turning geometry where the inside wheel turns at a sharper angle than the outside wheel, reducing tire scrub and improving low-speed maneuverability.

### Brushed vs Brushless Motors

Selected brushed DC motors for this application. At the target speed of 3 mph, brushed motors provide adequate performance with simpler control characteristics and better low-speed torque control compared to sensored brushless alternatives.

<!-- TODO: Add more detail on motor selection criteria, torque calculations -->

### Wheel Design

Custom 17cm diameter wheels were designed to provide sufficient ground clearance for curb transitions while maintaining a low center of gravity.

<!-- TODO: Add:
- Ground clearance measurement
- Why 17cm specifically (curb height + clearance margin?)
- TPU tire durometer/flexibility choice
- Bearing selection rationale
-->

## Build Progress

### Design Phase (September 2025)

![Early concept sketches](images/2025-09-early-rover-concept-sketches.jpg)

Initial design work in Onshape, establishing frame dimensions, wheel placement, and component layout. Key early decisions included frame material selection and steering geometry.

### Electronics Integration (September 2025)

Bench testing of the electronics stack: ESCs, steering servo, flight controller, and power distribution. Verified basic functionality before mechanical integration.

Initial ArduPilot configuration required understanding the mapping between RC channels, SERVO outputs, and the Rover firmware's expectations for throttle and steering control.

### 3D Printed Components (September 2025)

![All four wheels and tires laid out](images/2025-09-21-multiple-wheels-and-tires-laid-out.jpg)

Printed wheel and tire assemblies:
- Wheels: PLA (~5 hours each)
- Tires: TPU (~5 hours each)
- Total filament: ~1000g

### Frame Fabrication (November 2025)

![Completed aluminum frame](images/2025-11-11-complete-2020-aluminum-frame-assembly.jpg)

Cut and assembled the 2020 aluminum extrusion frame. Drilled and tapped M6 threads for fastening. Verified frame squareness by measuring diagonals.

![Frame with wheels mockup](images/2025-11-11-frame-with-wheels-mockup.jpg)

### Servo Mount Iteration (November 2025)

The steering servo mount required four design iterations:

1. Initial design had insufficient clearance for servo body
2. Screw hole diameter incorrect (designed for head OD vs shank)
3. No clearance for servo wiring
4. Final design: open-sided mount allowing lateral insertion

This process reinforced the importance of prototyping with actual components rather than relying solely on datasheet dimensions, and designing for assembly sequence including cable routing.

## Current Status

![Current rover state with servo and motor mounts](images/2025-11-21-rover-frame-with-servo-and-motor-mounts.jpg)

Mechanical assembly is largely complete. Current work is focused on electronics integration and validating RC control before implementing autonomous navigation.

**Completed:**
- Frame fabrication
- Drivetrain mechanical assembly
- Steering linkage
- Component mounting

**In Progress:**
- Wiring and power distribution
- ArduPilot configuration
- RC control validation

**Planned:**
- GPS waypoint navigation testing
- Autonomous mission execution

## Tools & Software

- **CAD:** Onshape
- **Slicing:** PrusaSlicer
- **Mission Planning:** QGroundControl
- **Firmware:** ArduPilot Rover

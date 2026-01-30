---
title: Autonomous Rover Build
tags: [project, robotics, ardupilot]
---

# Autonomous Rover Build

Building a self-driving unmanned homebrew ground vehicle because I'm the neighborhood's best neighbor (self-proclaimed).

I brew great beer and share it with everyone in Seattle. My neighbors give me eggs, fresh bread, sometimes vegetables. It's a beautiful barter economy. But walking beer over is inefficient. So naturally, the solution is to build an autonomous rover that can do it for me.

The body panels are inspired by ED-209 from RoboCop—because if you're going to build a delivery robot, it might as well look intimidating.

## Technical Specs

| Component | Details |
|-----------|---------|
| **Frame** | Custom 24" x 18" aluminum 2020 T-slot extrusion |
| **Drivetrain** | 2-wheel drive, dual HOBBYWING QUICRUN 1080 G2 ESCs with 540 40T brushed motors |
| **Steering** | Ackerman geometry with Zoskay DS3235 waterproof servo (35kg torque) |
| **Brains** | SpeedyBee F405 WING (STM32F405 @ 168MHz) running ArduPilot firmware |
| **Navigation** | Matek M10Q-5883 GPS + compass module |
| **Power** | Dual 3S LiPo batteries (15000mAh each, 333Wh total) |
| **Wheels** | Custom 3D-printed PLA (17cm diameter, 6.5cm wide, 6000RS bearings) |
| **Control** | Radiomaster TX12 MKII with ExpressLRS, BetaFPV SuperD receiver |

## Requirements

- **Payload:** 10 pounds (enough for a growler or two)
- **Speed:** ~3 mph (walking pace)
- **Terrain:** Seattle neighborhood streets, sidewalks, curbs, grass, mild hills
- **Autonomy:** GPS waypoint navigation via ArduPilot
- **Range:** Multi-kilometer (anywhere in the neighborhood)

## Budget

Started with "maybe $300?" Ended up around $800.

| Category | Cost |
|----------|------|
| Aluminum frame | $40 |
| Motors & ESCs | $120 |
| Steering servo | $30 |
| Flight controller | $50 |
| GPS module | $40 |
| Batteries (2x) | $80 |
| Transmitter & receiver | $100 |
| 3D printing filament | $50 |
| Bearings, bolts, hardware | $50 |
| **Parts subtotal** | **$560** |
| Tools (saw, blade, taps, etc.) | ~$200 |
| **Total** | **~$800** |

## Build Log

### Design Phase (September 2025)

Started designing in Onshape (browser-based CAD, works on Debian). Went with brushed motors instead of brushless—simpler, easier to control, saved $100-200 on budget.

Key decisions:
- Custom 17cm 3D-printed wheels for curb clearance
- Ackerman steering geometry (inside wheel turns sharper than outside)
- 2020 aluminum T-slot extrusion frame—like adult LEGO

### Electronics Test (September 16, 2025)

First bench test: wired up ESCs, servo, and batteries. Nothing caught fire. The SpeedyBee F405 flight controller is tiny and terrifying.

### ArduPilot Configuration (September 17-19, 2025)

Three days of madness:
- Forgot to arm the rover
- Confused Motor1 with Throttle
- Learned that "Roll" controls steering on a ground vehicle
- QGroundControl on Debian (Mission Planner is Windows-only)

### 3D Printing (September 20-23, 2025)

Printed all four wheels and tire assemblies:
- Wheels: PLA, ~5 hours each
- Tires: TPU, ~5 hours each
- All prints successful, no failures
- ~1000g filament total

### Motor Assembly (October 15, 2025)

Assembled steering servo and tested on bench. Digital servos are impressive—35kg of torque in a tiny package.

### Steering Linkage (October 25, 2025)

Learned Ackerman steering geometry the hard way. 3D printed steering knuckles and servo mounts. Everything fit first try.

### Tool Acquisition (November 2, 2025)

Got a Ryobi miter saw and aluminum blade off Craigslist. Spent as much on tools as parts at this point.

### Cutting Aluminum (November 10, 2025)

Cutting aluminum is easier than expected. Brother helped with the cuts.

### Frame Assembly (November 11, 2025)

Drilled and tapped M6 threads into aluminum with a hand drill. Holes were "barely serviceable" but functional. Frame came together square—both diagonals measured the same.

Tools used:
- Hand drill (no drill press)
- M6 tap from tap and die set
- Many clamps
- Multiple 250-piece metric screw assortment packs

### Wiring Harnesses (November 14-15, 2025)

A week in connector hell. JST connectors, custom wiring harnesses, tiny pins lost on the garage floor. Used pre-crimped wires for test harnesses.

### Final Assembly (November 18, 2025)

Attached steering servo and both drive motors to frame. Starting to look like an actual rover.

### Servo Mount (November 21, 2025)

The servo mount that took four tries:
1. Servo body 0.5mm too big for pocket
2. Screw holes too big (designed for heads not shanks)
3. Forgot about the wire coming out
4. Just removed one entire side—simple solution

Lessons learned:
- Measure the actual part, not the datasheet
- Account for wires, connectors, everything
- M3 screws need 3.2mm holes, not 3.5mm
- CAD is too perfect—reality is messier

## Current Status

- **Completed:** Frame, drivetrain, steering geometry, component procurement
- **In Progress:** Electronics integration, power distribution, flight controller config
- **Next:** Remote control testing, GPS navigation, autonomous features

## Tools & Software

- **CAD:** Onshape (browser-based, works on Linux)
- **Mission Planning:** QGroundControl on Debian
- **Firmware:** ArduPilot

---

*Built with determination, caffeine, and occasional profanity | 2025*

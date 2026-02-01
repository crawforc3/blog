---
title: Autonomous Rover Build
tags: [project, robotics, ardupilot]
---

# Autonomous Ground Vehicle

I'm building a rover that can navigate my neighborhood autonomously. GPS waypoints, curb climbing, the whole deal. The goal is to deliver homebrew to my neighbors without me having to walk it over myself. I make beer, they get beer, everybody wins. Except now I have to build a robot.

Here's the thing about building robots: you don't just learn one skill. You learn twelve. I started this project knowing how to write software. Now I'm doing CAD modeling, Ackerman steering geometry, aluminum fabrication, 3D printing in multiple materials, ArduPilot configuration, and spending way too much time thinking about gear ratios. Each problem solved reveals three more problems I didn't know existed.

This page documents the build. Components are subject to change as I break things and figure out better approaches.

![CAD render showing a four-wheeled rover with aluminum frame, large knobby tires, and a rectangular electronics enclosure mounted on top](images/2025-11-final-rover-assembly-perspective.png)
*CAD render of the current design*

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

I went with Ackerman steering instead of skid-steer. The inside wheel turns sharper than the outside wheel during a turn, which is how actual cars work. Skid-steer would've been simpler mechanically, but it tears up the tires and fights ArduPilot's steering logic. Ackerman plays nice with the GroundSteering servo function and doesn't leave rubber all over my driveway.

### Brushed vs Brushless Motors

Brushed motors. I know, I know. Brushless is more efficient. But at 3 mph, efficiency doesn't matter. What matters is smooth low-speed control, and brushed motors do that without needing sensored feedback or fancy ESC tuning. They're also cheaper, and I've already spent enough on this project.

### Wheel Design

The wheels need to climb curbs. Standard curbs are about 15cm, so I designed 17cm diameter wheels to clear them with some margin. I went with 6000RS bearings instead of the cheaper 608 skateboard bearings because the deeper groove handles radial loads better. When you're carrying 10 pounds of beer over rough terrain, you want bearings that won't complain.

## Build Progress

### Frame and Body

The frame is 2020 T-slot aluminum extrusion, 24" x 18". It's basically adult LEGO. I can move things around, drill new holes, and adjust the layout without starting over. The joints use M6 tapped holes. I learned to tap threads into aluminum, which is more satisfying than it has any right to be.

![Several lengths of silver 2020 aluminum extrusion laid out on a workbench](images/2025-11-10-cut-aluminum-2020-frame-pieces.jpg)
*Cut 2020 extrusion pieces before assembly*

![Hand holding a tap tool inserted into aluminum extrusion, cutting threads into the end](images/2025-11-11-tapping-threads-in-aluminum-frame.jpg)
*Tapping M6 threads by hand*

![Rectangular aluminum frame on garage floor with four large black wheels placed at the corners](images/2025-11-11-frame-with-wheels-mockup.jpg)
*First mockup with wheels placed for sizing*

![Aluminum frame with white 3D-printed motor mounts and steering components attached](images/2025-11-21-rover-frame-with-servo-and-motor-mounts.jpg)
*Frame with steering and motor mounts installed*

### Powertrain

Two motors, two ESCs, one dream. The HOBBYWING QUICRUN 1080 G2 ESCs drive 540 40T brushed motors. Getting power from the motor shafts to the wheels required flexible couplers. Rigid connections would bind up with any misalignment, and there's always misalignment. The bearings are 6000RS with a 10mm bore, and I spent way too long getting the shaft diameter right. 9.98mm fits a 10mm bore smoothly. 10.02mm does not.

![White 3D-printed motor mount with silver flexible coupler connecting motor shaft to axle](images/2025-09-19-3d-printed-wheel-hub-with-motor-mount.jpg)
*Early motor mount prototype with flexible coupler*

![Motor mounted in white 3D-printed housing with bearing block on workbench](images/2025-10-25-bearing-housing-with-servo-mount.jpg)
*Testing the bearing housing and motor alignment*

![Complete assembly showing motor, coupler, bearing housing, and black wheel with tire attached](images/2025-09-28-complete-wheel-motor-test-assembly.jpg)
*Complete drivetrain assembly with wheel attached*

The initial test drive was humbling. The rover couldn't drive over a small power cord in the garage. When I pushed throttle to the max, one of the motors started smoking. That's when I knew I couldn't get away from learning about gears and gear boxes. I designed a 2-stage gearbox that gives a 40:1 reduction. There are way cooler gear assemblies out there, but this one is mine.

![White 3D-printed gearbox with two gear stages visible, showing large and small spur gears](images/2026-01-2-stage-gearbox-40-1-reduction.jpg)
*2-stage gearbox providing 40:1 reduction*

<video controls width="100%">
  <source src="images/2026-01-gearbox-motor-test.mp4" type="video/mp4">
</video>
*Gearbox bench test with motor*

### Steering

The steering knuckles are 3D-printed and implement Ackerman geometry. A Zoskay DS3235 servo provides 35kg-cm of torque, which is enough to turn the wheels even when the rover is sitting still on pavement.

The servo mount took four tries to get right. First one didn't fit the servo. Second one had screw holes that were too big. Third one didn't account for the wire coming out of the servo. Fourth time I just removed one side of the mount entirely so the servo could slide in from the side. Sometimes the simple solution is the one you should've tried first.

![Four white 3D-printed servo mounts arranged in a row showing design progression](images/2025-11-21-servo-mount-failed-prototypes.png)
*Four iterations of servo mounts before getting it right*

![White 3D-printed steering knuckle attached to aluminum frame rail](images/2025-10-25-steering-knuckle-prototype-on-frame.jpg)
*Steering knuckle mounted to the frame*

![Small white 3D-printed cylindrical sleeve that fits over servo splines](images/2025-11-servo-arm-sleeve.jpg)
*Custom servo arm sleeve for the steering linkage*

![Blue servo motor installed in white mount with custom steering arm attached](images/2026-01-steering-servo-mount-and-arm.jpg)
*Servo installed with mount and custom arm*

![Top view of steering linkage showing tie rods connecting servo to both front knuckles](images/2026-01-steering-linkage-assembly.jpg)
*Steering linkage*

### Wheels and Tires

I printed my own wheels. 17cm diameter, 6.5cm wide, with a hex hub interface so they pop on and off easily. The wheels are PLA, rigid enough to hold their shape. The tires are TPU, which is flexible and grippy. Press-fitting 6000RS bearings into PLA hubs requires getting the hole diameter exactly right. Too tight and the bearing won't go in. Too loose and it falls out. I got it right eventually.

![White PLA wheel hub sitting on 3D printer bed with honeycomb infill pattern visible](images/2025-09-19-wheel-hub-on-printer-bed.jpg)
*PLA wheel hub fresh off the printer*

![Several wheel hubs and black TPU tires spread out on workbench for test fitting](images/2025-09-21-multiple-wheels-and-tires-laid-out.jpg)
*Tire fit on wheel prototype*

![Two completed wheels with white hubs and black knobby tires side by side](images/2025-09-23-two-complete-wheel-assemblies.jpg)
*Final wheels and tires*

### Electronics

The brain is a SpeedyBee F405 WING running ArduPilot Rover firmware. It's a flight controller, but ArduPilot doesn't care that I'm on the ground. GPS comes from a Matek M10Q-5883 module with a built-in compass. RC control uses ExpressLRS protocol. Low latency, good range, and if I mess up the autonomous navigation I can take over manually.

Power is two 3S LiPo batteries, 15000mAh each. That's 333Wh total, which should be enough to deliver a lot of beer before needing a recharge. Laying everything out on the garage floor helped me figure out what size enclosure I'd need.

![Batteries, ESCs, and wiring spread out on concrete garage floor for sizing](images/2025-10-31-power-distribution-batteries-and-escs.jpg)
*Planning the electronics layout on the garage floor*

![White 3D-printed enclosure with brass heat-set inserts visible in mounting holes](images/2025-12-electronics-enclosure-heat-inserts.jpg)
*Enclosure with heat inserts installed*

Inside the enclosure, I designed caddies for the batteries, flight controller, and ESCs. Each component velcro-straps to a caddy, and the caddies screw into the enclosure where I added heat inserts. It keeps everything modular and easy to swap out when I inevitably fry something.

![Inside of enclosure showing white 3D-printed trays holding batteries and electronics with velcro straps](images/2025-12-electronics-caddies-detail.jpg)
*Enclosure with batteries and ESCs installed in caddies*

ArduPilot configuration was its own adventure. I spent three days figuring out that "Roll" controls steering in rover mode, not "Yaw" like you'd expect. The motors use SERVO function 70 (throttle), and steering uses function 26 (GroundSteering). Now it makes sense. At the time, it did not.

![Rover frame with steering linkage, motors, and electronics box assembled but no wheels attached](images/2025-11-dry-fit-steering-powertrain-enclosure.jpg)
*Dry fit of major components without wheels*

## Current Status

Right now I'm working on the gearbox design. The smoking motor incident made it clear I need that 40:1 reduction. But of course, the gearbox output isn't level with the drive axles, so I'll need to redesign all the motor mounts too. Given my track record with this project, something will always need to be redesigned. That's fine. That's how this works.

![Assembled rover with all four wheels, steering, and electronics enclosure on garage floor](images/current-status.jpg)
*Current state of the build*

<video controls width="100%">
  <source src="images/VID_20251209_151820062.mp4" type="video/mp4">
</video>
*Test drive before the gearbox redesign*

## Tools & Techniques

| Area | Tools & Skills |
|------|----------------|
| Mechanical Design | CAD modeling, Ackerman steering geometry, drivetrain layout, bearing selection |
| Fabrication | Aluminum frame construction, 3D printing (PLA/TPU), wire routing |
| Embedded Systems | ArduPilot configuration, ESC/servo integration, RC systems |
| Software | Onshape, PrusaSlicer, QGroundControl, ArduPilot Rover |

## See Also

- [[rover-cad|CAD Models]] - Onshape renders and design views
- [[rover-notes|Design Notes and Calculations]] - Hand-drawn sketches and calculations

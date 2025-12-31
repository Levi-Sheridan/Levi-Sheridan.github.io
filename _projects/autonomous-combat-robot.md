---
layout: page
title: Autonomous Combat Robot
description: First-place autonomous combat robot with custom spring-retention launcher
img: assets/img/drbones/drbones_thumbnail.jpg
importance: 2
category: work
toc:
  sidebar: left
---

<style>
h2 {
  font-weight: 700 !important;
}
</style>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/drbones/hero.jpg" title="Autonomous combat robot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

This autonomous combat robot was designed for Cooper Union's Robot Tank Battle competition. As Hardware Lead working alongside Software Lead Ariel Tamayev, I developed all mechanical systems, selected components, and integrated the hardware over 14 weeks. The robot won 1st place with a 3-0-1 record.

## Competition Overview

**Objective:** Autonomous robots score points by shooting 40mm ping pong balls at opponent robots (20 pts) and home bases (10 pts). Robots navigate a 10ft × 6ft arena with obstacles, detect infrared targets, engage opponents, and autonomously return to base for reloading.

**Constraints:**
- Maximum dimensions: 12" × 12" × 10"
- Single projectile capacity
- Autonomous operation (no human control during rounds)
- -10 point penalties for obstacle collisions and friendly fire

## My Contributions

- **Complete mechanical design:** CAD modeling and fabrication of chassis, drivetrain, and weapon system
- **System architecture:** Component selection (Mecanum drivetrain, motors, sensors, controllers, power systems)
- **Custom spring-retention launcher:** High-energy-density design with repeatable 8 m/s launch performance
- **Sensor integration:** Strategic placement and hardware-software interface definition for LiDAR and IR camera
- **PID tuning:** Precise wheel speed control for omnidirectional navigation
- **Hardware debugging:** Iterative optimization throughout testing and competition

**Partner's Contributions:** Python control system, LiDAR processing, obstacle avoidance algorithms, camera-based target detection

## Key Results

- **1st Place:** 3-0-1 competition record
- **Real-time optimization:** Mid-competition firing range adjustment (1200mm → 1600mm) improved targeting performance
- **Reliable autonomous operation:** Successful target acquisition, navigation, and return-to-base throughout tournament

---

## System Architecture

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/system-overview.jpg" title="System architecture overview" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The robot integrates mechanical, electrical, and software systems to autonomously navigate a contested arena, detect infrared targets, avoid obstacles, and engage opponents within strict size and power constraints.

**Core Systems:**
- **Mecanum drivetrain:** Four independently-controlled motors enable omnidirectional translation (strafing in any direction without rotation)
- **Sensor suite:** 360° LiDAR for obstacle detection, modified IR camera for target acquisition
- **Spring-retention launcher:** Dual-servo mechanism with wave disc springs for high energy density
- **Dual battery system:** Separate power for motors (12V NiMH) and electronics (5V USB-C power bank)
- **Raspberry Pi 4B:** Central controller managing sensor processing, motor control, and autonomous decision-making

---

## Chassis Design

### Drivetrain

<div class="row">
    <div class="col-md-6 mt-3">
        <p>Four 80mm Mecanum wheels, each driven by a 12V 40 RPM geared brushed DC motor, enable omnidirectional translation—forward, backward, and lateral strafing—without rotation. This maintains weapon alignment during combat and simplifies obstacle navigation by eliminating orientation tracking complexity.</p>
        
        <p>The chassis integrates 6 laser-cut acrylic panels with 9 3D-printed components, assembled using metric screws and heat-set threaded inserts. Component positioning optimizes weight distribution and accessibility: cannon mounts to front panel and bottom plate, LiDAR and Raspberry Pi mount on standoffs above battery tunnel, motor controllers positioned in wheel wells.</p>
    </div>
    <div class="col-md-6 mt-3">
        {% include figure.liquid path="assets/img/drbones/drivetrain-iso.jpg" title="Drivetrain without cover" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Chassis Views

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/chassis-top.jpg" title="Top view (structure, motors, wheels)" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/chassis-bottom.jpg" title="Bottom view" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Interior Layout

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/interior.jpg" title="Interior layout with lid removed (front at top, rear at bottom)" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Cannon occupies center front, flanked by camera module (left) and speakers (right). LiDAR mounts on standoffs atop battery tunnel at mid-chassis, with beacon platform above. Motor drivers positioned in wheel wells, Raspberry Pi mounts to rear battery tunnel. Rear access hatch provides battery access.

---

## Spring-Retention Launcher

The launcher is the core mechanical innovation—a dual-servo spring-retention mechanism that achieves high energy density in a compact footprint while delivering consistent 8 m/s projectile velocity.

### Design Overview

<div class="row">
    <div class="col-md-6 mt-3">
        <p>The launcher consists of four 3D-printed components, two MG959 servos, stacked wave disc springs, and a 6mm linear rod with bearing. Stacked wave disc springs provide higher energy storage per unit volume compared to conventional coil springs, enabling compact design within the robot's 12" footprint.</p>
        
        <p>Two servos actuate rotating latches that retain a bearing-guided plunger against the compressed spring. Upon servo rotation, the latches release, allowing the spring to drive the plunger forward and strike the projectile. The linear bearing constrains plunger motion to a single axis, ensuring consistent strike velocity and launch repeatability.</p>
    </div>
    <div class="col-md-6 mt-3">
        {% include figure.liquid path="assets/img/drbones/launcher-iso.jpg" title="Launcher assembly" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Mechanism Operation

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/launcher-cross-section.jpg" title="Launcher cross-section: unloaded (left) and loaded (right)" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Cross-section shows unloaded (left) and loaded (right) states. In the unloaded state, servos are open and the spring is relaxed. In the loaded state, the plunger compresses the spring and the servos close to retain it.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/plunger-latch.jpg" title="Plunger and rotating latch system" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

When open (left), the plunger slides freely past the latches. When closed (right), the latches block the plunger, retaining the compressed spring until firing command.

### Design Iterations & Problem Solving

**Challenge 1: Servo Torque Limitation**

Initial servo selection proved insufficient—once the spring was compressed and retained, friction forces on the latches prevented servo rotation and spring release. Progressive servo sizing through bench testing led to the selection of MG959 servos, which provided adequate torque to overcome the retention friction and reliably trigger the mechanism.

**Challenge 2: Structural Failure**

The barrel front plate experienced shearing failure where the plunger stop attached. Impact forces during rapid deceleration exceeded the material strength of the initial design. Iterative testing with increased wall thickness and infill density, combined with a material change from PLA to PETG, resolved the structural failure. An integrated impact damper was added to the plunger stop interface to distribute deceleration forces and prevent stress concentration.

**Challenge 3: Launch Optimization**

The final optimization positioned the projectile 5mm before the plunger's full extension, allowing the plunger to accelerate to maximum velocity before impact, thereby maximizing momentum transfer to the projectile and achieving consistent 8 m/s launch velocity.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/ball-launcher-detail.jpg" title="Projectile positioning for optimal momentum transfer" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Technical Drawings

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/launcher-housing-drawing.jpg" title="Launcher housing technical drawing" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/launcher-plunger-drawing.jpg" title="Plunger assembly" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/launcher-latch-drawing.jpg" title="Servo latch mechanism" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Camera Module

<div class="row">
    <div class="col-md-6 mt-3">
        <p>A custom camera module houses an Arducam 1080P Day & Night Vision USB camera (2MP, 138° diagonal FOV) modified for infrared-only detection. The automatic IR-cut filter was removed and replaced with four layers of polarized film to filter out non-infrared light, enabling autonomous target acquisition of IR LED beacons on opponent robots and home bases.</p>
        
        <p>The 3D-printed housing mounts internally to the front panel with the lens sitting flush with the robot's exterior, maintaining the 12" dimensional constraint while providing unobstructed field of view.</p>
    </div>
    <div class="col-md-6 mt-3">
        {% include figure.liquid path="assets/img/drbones/camera-module.jpg" title="Camera module with IR filter integration" class="img-fluid rounded z-depth-1 mb-3" %}
        {% include figure.liquid path="assets/img/drbones/camera-module-section.jpg" title="Camera module cross-section" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/front-panel.jpg" title="Front panel with flush-mounted camera and launcher" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Electrical Systems

### Motor Control

Two DROK L298 H-Bridge Motor Speed Controllers drive the four motors, with each driver controlling two motors independently via three GPIO pins per motor (direction: IN1/IN2, speed: PWM enable pin). Driver boards powered at 3.3V to match Raspberry Pi GPIO logic levels—5V operation would prevent signal recognition and cause control failures.

### Power Architecture

Dual battery system: 12V 5000mAh NiMH battery powers drive motors (5A standard discharge, 10A max continuous). Nitecore NB10000 USB-C power bank (10,000mAh, 5V, 3A) powers Raspberry Pi 4B and all connected sensors and peripherals (LiDAR, camera, servos).

### Sensor Suite

- **Slamtec RPLiDAR A1M8:** 360° obstacle detection, 5.5Hz scan rate, 0.5mm distance resolution, 1° angular resolution
- **Modified Arducam camera:** IR-only target detection via polarized filter stack
- **Raspberry Pi 4B:** Central controller with GPIO motor control, USB 3.0 sensor interfaces

---

## Competition Performance

The robot won 1st place with a 3-0-1 record, demonstrating effective autonomous navigation, target acquisition, and opponent engagement throughout the tournament.

### Mid-Competition Optimization

Analysis between rounds revealed the robot was acquiring targets beyond its programmed firing range (1200mm). Increasing the engagement threshold to 1600mm improved performance in subsequent matches with no adverse effects, demonstrating the value of real-time parameter optimization under competition conditions.

### Results

**Strengths:**
- IR camera system reliably detected targets with minimal false triggers
- Autonomous navigation and return-to-base functionality performed consistently
- Launcher achieved repeatable 8 m/s projectile velocity throughout competition
- Successfully hit opponent bases and engaged fielded robots

**Challenges Encountered:**

*PID Controller Failure:* Days before competition, the back-left motor controller's PWM enable pin failed—any positive duty cycle was interpreted as 100%, preventing speed modulation. Rather than operate with asymmetric control, we abandoned PID entirely and operated all motors at fixed duty cycles (100%, 0%, or -100%), accepting reduced directional precision.

*Obstacle Avoidance Limitations:* LiDAR-based obstacle avoidance effectively handled frontal obstructions but struggled with lateral obstacles during strafing maneuvers, resulting in occasional collision penalties. The reactive algorithm changed direction for each individual LiDAR point, causing jittery motion that a 0.3-second hold time partially mitigated.

### Potential Improvements

- **Gyroscope integration:** Floor obstacles caused unintended rotational drift. A gyroscope would provide continuous angular position feedback for closed-loop heading control
- **Improved target detection:** Requiring a cluster of high-brightness pixels (100+) instead of single-pixel threshold would reduce false positives from reflections and ambient light
- **Scan aggregation:** Aggregating multiple consecutive LiDAR scans to identify persistent obstacles would enable smoother trajectory planning

<script>
document.addEventListener('DOMContentLoaded', function() {
  mediumZoom('img:not(.emoji)');
});
</script>

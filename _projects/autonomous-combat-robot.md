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

**Design Walkthrough Video:**

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        <iframe width="100%" height="480" src="https://www.youtube.com/embed/FWer01zHNTw" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</div>

This autonomous combat robot was designed for Cooper Union's Robot Tank Battle competition. As Hardware Lead working alongside Software Lead Ariel Tamayev, I developed the mechanical systems, selected all components, and integrated the hardware over a 14-week period. The robot won 1st place in the Robot Tank Battle Competition with a 3-0-1 record.

## Competition Overview

**Objective:** The objective is to score points by shooting 40 mm diameter ping pong balls at the opponent's home base and/or robot. Robots and home bases are marked with infrared (IR) light sources to enable autonomous targeting.

**Arena:** Competition rounds take place in an enclosed 10 ft × 6 ft arena with 1 ft tall walls. Home bases with infrared LED beacons are located at each end, with docking zones for robot reloading and maintenance. The arena contains avoidable obstacles (collisions result in point penalties) and floor obstacles that impede movement but don't penalize contact.

**Robot Constraints:** Robots must fit within 1 ft × 1 ft × 10 in dimensions in all operational modes, carry only one ping pong ball at a time, and avoid damaging the arena or other robots.

**Scoring:** Robots score 10 points for hitting the enemy home base and 20 points for hitting a fielded opponent robot (10 points if docked). Penalties include -10 points for self-inflicted home base hits and -10 points for colliding with avoidable obstacles.

## My Contributions

- Complete mechanical design, CAD modeling, and fabrication of chassis, drivetrain, and weapon system
- System architecture and component selection (Mecanum drivetrain, motors, sensors, controllers, power systems)
- High-energy-density spring-retention launcher design with repeatable launch performance
- Sensor placement strategy and hardware-software interface definition
- PID controller tuning for precise wheel speed control
- Hardware debugging and optimization throughout testing and competition

**Partner's Contributions:** Python control system and state machine implementation, LiDAR processing and obstacle avoidance algorithms, camera-based target detection and acquisition logic

---

## System Architecture

The design integrates mechanical, electrical, and software systems to autonomously navigate a contested arena, detect infrared targets, avoid obstacles, and engage opponents while operating within strict size and power constraints.

A dual-servo spring-retention launcher achieves high energy density using stacked wave disc springs and a bearing-guided plunger, delivering consistent projectile launches throughout competition while fitting within the robot's compact footprint. The Mecanum wheel drivetrain with four independently-controlled motors enables omnidirectional translation—strafing in any direction without rotation—maintaining weapon alignment and simplifying obstacle navigation during combat.

The chassis architecture integrates these systems within a 12"×12"×10" envelope using laser-cut acrylic panels and 3D-printed structural components connected via heat-set threaded inserts. The sensor suite fuses 360° LiDAR data for obstacle detection with a modified infrared camera for target acquisition, while a Raspberry Pi 4B manages sensor processing, motor control, and autonomous decision-making.

---

## Chassis Design

### Drivetrain

<div class="row">
    <div class="col-md-6 mt-3">
        <p>The chassis integrates 6 laser-cut acrylic panels with 9 3D-printed components, assembled using metric screws and heat-set threaded inserts. The cannon mounts to the front panel and bottom plate, while the camera module mounts flush to the front panel. The LiDAR and Raspberry Pi mount on standoffs atop the battery tunnel, and motor controllers are positioned in the wheel wells. A rear access hatch provides battery access.</p>
        
        <p>Four 80 mm Mecanum wheels, each driven by a 12V 40 RPM geared brushed DC motor, enable omnidirectional translation—forward, backward, and lateral strafing—without rotation. The motors mount to the inner side walls and connect to the wheels via provided shaft couplers.</p>
    </div>
    <div class="col-md-6 mt-3">
        {% include figure.liquid path="assets/img/drbones/drivetrain-iso.jpg" title="Vehicle drivetrain" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Chassis Views

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/chassis-top.jpg" title="Chassis top view (structure, motors, wheels)" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/chassis-bottom.jpg" title="Chassis bottom view" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Interior Layout

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/interior.jpg" title="Interior layout with lid removed (front at top, rear at bottom)" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The cannon occupies the center front, flanked by the camera module (left) and speakers (right). The LiDAR mounts on standoffs atop the battery tunnel at mid-chassis, with the beacon platform mounted above it. Motor drivers are positioned in the wheel wells, and the Raspberry Pi mounts to the rear battery tunnel.

---

## Spring-Retention Launcher

### Design Overview

<div class="row">
    <div class="col-md-6 mt-3">
        <p>The cannon mechanism consists of four 3D-printed components, two MG959 servos, a stacked wave disc spring, and a 6mm linear rod with bearing. Stacked wave disc springs provide higher energy storage per unit volume compared to conventional coil springs, enabling a compact launcher footprint.</p>
        
        <p>Two servos actuate rotating latches that retain a bearing-guided plunger against the compressed spring. Upon servo rotation, the latches release, allowing the spring to drive the plunger forward and strike the projectile. The linear bearing constrains plunger motion to a single axis, ensuring consistent strike velocity and launch repeatability.</p>
    </div>
    <div class="col-md-6 mt-3">
        {% include figure.liquid path="assets/img/drbones/launcher-iso.jpg" title="The cannon" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Mechanism Operation

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/launcher-cross-section.jpg" title="Launcher cross section: unloaded (left) and loaded (right)" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The cross section shows the launcher in unloaded (left) and loaded (right) states. In the unloaded state, the servos are open and the spring is relaxed. In the loaded state, the plunger compresses the spring and the servos close to retain it.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/plunger-latch.jpg" title="Plunger and rotating latch positions" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

When open (left), the plunger slides freely past the latches. When closed (right), the latches block the plunger, retaining the compressed spring.

### Design Iterations

The launcher underwent multiple design iterations to address mechanical failures discovered during testing.

**Servo Torque:** Initial servo selection proved insufficient; once the spring was compressed and retained, friction forces on the latches prevented servo rotation and spring release. Progressive servo sizing through bench testing led to the selection of MG959 servos, which provided adequate torque to overcome the retention friction and reliably trigger the mechanism.

**Structural Failure:** The barrel front plate experienced shearing failure where the plunger stop attached. The impact forces during rapid deceleration exceeded the material strength of the initial design. Iterative testing with increased wall thickness and infill density, combined with a material change from PLA to PETG, resolved the structural failure. An integrated impact damper was added to the plunger stop interface to distribute deceleration forces and prevent stress concentration.

**Launch Optimization:** The final optimization positioned the projectile 5mm before the plunger's full extension, allowing the plunger to accelerate to maximum velocity before impact, thereby maximizing momentum transfer to the projectile.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/ball-launcher-detail.jpg" title="Ball launcher details" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Technical Drawings

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/launcher-housing-drawing.jpg" title="Launcher housing" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/launcher-plunger-drawing.jpg" title="Launcher plunger" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/launcher-latch-drawing.jpg" title="Launcher servo latch" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Camera Module

<div class="row">
    <div class="col-md-6 mt-3">
        <p>A custom camera module was designed to mount the Arducam camera and integrate polarized filters for IR-only light detection. The robot is equipped with a single Arducam 1080P Day & Night Vision USB Camera. The resolution of the camera is 2 megapixels, and has a 100° vertical field of view, and a 138° diagonal field of view.</p>
        
        <p>The camera comes with an automatic IR-cut filter. This filter was removed, so that infrared light would always be visible to the camera. The IR illuminators that came with the camera were also disabled. In addition to removing the IR filter, four pieces of polarized film were placed in front of the camera to filter out non-infrared light. Thus, the camera only received infrared light.</p>
        
        <p>The housing mounts internally to the front panel with the lens sitting flush with the robot's exterior.</p>
    </div>
    <div class="col-md-6 mt-3">
        {% include figure.liquid path="assets/img/drbones/camera-module.jpg" title="Camera module" class="img-fluid rounded z-depth-1 mb-3" %}
        {% include figure.liquid path="assets/img/drbones/camera-module-section.jpg" title="Camera module cross-section" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/drbones/front-panel.jpg" title="Front panel" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Electrical Systems

### Motor Control

Two DROK L298 H-Bridge Motor Speed Controllers drive the four motors, with each driver controlling two motors independently. Each driver requires separate power inputs: one for control logic and one for motor power. Three GPIO pins per motor control direction (IN1/IN2) and speed via PWM (Enable pin).

The driver boards are powered at 3.3V to match the Raspberry Pi's GPIO logic level. Powering the boards at 5V would prevent recognition of the Pi's 3.3V signals, causing control failures. Motor power channels accept 6.5V-27V input with 7A continuous current capability.

### Power System

Separate battery systems for motors and electronics. A 12V 5000mAh NiMH battery powers the four drive motors with 5A standard discharge (10A maximum continuous). A Nitecore NB10000 USB-C power bank (10,000mAh, 5V, 3A) powers the Raspberry Pi and all connected sensors and peripherals.

### Sensor Suite

- **Slamtec RPLiDAR A1M8:** 360° obstacle detection with 5.5Hz scanning frequency, 0.5mm distance resolution, and 1° angular resolution. Each scan returns quality-filtered distance measurements at one-degree intervals around the robot. The sensor connects via USB 3.0 for power and data.
- **Modified Arducam camera:** IR-only target detection via polarized filter stack
- **Raspberry Pi 4B:** Main controller with GPIO pins interfacing with four motors (three pins each), launcher servos, and control buttons. USB 3.0 ports connect to the LiDAR and camera, while a USB 2.0 port powers the speaker.

---

## Competition Performance

The robot won first place with a 3-0-1 record, demonstrating effective autonomous navigation, target acquisition, and opponent engagement throughout the tournament.

### Strategy

The competition strategy prioritized simplicity: the robot exclusively translated (forward, backward, left, right strafing) without rotation, eliminating the complexity of orientation tracking during turns.

The core logic drove forward continuously until sensors detected either an obstacle or IR target. Upon obstacle detection, the robot strafed away from the obstruction. Upon target detection, the robot strafed to align, then fired when centered and within range. This approach leveraged the Mecanum drivetrain's omnidirectional capability and the camera's 4+ foot detection range for engagement beyond typical collision distances.

### Mid-Competition Optimization

Mid-competition analysis revealed the robot was acquiring targets beyond its programmed firing range (1200mm). Increasing the engagement threshold to 1600mm improved performance in subsequent matches with no adverse effects, demonstrating the value of real-time parameter optimization under competition conditions.

### Results

The robot successfully hit opponent bases, engaged fielded robots, and autonomously returned to home base. The IR camera system reliably detected targets with minimal false triggers. LiDAR-based obstacle avoidance effectively handled frontal obstructions but struggled with lateral obstacles during strafing maneuvers, resulting in occasional collision penalties.

### Challenges

**PID Controller Failure:** Maintaining straight-line translation without rotation required all four wheels to spin at identical speeds. Motor encoder feedback enabled implementation of a PID (proportional-integral-derivative) controller to regulate individual motor speeds via PWM (pulse width modulation). Initial test-stand trials and ground testing validated the control strategy, successfully returning the robot to its starting position after full directional test sequences.

However, days before competition, the back left motor controller's enable pin failed, preventing PWM functionality—any positive duty cycle was interpreted as 100%, any negative as -100%. With speed modulation impossible on one motor, we abandoned PID entirely and operated all motors at fixed duty cycles (100%, 0%, or -100%), accepting reduced directional precision rather than asymmetric control.

**Obstacle Avoidance Limitations:** The obstacle avoidance algorithm reactively changed direction for each individual LiDAR point, resulting in jittery motion. A 0.3-second hold time after each strafe command served as a crude workaround but nullified subsequent scan data.

### Potential Improvements

**Proper PID Implementation:** Replacing the failed motor controller would enable re-implementation of the validated PID speed control system. Uniform wheel speeds would improve straight-line tracking, enhancing obstacle navigation accuracy and target alignment precision.

**Gyroscope:** Floor obstacles caused unintended rotational drift during translation. Without orientation feedback, the robot had no mechanism to detect or correct heading deviations. A gyroscope would provide continuous angular position data, enabling closed-loop heading control to maintain alignment with target objectives throughout navigation.

**Improved Light Detection:** The firing condition relied on a single pixel exceeding the brightness threshold, centered in frame, within 1600 mm range. This single-pixel criterion proved susceptible to false positives from reflections and ambient light sources, causing occasional misfires. Requiring a cluster of high-brightness pixels (e.g., 100+ pixels) would provide more robust target confirmation and reduce false trigger rates.

**Improved Obstacle Detection:** Aggregating multiple consecutive scans to identify persistent obstacles would enable smoother trajectory planning with direction changes triggered only when threats are consistently detected across multiple measurements.

<script>
document.addEventListener('DOMContentLoaded', function() {
  mediumZoom('img:not(.emoji)');
});
</script>

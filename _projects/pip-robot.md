---
layout: page
title: Pip Educational Robot
description: Complete hardware development of an affordable educational robot for K-8 classrooms
img: assets/img/pip/pip_thumbnail.jpg
importance: 1
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
        {% include figure.liquid loading="eager" path="assets/img/pip/hero.jpg" title="Pip robot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Pip is an educational robot designed to make robotics and programming accessible to K-8 rooms. Conceived as a superior alternative to existing educational robotics tools, Pip combines sensors, motors, and wireless connectivity in a kid-friendly platform. Students learn through a gamified, Duolingo-style web interface where hardware and software work together to teach coding fundamentals through hands-on interaction.

## System Overview

- **ESP32-S3:** WiFi + Bluetooth Low Energy connectivity
- **LiPo battery** with TI power management architecture
- **Multi-sensor suite:** IMU (orientation), ToF distance sensors (obstacle detection/navigation), color sensor (line-following)
- **User interface:** OLED display, buttons, LEDs, buzzer
- **Dual motors** with quadrature Hall effect encoders
- **Web-based programming interface** for classroom curriculum

## PCB System

- **Main board:** 4-layer rigid PCB
- **3 peripheral boards:** 2-layer flex PCBs (front sensor, bottom sensor, encoder boards)
- Custom enclosure design and PCB integration
- Backplane connector integration across all boards

## Key Achievements

- **5 main board revisions** + peripheral board iterations
- **Cost reduction:** $200+ to $69 per unit (component selection and design optimization)
- **DFM optimization:** Assembly reduced from 45 min → 4 min through connector integration (eliminated soldering, improved reliability)
- **Production collaboration** with overseas manufacturers

## Deployment

Piloted in K-8 classrooms | 25+ students, ~200 user hours | Production-ready design

---

## Multi-Board Architecture

Pip's hardware is built on a 5-board system: one 4-layer rigid main board serving as the central hub, with three 2-layer flex peripheral boards handling sensors and motor encoders. This modular approach enabled independent design iteration, simplified assembly, and optimized board real estate for component placement.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/boards-exploded.jpeg" title="5-board system" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Main Board (4-Layer Rigid PCB)

Central processing and power management hub containing:

- ESP32-S3-WROOM-1 module (WiFi/BLE)
- Complete TI power management architecture: LiPo charging, system regulation, motor boost conversion, voltage divider battery monitoring with MOSFET for power savings
- DRV8411 dual motor driver
- LSM6DSV16X 6-axis IMU
- OLED display, user interface (buttons, LEDs, buzzer)
- USB-C interface with ESD protection
- Hirose backplane connectors (peripheral boards), Molex connector (display), JST connector (battery)
- I2C bus routing to sensor suite

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/main-board-layers.jpg" title="Main board layers" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/main-board-final.jpg" title="Main board assembled" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Front Sensor Board

<div class="row">
    <div class="col-md-6 mt-3">
        <p><strong>Obstacle detection and navigation</strong></p>
        <ul>
            <li>VL53L1CX multizone ToF distance sensor (forward-looking)</li>
            <li>Dual VCNL36828P side-looking 1D ToF sensors</li>
            <li>Dual RGB LEDs (headlights)</li>
            <li>2-layer flex design: conforms to curved mounting surface for proper sensor angle through enclosure, integral flex cable to main board backplane connector</li>
        </ul>
    </div>
    <div class="col-md-6 mt-3">
        {% include figure.liquid path="assets/img/pip/front-sensor-bracket.jpg" title="Front board mounting bracket" class="img-fluid rounded z-depth-1 mb-3" %}
        {% include figure.liquid path="assets/img/pip/front-sensor-board.jpg" title="Front sensor board" class="img-fluid rounded z-depth-1 mb-3" %}
        {% include figure.liquid path="assets/img/pip/front-sensor-layout.jpg" title="Front sensor PCB layout" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Bottom Sensor Board

**Line-following and surface detection**

- VEML3328 color sensor
- 3014 LED (illumination)
- 2-layer flex with double-sided assembly, integral cable and backplane connector
- Heat-staked directly to enclosure

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/bottom-sensor-layers.jpg" title="Bottom sensor PCB" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/bottom-sensor-assembled.jpg" title="Bottom sensor assembled" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Encoder Boards

**Motor position feedback**

- TLE4946-2K hall effect sensors
- Shaft-mounted magnets
- 2-layer flex with stiffener for durability
- Soldered directly to motor pins, backplane connector to main board
- Mirrored left/right layouts

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/encoder-layers.jpg" title="Encoder PCB layers" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/encoder-assembled.jpg" title="Encoder boards" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Design Evolution

### Proof of Concept

<div class="row">
    <div class="col-md-7 mt-3">
        <ul>
            <li>Core system validation: ESP32-S3 wireless control, motor driver (DRV8411), LiPo charging (BQ25185), voltage regulation (TLV62085)</li>
            <li>USB-C interface</li>
        </ul>
    </div>
    <div class="col-md-5 mt-3">
        {% include figure.liquid path="assets/img/pip/Proof.jpg" title="Proof of concept" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Rev 1

<div class="row">
    <div class="col-md-7 mt-3">
        <ul>
            <li>Production form factor and shape established</li>
            <li>User buttons, RGB LEDs</li>
            <li>Speaker (8Ω) with PAM8302AAS driver</li>
            <li>BNO085 9-axis IMU</li>
            <li>Increased bulk capacitance to motor driver (resolved ESP stability issues from proof of concept)</li>
            <li>Solder pad connections for peripheral boards (motors, front board, bottom board)</li>
        </ul>
    </div>
    <div class="col-md-5 mt-3">
        {% include figure.liquid path="assets/img/pip/REV1.jpg" title="Rev 1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Rev 2

<div class="row">
    <div class="col-md-7 mt-3">
        <ul>
            <li>Upgraded power electronics: BQ24075 charger + BQ27441 battery monitor IC</li>
            <li>Increased motor voltage: Added TPS61088 boost converter for motor power (6V instead of 3.3V for higher speed and torque)</li>
            <li>Audio improvement: MAX98357A speaker driver (enabled volume control)</li>
            <li>Speaker upgrade: wired → SMD</li>
            <li>Added OLED display support (solder pads and supporting electronics)</li>
        </ul>
    </div>
    <div class="col-md-5 mt-3">
        {% include figure.liquid path="assets/img/pip/REV2.jpg" title="Rev 2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Rev 3

<div class="row">
    <div class="col-md-7 mt-3">
        <ul>
            <li><strong>I2C redesign:</strong> Split to dual I2C channels, added TCA9617B I2C buffer, improved routing to eliminate long branches and stubs (resolved bandwidth/stability issues)</li>
            <li><strong>Motor power stability:</strong> Added current limiting resistor to motor driver (resolved ESP32 brownout during rapid direction changes)</li>
            <li><strong>Power management:</strong> Added TPS22810 load switch to cut idle power while maintaining ESP32 low-power mode (off-state battery life: days → months)</li>
        </ul>
    </div>
    <div class="col-md-5 mt-3">
        {% include figure.liquid path="assets/img/pip/REV3.jpg" title="Rev 3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Rev 4

<div class="row">
    <div class="col-md-7 mt-3">
        <ul>
            <li><strong>Motor encoder integration:</strong> Redesigned motor solder pads for custom flex PCB encoder boards (smaller footprint, eliminated large hand-solder pads)</li>
            <li><strong>I2C optimization:</strong> Moved IMU to secondary I2C line with battery monitor (further stability improvements)</li>
            <li>General routing improvements</li>
        </ul>
    </div>
    <div class="col-md-5 mt-3">
        {% include figure.liquid path="assets/img/pip/REV4.jpg" title="Rev 4" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Rev 5 (Final Production)

- **Cost optimization:** Battery monitor to voltage divider, 9-axis to 6-axis IMU (LSM6DSV16X), speaker+driver to buzzer, N16R8 to N4 ESP32 (PSRAM removal)
- **I2C simplification:** Single bus (battery monitor removal eliminated bandwidth issues)
- **Connectors & DFM:** Hirose backplane (peripheral boards), Molex (display), JST (battery) - eliminated all soldering (assembly: 45 min to 4 min)
- **Protection & layout:** TPD4E05U06 USB ESD, optimized routing and component placement, relocated USB-C/LEDs

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/REV5.jpg" title="Rev 5 final production" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Peripheral Board Evolution

### Front Sensor Board (Rev 1 → Rev 3)

**Rev 1:** VL53L7CX multizone ToF, dual RGB LEDs, VCNL36828P side ToFs with voltage regulators, constrained outline limited routing, no alignment features caused installation issues

**Rev 2:** Expanded outline for improved routing, added alignment features, switched to VL53L5CX (cost reduction)

**Rev 3 (Final):** VL53L5CX → VL53L1CX (cost reduction), added Hirose backplane connector (DFM), improved routing

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Front_Board_Revs.jpg" title="Front sensor evolution" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Bottom Sensor Board (Rev 1 → Rev 3)

**Rev 1:** 4-layer rigid PCB with custom flex cable, 5x VCNT2020 IR sensor array (TMUX1208 analog multiplexer, CSD17484F4 power control), VEML3328 color sensor with 3014 LED (CSD17484F4 power control), small MOSFET package caused assembly failures

**Rev 2:** CSD17484F4 to NTK3134NT1G (larger footprint resolved assembly issues), improved flex cable outline for better routing

**Rev 3 (Final):** Eliminated IR sensor array (color sensor sufficient for line-following, cost reduction), 4-layer rigid to 2-layer flex PCB with integral flex ribbon and Hirose connector (eliminated soldering, reduced size)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Bottom_Board_Revs.jpg" title="Bottom sensor evolution" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Encoder Boards (Rev 1 → Rev 2)

**Rev 1:** 2-layer flex PCB with integral flex cable, dual TLE4946-2K hall effect sensors, soldered to motor pins and main board solder pads, mirrored left/right layouts

**Rev 2 (Final):** Improved routing, added Hirose backplane connector (eliminated main board soldering)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Encoder_Board_Revs.jpg" title="Encoder evolution" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Encoder Boards (Rev 1 → Rev 2)

**Rev 1:** 2-layer flex PCB with integral flex cable, dual TLE4946-2K hall effect sensors, soldered to motor pins and main board solder pads, mirrored left/right layouts

**Rev 2 (Final):** Improved routing, added Hirose backplane connector (eliminated main board soldering)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/encoder-evolution.jpg" title="Encoder evolution" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Web Platform

### Quest
Duolingo-style gamified curriculum where students learn through real-time interaction between Pip's physical actions and web-based challenges

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Quest.jpg" title="Quest interface" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Sandbox
Unrestricted coding playground for creating and uploading custom programs to Pip

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Sandbox.jpg" title="Sandbox coding interface" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

### Garage
Free play mode to drive Pip around, customize colors, sounds, and display

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Garage.jpg" title="Garage interface" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

---

## Classroom Deployment

<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Pilot_2.JPG" title="Student programming Pip" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Pilot_3.jpg" title="Classroom activity" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Pilot_1.jpg" title="Student using Pip" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row mt-3">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Pilot_4.jpg" title="Line following activity" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/pip/Pilot_5.jpg" title="Maze challenge" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

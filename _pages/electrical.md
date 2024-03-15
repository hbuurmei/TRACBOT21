---
layout: page
permalink: /electrical/
title: Electrical
# description: Electrical design.
nav: false
nav_order: 2
---


<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/power_distribution_drive_train.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ir_sensors_electrical" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/i2c_components_electrical.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    The electrical diagrams for the TRACBOT21. On the left is the schematic of the drive train, in the center the IR sensors, and on the right the IMU plus servos. Click to enlarge.
</div>

### Power Distribution
Our robot was powered by two 7V2 battery packs attached in a series configuration to provide a total of 14V4. Several voltage regulators were used in order to manage power disribution to the rest of the robot:
- Two 12V regulators in parallel to the drive train (using multiple increases acceptable drive train current draw)
- One 12V regulator to the Arduino Uno 
- One 5V regulator to the Servos

The 12V regulator used was the L7812, and the 5V regulator was the M1084. All were attached to the 14V4 supply; however, a potential improvement here to reduce wasted energy would be to supply the 5V regulator with a single 7V2 battery to reduce the voltage drop.

### Drive Train
The drive train electronics were run off the L289N motor driver with a 12V power supply. Logic supply was taken from the Uno at 5V. Two 12V Greartisan DC Motors were selected for the drive train, and a the 100RPM configuration was chosen as this provided a good balance between maximum speed and speed range. Initially we selected the 200RPM configuration, but ultimately found that the minimum loaded speed was too high to enable precise turning. Luckily, this vendor has many different options with the same motor geometry, making it easy to iterate without redesigning the motor mount assembly.

Both motors were driven by a PWM signal to the enable pins for speed control. The pins used were specifically chosen to be on the same hardware timer (ITimer2) to improve consistency between the motor behavior.

### Swivel & Deposit Servos

### Beacon Sensing

### Line Sensing

### Inertial Measurement Unit


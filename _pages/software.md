---
layout: page
permalink: /software/
title: Software
nav: false
nav_order: 2
giscus_comments: true
---

For this project, we made us of the [PlatformIO](https://platformio.org/) ecosystem to develop the software for the robot.
This allowed for easy version control, dependency management, and testing.
Our GitHub repository can be found [here](https://github.com/hbuurmei/TRACBOT21-PIO).

### State Diagram
--- 

[insert state diagram]

### Libraries
#### TimerInterrupt
#### IMU Processing
The IMU processing class inherits the open-source [mpu6050](https://github.com/ElectronicCats/mpu6050) library and acts as a wrapper to improve ease of use. This library contains two key functions that expand upon the capabilities of the mpu6050 library:
- ``calibrate()`` reads IMU data for an user specified amount the time. The arithmetic mean of this data is stored as the bias for each sensor. This bias is then used to correct the IMU raw measurements to greatly improve accuracy.
- ``update_integrator()`` is called at a fixed interval by ITimer1 to provide estimates of angles and position/velocity. It works by collecting the current bias-compensated measurements and integrating those measurements via a forward Euler approximation. This function along with the ability to ``reset_integrators()`` is key in measuring our turns to a high degree of precision, necessary for many events in our state diagram.


#### Servo Commanding

#### Motor Commanding

#### Line Sensor Processing



[comment on limited timers as well]

---
layout: page
permalink: /software/
title: Software
nav: false
nav_order: 2
giscus_comments: false
---

For this project, we made us of the [PlatformIO](https://platformio.org/) ecosystem to develop the software for the robot.
This allowed for easy version control, dependency management, and testing.
Our GitHub repository can be found [here](https://github.com/hbuurmei/TRACBOT21-PIO).

### State Diagram
--- 
Due to the sequential nature of the tasks assigned for our robot, our state diagram is also highly linear in nature. States exist in order to complete each task one after the other. The graphic of our state diagram provided below is a substantial simplifcation over the true stateflow logic in our software, but is rather meant to provide a general understanding of the logical flow we intend to achieve. The key difference that is not represented here is that our software includes a second state diagram that handles pauses and the details of drive train commanding.
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/state_diagram4.png" class="img-fluid rounded z-depth-0" zoomable=false %}
  </div>
</div>
Execution of state logic is done in the Arduino ``loop()`` function. Rather than having a difficult-to-maintain switch case in our loop, we rather use a function pointer as our state parameter in the form ``void (*state) (void)``. This allows us to just call ``state()`` in the loop and change the function pointer to transition between states. 

### Libraries/Custom Classes
---

#### **TimerInterrupt**
The [TimerInterrupt](https://github.com/khoih-prog/TimerInterrupt) library is an open-source repository that allows users to directly interface with the hardware timers available on their Arduino board. This was especially relevant for us as it allowed us to repurpose a hardware timer for integrating IMU measurements, allowing for angle tracking in our software. Having a dedicated hardware timer proved to be far more precise than using ``millis()`` for the same purpose.

A key learning experience from our project is that one must be extremely conscious of the timers being used by not only the user, but the Arduino itself. The PWM pins on the board use these timers, and one must be careful that you are not accidentially using the timer for two purposes. For example, we chose to perform IMU integration on ITimer1, but the standard Servo library on the Uno controls the Servos via pins 9 and 10, whos PWM also runs off of ITimer1. This led to integration issues and ultimatelly necessitated a last-minue wiring change to offload the Servos to an external breakout board. Another example is that initially we had the one motors enable pin connected to an ITimer0 pin, while the other was on ITimer2. When diagnositng issues driving in a straight line, we eventually moved both motors onto ITimer2, which improved consistency and straight line performance.

#### **IMU Processing**
The IMU processing class was developed in-house and inherits the open-source [mpu6050](https://github.com/ElectronicCats/mpu6050) library and acts as a wrapper to improve ease of use. This library contains two key functions that expand upon the capabilities of the mpu6050 library:
- ``calibrate()`` reads IMU data for an user specified amount the time. The arithmetic mean of this data is stored as the bias for each sensor. This bias is then used to correct the IMU raw measurements to greatly improve accuracy.
- ``update_integrator()`` is called at a fixed interval by ITimer1 to provide estimates of angles and position/velocity. It works by collecting the current bias-compensated measurements and integrating those measurements via a forward Euler approximation. 

$$\theta_{z,n+1} = \theta_{z,n}+(\omega_{z,raw}-\omega_{z,bias})\Delta t$$

This function along with the ability to ``reset_integrators()`` is key in measuring our turns to a high degree of precision, necessary for many events in our state diagram.

#### **Beacon Processing**
Low level control over the IR beacon detection circuit is handled by the IR_Beacon class: this class initializes the analog input pin and digital reset pin, and provides an ``update()`` function that when called periodically takes a new sensor reading from the analog input pin and briefly pulls the reset pin high in order to reset the peak detection circuit. The last detected value of the IR beacon is mapped to a value between 0 and 1023 and is stored in the class for use by other subroutines. 

In our robot the primary role of the IR beacon detector is to determine initial orientation. To do this, the robot sweeps the swivel servo through a 180-degree arc and identifies the IR signature that best matches the servo. The original intention was to design the filtering circuit such that only signals from the beacon would pass through to the Arduino: if this was the case, then the robot would only need to find the direction of maximum signal. However during testing we found two additional sources of noise: 

- Spurious peaks, likely due to electronic noise generated by the servos, high-frequency glints or reflections of sunlight that passed through the filtering, or noise caused by the peak detection reset process. 
- Consistent high-signal regions due to strong sunlight or interference from other IR sources in the room. 

The maximum-only method occasionally failed due to these sources of noise. Attempts to redesign the circuit failed to completely suppress the noise, so we devised a convolution-based method for isolating the beacon signal based on geometric characteristics: this routine is implemented in ``find_beacon_relative()``. We found empirically that when sweeping through 1-degree angle increments from the starting zone the beacon generated a roughly Gaussian-shaped peak covering about 10 degrees. As the sensor sweeps through the angles, the beacon detection subroutine retains the last 15 samples, and multiplies them element-wise with a convolution kernel consisting of an approximate Gaussian covering the middle 10 samples, and heavily negative weights outside of these samples. The sum of these multiplied samples corresponds to a measure of how well the middle of the 15-sample range matches the expected signal shape. Both the single-sample spurious peaks and many-sample noise could be effectively suppressed using this method. 

However, we found that when the board was moved to the other side of the building, we did not see the expected signal shape, and new sources of noise appeared that interfered with this method. For the competition, we simplified this routine to use a simple top-hat convolution kernel that only filtered out spurious peaks. 

#### **Line Sensor Processing**
The line sensor processing was relatively straight forward in our software. We used hysterisis in order to remove chattering around a single threshold, and the min and max thresholds were turned experimentially such that we could detect line crossings. The software also kept running counters of the number of transitions between ``on_line`` and ``off_line`` states which was useful for debugging. The reliability of our sensor meant that this simple software implentation was very reliable, and it did not cause many issues during the project.

#### **Servo Commanding**

#### **Motor Commanding**
The motor control library was developed in-house and provides a range of commanding capabilities for the motor driver. This simplified actions in our state diagram and provided developers with flexibility in how the robot could be maneuvered. Given the size of our robot, this maneuverability was critical to mission success.

One key aspect of the commanding capabilities was three different turn modes, described below:
- ``FORWARD`` executes a turn where one wheel stays fixed, and the other drives forward. This results in a shift of the vehicle center of mass forward while turning.
- ``BACKWARD`` is the opposite of forward, where one wheel drives backward results in the center of mass shifting backward as well.
- ``MIDDDLE`` has the wheels drive in opposite directions, minimizing the shift in center of mass.
  
We found that while the ``MIDDLE`` turns were slightly less accurate due to a higher minimum turning speed, the value of keeping the center of mass in the same place was especially important to tuning the parameters in our software. Therefore, most turns were executed using the ``MIDDLE`` specification.

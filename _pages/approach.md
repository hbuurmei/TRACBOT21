---
layout: page
permalink: /approach/
title: Approach
# description: Our approach to the ME210 challenge.
nav: true
nav_order: 2
---

Several approaches to achieve the tasks as outlined in the competition were considered.
Here, we briefly outline the main approaches we considered and the reasons for our final choice.

### Monolithic Dumpster (*Selected*)
---

Quickly, our team settled on using a dumping mechanism as compared to a shooting mechanism.
The main reason for this is that a dumping mechanism is more robust and less sensitive to the exact position and orientation of the robot, which may not be known accurately.
This, however, comes at the cost of having to drive up to the shooting zone and dump the balls, which takes more time than shooting them from a distance.

Then, the most straightforward approach to a dumping mechanism is to have a monolithic dumpster that first drives up the contact zone, then disposes all the balls simultaneously at the shooting goal and drives up the ramp to celebrate.


### Distributed Dumpster
---

An alternative approach we came up with is a distributed system, where the functionality of the monolithic dumpster is distributed across two robots.

Specifically, a **carrier (C)** robot would be equipped with the necessary sensing capabilities (e.g. line following) to get to the contact zone, back up and drive up the ramp.
A **dumper (D)** robot would only have to be able to drive from the contact zone in a straight line to the shooting goal and dump the balls all at once.
To avoid complex communication between the robots, the carrier robot would simply push the dumper to the contact zone and back up, thereby *passively* releasing the dumper.
If the dumper is equipped with a simple distance sensor, it can detect that it is released, and drive to the shooting goal. 
This is also depicted in the figure below.

<div class="row justify-content-sm-center">
  <div class="col-sm">
    {% include figure.liquid path="assets/img/annotated_distributed.png" title="Distributed dumpster ConOps" class="img-fluid" %}
  </div>
</div>

The main advantages of this concept is that it can achieve the objectives faster, as the robots can work in parallel, it is easier to parallelize the development and each individual robot can be simpler and cheaper.
However, the fact that the power has to be distributed was found to be prohibitive, as we are only allowed two batteries, and the motors to drive up the ramp are power-hungry and require the voltage of both batteries in series.
Thus, this approach was not pursued further.

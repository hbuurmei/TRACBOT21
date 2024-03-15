---
layout: page
permalink: /results/
title: Results
# description: Final results.
nav: true
nav_order: 5
---

After a few weeks of hard work, the robot is fully integrated and operational.

### Robot Assembly
---
We show our fully assembled robot in the images below.
The robot is built with a combination of 3D printed parts and off-the-shelf components.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/side_view.jpeg" class="img-fluid rounded z-depth-1"%}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/front_view" class="img-fluid rounded z-depth-1"%}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/left_side_view.jpeg" class="img-fluid rounded z-depth-1"%}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/top_view.jpeg" class="img-fluid rounded z-depth-1"%}
    </div>
</div>

### Sensing Demonstation
---
Sensing was one of the key components of this project, and posed significant challenges.
In particular, it was nontrivial to get an initial estimate of our (random) starting orientation.
We show a video of the robot sensing the beacon and adjusting its orientation accordingly.

<div class="row mt-3 justify-content-sm-center">
    <div class="col-md-6 mt-3 mt-md-0">
        {% include video.liquid path="assets/video/beacon_sensing.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
    </div>
</div>

Moreover, we show a video of the robot tracking a line and navigating itself to the contact zone and shooting goal, respectively.
Note that at this stage the robot was yet to be equipped with the shooting mechanism.

<div class="row mt-3 justify-content-sm-center">
    <div class="col-md-3 mt-3 mt-md-0">
        {% include video.liquid path="assets/video/line_following.mp4" class="img-fluid rounded z-depth-1" controls=true %}
    </div>
</div>

### Competition Day
---
We succesfully competed with other teams on competition day.
Although we did not make it to the finals, we are proud of our performance and the robot we built.
Below is a picture of the setup, with our robot on the left starting zone, about to start the first round of the competition.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/competition_day.jpeg" title="Competition day" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

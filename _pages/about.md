---
layout: distill
title: Home
permalink: /
description: Project website of TRACBOT21 for Stanford ME210 Robot Challenge. 
authors: [
        {
          "name": "Hugo Buurmeijer",
          "url": "https://hbuurmei.github.io/",
          "affiliation": AA Stanford University
        },
        {
          "name": "Bobby Collins",
          "url": "",
          "affiliation": ME Stanford University
        },
        {
          "name": "Nick Delurgio",
          "url": "",
          "affiliation": ME Stanford University
        },
        {
          "name": "Saurin Holdheim",
          "url": "",
          "affiliation": ME Stanford University
        }
      ]
date: March 15, 2024
toc: [
    {
      "name": "Team"
    },
    {
      "name": "Challenge"
    }
    ]
---

<h2 id="team">Team</h2>

We are a team of Stanford students with a diverse set of backgrounds, dedicated to designing and building a fully functioning robot in a few weeks.
We prioritize functionality over aesthetics and aimed for achieving the MVP in the shortest time.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/first_team_photo.jpeg" title="Team photo" class="img-fluid rounded z-depth-1" %}
  </div>
</div>


<h2 id="challenge">Challenge</h2>

The challenge for this year's competition was to autonomously place a number of balls in a bin, while completing a number of tasks along the way.
Refering to the outline of the field below, the robot is placed in a random orientation, in either *start zone A* or *start zone B*.
Subsequently, the robot is required to hit the *contact zone*, and an additional point is awarded to the team that hits this milestone first.
To meet the requirements, the robot then has to place at least one ball in the *shooting goal* and do a celebration.
This can either be done through dumping or shooting the ball(s).
Of course, the more balls are placed in the basket, the more points the team is awarded, and after the minimum requirements are met, more balls can be loaded in the starting zone.
Finally, for bonus points, the robot can traverse the *climbing ramp*.
All of this shall be done within 2 minutes and 10 seconds.

<div class="row justify-content-sm-center">
  <div class="col-sm">
    {% include figure.liquid path="assets/img/course_challenge.png" title="Course" class="img-fluid" %}
  </div>
</div>

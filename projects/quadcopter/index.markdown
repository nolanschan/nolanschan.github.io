---
title: Self-Stabilizing Quadcopter using Arduino (EE400D - Electrical Engineering Design Project) 
layout: default
---

# Self-Stabilizing Quadcopter using Arduino #

## Introduction ##
<p></p>

For our senior capstone design course, our group decided to build an unmanned aerial vehicle (UAV), more commonly known as a drone. None of us knew much about drones in general, but we thought it would be a cool project and a good learning experience. As electrical engineers, our focus was on the control system — the flight controller, rather than the actual vehicle. 

Our goal was to use commercially-available parts to build a(n X-configuration) quadcopter which would be capable of self-stabilization. The X-configuration quadcopter is by far the most popular UAV configuration for general purposes due to the fact that it can be controlled with a simple flight control system. We chose to use an Arduino UNO as our flight controller because it was something we were all at least somewhat familiar with, and for the abundance of resources available.

[Full project details](/projects/quadcopter/detail)

## Project Overview ##

-  <u>Type</u>: Group (3 members)
-  <u>Timeframe</u>: 1 semester (approx. 3 months)
-  <u>Relevant Concepts/Skills</u>: Research, cost analysis, component selection, electronics assembly and testing, signal processing, failure analysis, Arduino/C++ programming and debugging, flight mechanics, embedded systems, control theory, PID controller
-  <u>Tools</u>: Arduino IDE, Arduino UNO microcontroller, soldering iron
-  <u>Deliverable(s)</u>: Final "product" with demo video + 4 class presentations (Preliminary Design Review, Progress Update, Initial Results, Final Results)
<p></p>

## Procedures ##

<ul style="list-style-type:disc;line-height:100%">
  <li>Researched quadcopter flight mechanics, modeling, components, and control</li><ul style="list-style-type:circle;line-height:100%">
    <li>Performed cost analysis and component selection to design, assemble, and test quadcopter</li></ul>
  <li>Programmed and debugged flight controller code using Arduino</li><ul style="list-style-type:circle;line-height:100%">
    <li>Implemented complementary filter to process signals from IMU</li>
    <li>Set up and calibrated quadcopter and RC system using calibration code</li></ul>
  <li>Implemented PID controller to control quadcopter movement</li><ul style="list-style-type:circle;line-height:100%">
    <li>Improved flight and self-stabilization performance by tuning PID controller</li></ul></ul>
<p></p>

## Results ##

Quadcopter was functional, but had a tendency to drift backwards and would occasionally "jump" unexpectedly. This was likely due to misalignment between the IMU and vehicle body.

<iframe src="https://player.vimeo.com/video/714344300?h=37aa9a706a&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" width="800" height="450" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen title="EE 400D Project Demo"></iframe>
<br>

Unfortunately, we were not able to test our theory or remedy the design before the deadline, as a crash on our last testing day resulted in a broken wire to the power distribution board (PDB) which was not discovered until later.

## Future Work ##
<p></p>

The first things would of course be to fix the broken wire and the misalignment between the IMU and the vehicle body. However, a redesign could also be beneficial. For example, the use of a 4-in-1 ESC (electronic speed controller) rather than 4 separate ESC's could reduce the weight of the quadcopter and also potentially improve the balance. 

## Repository ##
<p></p>

The full code/repository can be found [here](https://github.com/nolanschan/Arduino-Quadcopter).

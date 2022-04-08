---
title: EE400D - Self-stabilizing quadcopter
layout: default
---
# Self-stabilizing quadcopter #

## Project Overview ##

For our senior capstone design course, our group decided to build an unmanned aerial vehicle (UAV), more commonly known as a drone. None of us knew much about drones in general, but we thought it would be a cool project and a good learning experience. As electrical engineers, our focus was on the control system -- the flight controller, rather than the actual vehicle. While there're many types of UAV's out there, the X-configuration quadcopter is by far the most popular, due to the fact that it can be controlled with a simple flight control system.

Our goal was to use commercially-available parts to build a quadcopter which would be capable of self-stabilization. We chose to use an Arduino UNO as our flight controller since it was something we all had worked with before in some way, shape, or form. 

## Theory ##

#### Flight Mechanics ####

Before we could design a quadcopter, we had to learn how they fly!

Unlike cars or boats, which move in 2-dimensional space, aircrafts move in 3-dimensional space. The orientation and control of an aircraft is therefore described by the three angles of rotation about the aircraft's center of gravity: roll, pitch, and yaw.

<i>diagram here</i>

A quadcopter is a helipcopter with 4 rotors. One (diagonal) pair spins clockwise (CW), while the other pair spins counterclockwise (CCW). The movement of a quadcopter is controlled by varying the speed of the rotors.

The altitude of the quadcopter can be controlled by spinning all 4 rotors at the same angular velocity, such that the thrust generated is equal. In general,  2:1 is an acceptable thrust-to-weight ratio for a quadcopter, and allows the vehicle to hover at ~50% throttle.

The roll, pitch, and yaw of the quadcopter can be controlled by spinning 1 pair of rotors faster than the other pair.

### Inertial Measurement Unit (IMU) ###

To control our quadcopter, we had to know where it is and what it's doing. 

## System Block Diagram ##

<img src="/projects/quadcopter/blockdiagram.png" />

## Design Process ##

Since none of us knew much about selecting quadcopter components, we began by looking into build kits. However, we quickly found that most of them were not only beyond our budget, but meant to be used with manufactured/pre-programmed flight controller chips, which would defeat the purpose of our project.

After further research, we made our initial purchases, which included a 220mm wheelbase carbon fiber frame (with 5030 propellers), a set of 2300kV brushless DC motors, electronic speed controllers, an MPU6050 IMU chip, a LiPo battery (+ charger), and a 6-channel digital radio control system.

## Initial Testing and Design Adjustments ##

Upon assembling and testing our quadcopter, we found that it was too heavy! It took almost full throttle for our vehicle to start lifting, and it seemed off-balance. In our inexperience, we had neglected to properly account for the weight of all the components together! Oops. Going back to the drawing board, we decided to use a smaller battery, trading battery-life for less weight. We also opted for 3-blade propellers, which would help generate more lift.


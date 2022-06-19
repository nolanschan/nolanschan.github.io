---
title: Analog-to-Digital / Digital-to-Analog Conversion (EE470 - Digital Control) 
layout: default
---
# Analog-to-Digital / Digital-to-Analog Conversion using Arduino #

## Introduction ##
<p></p>

Part 2 of Benchtop Labs for Digital Control course.

The purpose of this lab experiment is to understand the principals of analog-to-digital conversion (ADC) and digital-to-analog conversion (DAC). The system is implemented on an Arduino Mega2560. A sine wave from an external function generator serves as the analog input signal to the system. Analog-to-digital conversion is performed by the Arduino’s onboard ADC. The digital-to-analog process utilizes a MCP4921 IC chip. The resulting signal is outputted to an external oscilloscope in order to view the waveform. The effect of clock rate on the sampling process is also explored.

[Full project details](/projects/adcdac/detail)

## Project Overview ##

-  <u>Type</u>: Individual
-  <u>Timeframe</u>: Approx. 1 month
-  <u>Relevant Concepts/Skills</u>: Research, component selection, analog circuit design, analog circuit testing, Arduino/C++ programming and debugging, analog-to-digital conversion (ADC), digital-to-analog conversion (DAC)
-  <u>Tools</u>: Arduino IDE, Arduino Mega2560, digital function generator, digital multimeter (DMM), DC power supply, digital oscilloscope
-  <u>Deliverable(s)</u>: Physical circuit, demo, lab report
<p></p>

## Procedures ##

<ul style="list-style-type:disc;line-height:100%">
  <li>Assembled system circuit</li>
  <li>Converted analog input (sine wave) to digital signal using Arduino ADC</li>
  <li>Converted digital signal to analog output using MCP4921 IC chip (DAC)</li>
  <li>Increased clock rate and repeated procedures</li></ul>
<p></p>

## System Block Diagram with Circuit Connections ##
<p></p>

![](/projects/adcdac/assets/blockdiagram.png)

## Physical Implementation ##
<p></p>

![](/projects/adcdac/assets/circuit.jpg)

## Results ##

Selected results are shown below. For the full results, please check out the [details page](/project/adcdac/detail). 

For all results, the default clock rate input/output is shown in the left, and the faster clock rate input/output is shown on the right. It should be noted that due to technical issues with the oscilloscope probes, the amplitude shown are not accurate. However, they were tested to be experimentally equivalent.

### 100Hz ###
![](/projects/adcdac/assets/100Hz.png)

### 1kHz ###
![](/projects/adcdac/assets/1kHz.png)

### 1kHz (paused) ###
![](/projects/adcdac/assets/1kHzpaused.png)

System was implemented properly and correctly converted analog input to digital signal, then back to analog output. The maximum input frequency at which the default clock rate is able to replicate the input sine wave is ≤ 1kHz, likely at a frequency closer to 100Hz. For the faster clock rate, the highest frequency appears to be around 2k - 5kHz.

## Repository ##
<p></p>

The full code/repository can be found [here](https://github.com/nolanschan/Arduino-ADC-DAC).
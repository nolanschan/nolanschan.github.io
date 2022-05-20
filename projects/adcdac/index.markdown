---
title: Analog-to-Digital / Digital-to-Analog Conversion (EE470 - Digital Control) 
layout: default
---
# Analog-to-Digital / Digital-to-Analog Conversion using Arduino #

## Project Overview ##

The purpose of this lab experiment is to understand the principals of analog-to-digital
conversion (ADC) and digital-to-analog conversion (DAC). The system is implemented on an Arduino
Mega 2560. A sine wave from an external function generator serves as the analog input signal to the
system. Analog-to-digital conversion is performed by the Arduino’s onboard ADC. The digital-to-analog
process utilizes a MCP4921 IC chip. The resulting signal is outputted to an external oscilloscope in order
to view the waveform. The effect of clock rate on the sampling process is also explored.

## Analog-to-Digital Conversion (ADC) ##

Analog-to-digital conversion, also known as sampling, is the process of converting a continuous
analog signal into a discrete digital signal. In general, an ADC system takes in, or “samples” the analog
input at an interval determined by the sampling frequency, and converts the actual value to the closest
discrete value.

Like the ATmega328P, the ATmega2560 features a 10-bit successive approximation ADC with +/-
2LSB absolute accuracy. A successive approximation ADC essentially compares the analog input voltage
to the reference voltage by performing a binary search through all possible quantization levels until it
converges on a digital output. Starting with the MSB, the ADC uses a sample and hold comparator to
  compare the analog input voltage V$_{IN}$ with an internally generated reference voltage V$_{ref,n}$ = (½)V$_{REF}$. If
the analog input voltage V$_{IN}$ is greater than the internally generated reference voltage V$_{ref,n}$, then the
MSB is set to 1. Otherwise, it is set to 0. The process is repeated with the next lower bit, with the new
internally generated reference voltage V$_{ref,n+1}$ = (½) (V$_{ref,n}$) + V$_{ref,n}$ or (½)V$_{ref,n}$ depending on the previous
result, until the results converge, and the conversion is completed.

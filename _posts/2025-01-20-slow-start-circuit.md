---
title: "Slow-Start Motor Circuit (Dual NE555)"
dek: "A discrete ramp-up circuit that eases a DC motor up to speed instead of slamming it to full power on switch-on."
status: completed
type: "Mini project"
tags: [Analog Electronics, NE555, Transistors, Motor Control]
images:
  - src: /assets/images/projects/slow-start/circuit-diagram.jpeg
    caption: "Dual NE555 timer schematic with BC557/BC547 switching transistors and RC ramp network"
  - src: /assets/images/projects/slow-start/breadboard.jpeg
    caption: "Breadboard build driving a geared DC motor and wheel"
---

Switching a DC motor straight to full supply voltage causes an inrush current spike and a hard mechanical jerk on start-up — hard on the motor, hard on whatever it's driving, and hard on the power rail feeding it. A slow-start circuit fixes this in hardware, with no microcontroller involved: it's pure analog timing.

## The circuit

The design uses **two NE555 timers** working together with a small network of switching transistors (**BC557**, **BC547**, **2N2222**) and an RC timing network. Instead of the motor supply snapping to full voltage, the RC network's charge curve controls how gradually the transistors let current through to the motor — so speed ramps up over a set time rather than jumping instantly.

Discrete, all-analog soft-start circuits like this are the kind of thing that shows up ahead of a microcontroller-based PWM soft-starter in a course sequence: same problem, solved with timers and RC charging curves instead of code.

## Build & test

Built and tested on breadboard, driving a small geared DC motor with a wheel attached so the ramp-up was visible and audible rather than just measured on a scope — motor spins up smoothly rather than snapping to speed, which is the whole point.

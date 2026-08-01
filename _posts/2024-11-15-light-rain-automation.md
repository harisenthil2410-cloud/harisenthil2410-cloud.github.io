---
title: "Light & Rain-Water Automation System"
dek: "An Arduino-driven window that reacts to the weather on its own — closing on rain and responding to ambient light, no manual input needed."
status: completed
type: "Mini project"
tags: [Arduino, Sensors, Servo Motors, Automation]
images:
  - src: /assets/images/projects/rain-automation/breadboard.jpeg
    caption: "Arduino Uno with rain-drop sensor module and dual servo motors on breadboard"
  - src: /assets/images/projects/rain-automation/enclosure.jpeg
    caption: "Assembled model — servo-driven shutters and indicator LEDs mounted in a window-frame enclosure"
---

The idea behind this one was simple: an open window doesn't know it's raining. This project gives it a way to find out and react — automatically closing a shutter mechanism when rain is detected, without anyone needing to run over and shut it.

## How it works

An **Arduino Uno** reads a rain-drop sensor module continuously. Rain on the sensor's exposed traces changes its output, which the Arduino picks up as the trigger condition. On detecting rain, it drives **two servo motors** that operate the shutter mechanism, closing the window model automatically. Onboard LEDs give a visual status indicator — lit when the automation has responded to a rain event.

## From breadboard to model

Prototyped first on breadboard with the rain sensor and servos wired directly to the Uno, then built into a small window-frame enclosure so the servo-driven shutter action could actually be seen closing over the "window," with the rain sensor mounted outside the frame where it would sit on a real window ledge.

## Result

A working automation loop — rain detected → servos actuate → shutter closes — demonstrated end to end on the physical model. A straightforward but complete example of sensor input driving a real mechanical response instead of just a readout.

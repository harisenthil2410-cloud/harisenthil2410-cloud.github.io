---
title: "Audio Amplifier Using LM380"
dek: "A discrete-built power amp around the LM380 IC, driving a real speaker off a 9V battery."
status: completed
type: "Mini project"
tags: [Analog Electronics, LM380, Audio Amplification]
images:
  - src: /assets/images/projects/audio-amp/breadboard.jpeg
    caption: "Breadboard build — LM380 amplifier stage driving a 4-inch speaker from a 9V supply"
  - src: /assets/images/projects/audio-amp/lm380-datasheet.jpeg
    caption: "LM380 pinout (8-pin and 14-pin PDIP) and internal amplifier schematic used as the design reference"
---

The **LM380** is a fixed-gain (~50x) audio power amplifier IC, popular for exactly this kind of build: minimal external parts needed to go from a weak audio signal to something that can actually push a speaker.

## The build

Centered on the 8-pin LM380, with input coupling capacitors, an output coupling capacitor into the speaker, and decoupling on the supply rail to keep the amplifier stable. Power came from a 9V battery, feeding a standard PC-style speaker on the output. The internal schematic (from the datasheet, referenced above) shows why so few external parts are needed — the differential input stage, biasing, and output push-pull stage are all already inside the IC; the breadboard work is really just signal coupling and power supply decoupling around it.

## Result

A working amplifier stage that took line-level audio input and drove the speaker at a usable volume, with a short demo video recorded of it running. Small project, but it's the fundamental building block behind every "add sound output" feature in a larger embedded build.

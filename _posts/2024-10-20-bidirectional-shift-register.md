---
title: "Bidirectional Shift Register Using JK Flip-Flops"
dek: "A digital-logic build of a shift register that moves bits left or right on command, wired up on a 16-bit digital trainer kit."
status: completed
type: "Mini project"
tags: [Digital Logic, JK Flip-Flop, Sequential Circuits]
images:
  - src: /assets/images/projects/shift-register/trainer-board.jpeg
    caption: "16-bit digital learning trainer — JK flip-flop IC wired for bidirectional shifting, driven by a 1 Hz clock"
---

A standard shift register only moves data one way. A **bidirectional** shift register adds a direction control so the same chain of flip-flops can shift its stored bits left or right depending on an external control line — the building block behind things like bit-serial data movement, ring counters, and simple sequence generators.

## The build

Built using **JK flip-flops**, wired on a 16-bit digital learning trainer with a 1 Hz clock source, switch-selectable inputs, and an onboard LED level monitor to read the register's contents directly off the board as bits shifted through on each clock pulse. The direction control routes each flip-flop's output back to its neighbor's input on either the left or right side depending on the selected mode, so the same hardware serves both shift directions without needing separate circuits.

## Result

Verified the register shifting correctly in both directions on the trainer's LED indicators, clocked manually and via the 1 Hz source — a small but solid sequential-logic exercise in JK flip-flop behavior and control-line design.

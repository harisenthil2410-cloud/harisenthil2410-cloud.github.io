---
title: "First-Fault Identification System"
dek: "An 8051-based fault annunciator that doesn't just detect overheat and overload — it remembers which one happened first."
status: completed
type: "Mini project"
tags: [8051, Embedded C, Interrupts, UART, RTC Simulation]
report_pdf: /assets/docs/first-fault-identification-report.pdf
---

Industrial panels often have more than one thing that can go wrong at once, and when they do, the *first* fault matters more than the second — it's usually the root cause, and the second is often just a consequence. This project is a small 8051-based system that captures exactly that: which fault hit first, and prioritizes displaying it accordingly.

## How it behaves

Two active-low switches simulate fault conditions — **overheat** and **overload** — each wired to its own pin. The system's priority logic:

- If **overload** is pressed, the display and UART show `LOAD`/"OVERLOAD ACTIVE" — overload takes priority.
- If **overheat** is pressed *while overload is not active*, the display shows `HEAT`/"OVERHEAT ACTIVE."
- If **overload** is pressed **first**, followed by **overheat**, only "OVERLOAD ACTIVE" is reported — overheat is suppressed because overload is the higher-priority fault.
- If **overheat** is pressed **first**, followed by **overload**, both get reported in sequence, since overheat is the lower-priority one and doesn't block overload's report.
- With no fault active, the display falls back to `SAFE` and shows the current time.

That "which one wins when both are active" logic is the actual point of the project — it's a first-fault latch, not just two independent alarms.

## How it's built

- **Timer0 ISR** drives a multiplexed 4-digit 7-segment display and doubles as a **software RTC** — incrementing seconds/minutes/hours and toggling a colon flag once a second.
- **UART** (via Timer1, 9600-style config) logs every state transition — fault entry and the return to `SAFE` — with a timestamp, so there's a serial trail of exactly when each fault occurred and cleared.
- Segment codes for `SAFE`, `HEAT`, `LOAD`, and digits are hand-defined and swapped into a shared `display_buf`, refreshed digit-by-digit inside the interrupt for flicker-free multiplexing.
- Two status LEDs mirror the current fault state independently of the display, so the panel is readable even at a glance.

```c
void timer0_ISR(void) interrupt 1 {
  TH0 = 0xFC; TL0 = 0x66;      // multiplex display
  P2 &= ~0x0F;
  P0 = display_buf[digit_index];
  switch(digit_index){
    case 0: DIG0=1; break;
    case 1: DIG1=1; break;
    case 2: DIG2=1; break;
    case 3: DIG3=1; break;
  }
  digit_index = (digit_index+1)&0x03;
  ms_count++;
  if(ms_count >= 1000){
    ms_count = 0;
    colon_flag = !colon_flag;
    led_timer = ~led_timer;
    sec++; if(sec>=60){ sec=0; min++; if(min>=60){ min=0; hour++; if(hour>=24) hour=0; } }
  }
}
```

The full annotated source is in the report linked above.

## Result

A working panel that correctly distinguishes "overload happened, then overheat" from "overheat happened, then overload," reports both cases differently over UART, and always resolves cleanly back to a time-keeping `SAFE` state. I recorded a full run-through on video — small enough project to demo end to end in a couple of minutes, but the priority-latch logic is the kind of thing that shows up in real industrial fault panels at much larger scale.

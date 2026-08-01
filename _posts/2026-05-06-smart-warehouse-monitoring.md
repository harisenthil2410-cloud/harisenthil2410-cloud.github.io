---
title: "Smart Warehouse Security & Environmental Monitoring System"
dek: "An ARM Cortex-M33 system that tracks warehouse temperature and worker check-ins, and pushes alerts straight to the owner's phone over BLE — built on Renesas's RA6E2."
status: completed
type: "Team dissertation project — Bachelor of Engineering, ECE, Bharathiar University"
org: "Renesas Electronics — University Program"
tags: [Embedded Systems, ARM Cortex-M33, Renesas RA6E2, BLE, RTC, TrustZone]
report_pdf: /assets/docs/smart-warehouse-monitoring-report.pdf
images:
  - src: /assets/images/projects/warehouse/renesas-certificate.jpeg
    caption: "Certificate of Participation — Renesas University Program Demo Day, 6 May 2026"
---

Warehouses full of electronics, pharmaceuticals, or food stock have two quiet failure modes: nobody notices the temperature drifting out of safe range, and nobody notices a scheduled worker inspection didn't happen. Both are easy to miss with manual supervision and easy to catch with a microcontroller that never gets tired.

## The system

Built on a **Renesas RA6E2** board (Arm Cortex‑M33, 200 MHz, with TrustZone), the system does two things continuously:

- **Environmental monitoring** — an **HS4001** temperature/humidity sensor on I2C reports conditions to the MCU. If the reading crosses a safe threshold, an LED alert triggers and a warning is pushed out over Bluetooth.
- **Worker check-in verification** — the RA6E2's onboard **RTC** tracks a scheduled inspection deadline. A push button lets a worker confirm they've completed their round; if the button isn't pressed in time, the system raises an alert instead of silently assuming everything's fine.

Alerts go out over a **DA14531 BLE module** on UART, straight to the warehouse owner's smartphone — so the response to "something's wrong" doesn't depend on someone standing in front of the LED at the right moment.

<blockquote>Fig 8.1 in the full report walks the two parallel decision paths — RTC-driven check-in monitoring and threshold-driven temperature monitoring — that both funnel into the same BLE alert and LED indicator.</blockquote>

## Why Cortex-M33 / TrustZone

The brief specifically called for justifying the MCU choice, not just using it. Cortex-M33's TrustZone lets the system separate secure operations — like authenticating what gets sent over BLE — from the rest of the application logic, which matters for a system whose whole job is trustworthy alerting. It's also the reason this platform scales cleanly toward future work like authenticated cloud reporting, without a redesign.

## Toolchain

Development ran through Renesas **Quick Connect Studio** and the **Flexible Software Package (FSP)** inside **e² Studio**, which generates peripheral init code from a visual configuration rather than hand-writing register setup for GPIO, UART, I2C, and RTC. The build went through the **GNU ARM toolchain**, and the compiled image was flashed to the board as an **SREC** file via **SEGGER J‑Flash Lite** over SWD.

## Team & my part

This was an 8-person dissertation project (Bhadmavaisnavi T, Gopika B, **Haripriya S**, Nataraj C, Niveditha AR, Tharshanaa P, Viknesh V, Lijith Kumar P). I worked on the **hardware implementation**, and contributed to the presentation deck and demo video that we took to the Renesas Expert Panel.

The system was demoed live at the **Renesas University Program Demo Day** on 6 May 2026, where it received a Certificate of Participation.

The full dissertation — block diagrams, circuit schematics, flowcharts, and results — is linked above.

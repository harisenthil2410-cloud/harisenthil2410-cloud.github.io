---
title: "An Edge-Native Real-Time Water Quality Monitoring System for Anomaly Detection"
dek: "Multi-zone pH/TDS/turbidity sensing over LoRaWAN, with Isolation Forest catching contamination the moment it deviates from normal — not after it crosses a fixed threshold."
status: completed
type: "Industry-mentored project"
org: "Gyan Astra IT Solutions"
tags: [IoT, ESP32, LoRaWAN, Machine Learning, Isolation Forest, Cloud Dashboard]
demo_url: https://water-anomaly-cloud.onrender.com/dashboard
images:
  - src: /assets/images/projects/water-quality/setup-single-zone.jpeg
    caption: "Zone node — pH, TDS, and turbidity sensors feeding an ESP32, live readings on the local LCD/7-segment display"
  - src: /assets/images/projects/water-quality/multi-zone-setup.jpeg
    caption: "Multi-zone test bench: contamination sample, sensor breadboard, and the zone controller streaming readings over serial"
  - src: /assets/images/projects/water-quality/severity-table.png
    caption: "Anomaly severity classification used to grade incoming readings"
  - src: /assets/images/projects/water-quality/certificate.png
    caption: "Project completion certificate — Gyan Astra IT Solutions, Dec 2025–Apr 2026"
---

Most water quality monitors work off fixed thresholds: if pH crosses X or turbidity crosses Y, raise an alarm. That misses a lot — a slow drift toward contamination can stay just inside every individual threshold while still being clearly abnormal. This project instead treats "normal" as a pattern the system learns, and flags anything that breaks it.

## What it does

The system watches multiple physical zones at once. Each zone has its own sensor node — pH, TDS (total dissolved solids), and turbidity sensors wired to an **ESP32**, which reads all three continuously and pushes them out over **LoRaWAN**. That's the deliberate design choice here: cheap, low-power, long-range radio links from each zone node back to a central intermediate zone, so the sensing hardware doesn't need Wi-Fi coverage or a wired run to sit wherever the water actually is.

The intermediate zone collects the incoming stream from every zone and runs it through an **Isolation Forest** model — an anomaly-detection algorithm that isolates outliers rather than comparing against a fixed rule. Because it's trained on what normal readings look like across pH, TDS, and turbidity together, it can catch a contamination event that no single threshold would trip.

Every reading is graded into a severity tier — from normal operation, through a first-detected anomaly, to a sustained-caution state, up to a confirmed critical event — so downstream alerts distinguish between "the model noticed something" and "this has now happened repeatedly and needs attention." That tiering is what turns a raw model output into something a person monitoring the dashboard can actually triage at a glance.

## Architecture, end to end

1. **Sense** — pH, TDS, and turbidity sensors per zone, sampled by an ESP32.
2. **Transmit** — local zone → intermediate zone over LoRaWAN, so zones can be physically spread out without needing local internet.
3. **Detect** — Isolation Forest at the intermediate zone scores incoming readings and classifies severity.
4. **Visualize & alert** — real-time data, anomaly trends, and alerts surface on a [cloud dashboard](https://water-anomaly-cloud.onrender.com/dashboard).

The on-node display (LCD + 7-segment, seen above) mirrors pH, TDS, turbidity, and a computed Water Quality Index locally, so a zone is readable even without pulling up the dashboard.

## Where it stood

The project was completed over December 2025–April 2026 under industry mentorship from **Gyan Astra IT Solutions**, who certified the final system. It's the project I'd point to first for how sensing, wireless transport, and ML come together in one working pipeline rather than staying separate demos.

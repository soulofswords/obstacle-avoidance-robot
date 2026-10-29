# Obstacle Avoidance Robot

An Arduino-based obstacle-avoidance car prototype developed as a second-year electrical engineering project.

## What it demonstrates

- Ultrasonic distance sensing for obstacle detection
- Motor control and autonomous direction changes
- Embedded C++/Arduino implementation
- Iterative prototyping across electronics, wiring and chassis integration

The project began as an exploration of a home-cleaning robot concept and was adapted into an obstacle-avoidance car prototype.

## Source

- `build_Obstacle_Avoider_Robot.ino` — Arduino sketch used for the build

## Portfolio

See the project in Gaurang Parag Bhogle's portfolio: https://soulofswords.github.io/gaurang-bhogle-portfolio/

## Notes

The original project archive included a demonstration video. It is intentionally not duplicated here so the repository stays lightweight; the source sketch is the canonical shareable artifact.

---

# IoT-Based Smart Metering

An educational IoT energy-monitoring prototype for observing electrical measurements locally and over Wi-Fi. The supplied project material describes two related implementations:

- **Single-phase prototype:** ESP32, one PZEM-004T, and a 20×4 LCD.
- **Three-phase prototype:** ESP8266 D1 Mini, phase-wise PZEM measurements, an OLED display, and Blynk monitoring.

This repository is a sanitized technical documentation of the project. It is not an installation guide, a utility-grade meter design, or a certified electrical product.

## What problem it addresses

Conventional meter reading can be manual, delayed, and difficult to use for day-to-day analysis. This prototype explores a low-cost way to expose voltage, current, active power, energy, frequency, and power factor locally and through a Wi-Fi dashboard.

## Architecture

### Single phase

```text
AC load
  │
  ├─ PZEM-004T + CT ── UART/TX-RX ── ESP32 ── 20×4 LCD
  │                                      │
  └──────────────────────────────────────┴── Wi-Fi/Blynk
```

### Three phase

```text
R/Y/B phase inputs
  │
  └─ phase measurement modules ── ESP8266 D1 Mini ── OLED
                                              │
                                              └── Wi-Fi/Blynk
```

The three-phase firmware described in the report maintains separate R/Y/B values and publishes phase-wise readings for remote visualization. The supplied material is not a complete, validated mains wiring design.

## Measurements and monitoring

The documented firmware reads or exposes:

- Voltage
- Current
- Active power
- Energy
- Frequency
- Power factor

The single-phase demonstration describes no-load behavior and a phone-charger load. The three-phase implementation cycles phase information on the OLED and maps measurements to Blynk channels. EEPROM-backed daily/monthly energy summaries and WiFiManager-based configuration support are also described.

## Results and limitations

The project material supports a bench-level prototype demonstration and firmware architecture. It does **not** provide calibrated accuracy results, uncertainty analysis, repeatability data, long-duration logs, a validated billing workflow, or evidence for predictive maintenance and fault-detection claims. Automated billing, payment integration, and appliance control should therefore be treated as future design goals rather than implemented features.

The source material also contains a documentation conflict: one report passage says two PZEM modules for the three-phase path, while the presentation and firmware define three logical PZEM devices. This repository records the implementation as three phase channels and flags the wiring documentation for review.

See [`docs/TECHNICAL-SUMMARY.md`](docs/TECHNICAL-SUMMARY.md) for the consolidated, sanitized summary and source-handling notes.

## Safety

This project involves potentially lethal mains voltage. Do not reproduce the prototype from this documentation without qualified electrical supervision.

- Use appropriate isolation, fusing, enclosure, earthing, strain relief, creepage, and clearance.
- Confirm the exact PZEM variant, CT orientation, voltage/current limits, and isolation characteristics from current manufacturer documentation.
- Never connect ESP32/ESP8266 GPIO, USB equipment, breadboards, or exposed jumper wires directly to mains.
- A 5 V isolated supply module alone does not make the complete assembly safe.
- Treat diagrams and descriptions as incomplete until a qualified professional has inspected and tested the entire assembly.
- Do not publish or reuse Wi-Fi credentials, Blynk tokens, IP addresses, or identifiable energy traces.

## Public-source policy

The original presentations and report were used as source material but are not copied into this repository. Personal names, roll numbers, institutional sign-offs, credentials, network details, and other identifying or security-sensitive information were intentionally excluded.

## License

The documentation in this repository is provided under the MIT License. Hardware, firmware libraries, cloud services, and manufacturer documentation remain subject to their own licenses and terms.

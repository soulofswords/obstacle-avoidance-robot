# Sanitized technical summary

## Scope and source consolidation

The supplied presentation files are substantively duplicate versions of the same project. The second version adds clearer phase labels and a closing slide; it does not establish a materially different architecture. This summary consolidates the shared technical content and uses the mini report to qualify implementation details and limitations.

The project should be described as an **IoT energy-monitoring prototype**. The supplied evidence does not establish a certified meter, a complete billing product, or an installation-ready mains design.

## Problem statement

The project targets the inconvenience and limited visibility of conventional manual electricity readings. Its intended value is to make electrical measurements available locally and through a Wi-Fi-connected dashboard so that consumption can be observed more frequently and summarized over time.

The material discusses real-time monitoring, automated readings, overuse notifications, predictive maintenance, and billing as broader goals. Only the measurement and monitoring portions are sufficiently supported by the supplied firmware and report.

## System architecture

### Single-phase implementation

The single-phase design uses:

1. A PZEM-004T and current transformer to measure the connected AC load.
2. An ESP32 connected to the measurement module over UART/TX-RX.
3. A 20×4 character LCD for local display.
4. Wi-Fi/Blynk connectivity for remote visualization.
5. Pushbuttons for configuration and energy-data reset functions.

The described demonstration includes a no-load condition and a phone-charger load.

### Three-phase implementation

The three-phase design uses:

1. Separate phase measurements represented as R/Y/B.
2. An ESP8266 D1 Mini as the controller.
3. An OLED for local, sequential phase display.
4. Wi-Fi/Blynk channels for remote values.
5. EEPROM-backed energy summaries and WiFiManager-style configuration support.

The firmware structure defines three logical PZEM devices and phase-wise values. One report passage says that two PZEM modules are used, while the presentation and firmware describe three. The public documentation therefore records the implementation as three logical phase channels and marks the physical wiring count and addressing as an item requiring validation.

## Hardware and software stack

### Single phase

- ESP32
- One PZEM-004T with CT
- 20×4 LCD
- Two pushbuttons
- Switched socket and test wiring

### Three phase

- ESP8266 D1 Mini
- Three logical PZEM measurement channels in the firmware
- 0.96-inch OLED
- Pushbutton
- Hi-Link 5 V isolated AC/DC module
- Supporting passive components and indicator circuitry

### Firmware and services

- Arduino IDE-style embedded firmware
- PZEM004Tv30 library
- UART/software serial support as appropriate to the controller
- Wi-Fi and Blynk client libraries
- OLED graphics library
- WiFiManager-style provisioning/configuration
- EEPROM storage for energy summaries
- RTC/time synchronization support

Library names and implementation details should be checked against the actual source before reproducing the build; the supplied report is the evidence base for this summary.

## Measurement and data flow

The documented measurement set is:

- Voltage
- Current
- Active power
- Energy
- Frequency
- Power factor

The data path is:

```text
Mains/load measurement → PZEM sensor → controller UART → local display
                                             │
                                             └→ Wi-Fi → Blynk dashboard
```

The three-phase firmware reports phase-specific values, detects invalid readings using `isnan()`-style checks, logs serial diagnostics, and cycles OLED pages at approximately four-second intervals according to the report. The material also describes daily, previous-day, monthly, and previous-month energy summaries stored in EEPROM.

## Results supported by the material

- The single-phase setup is described for no-load and phone-charger test conditions.
- The three-phase firmware initializes measurement devices, display, Wi-Fi, and Blynk services.
- R/Y/B values are read and exposed to the display/dashboard path.
- Configuration reset and energy reset controls are described.
- Remote monitoring is the clearest supported IoT feature.

## Limitations and claims not independently demonstrated

The supplied material does not include:

- Reference-meter comparisons or calibration results
- Accuracy, uncertainty, or repeatability percentages
- A defined sampling rate or sustained logging dataset
- Long-term cloud availability evidence
- A validated billing or payment implementation
- A trained predictive-maintenance model
- Fault-detection thresholds or test metrics
- A complete protection, fusing, earthing, insulation, or enclosure design
- A validated phase wiring/addressing diagram

Accordingly, words such as “accurate,” “secure,” “automated billing,” “predictive maintenance,” and “real-time” should be read as project objectives or intended capabilities unless backed by measurements and test records.

## Safe electrical-use warnings

This is a mains-voltage prototype. The documentation must not be used as a substitute for electrical engineering review.

- De-energize circuits before inspection or wiring.
- Use a suitable enclosure, terminals, strain relief, overcurrent protection, earthing, creepage, and clearance.
- Verify sensor ratings, CT direction, conductor routing, isolation barriers, and controller power supplies against current manufacturer specifications.
- Do not use breadboards, exposed jumper wires, or accessible mains conductors for an energized or permanent assembly.
- Never connect a microcontroller pin, USB cable, laptop, or oscilloscope ground to a mains conductor unless the complete measurement method is specifically rated and professionally approved.
- An isolated AC/DC module does not certify the surrounding PCB, wiring, enclosure, or installation.
- Have a qualified electrician or electrical engineer inspect and test the complete assembly before energizing it.
- Protect Wi-Fi provisioning, dashboard access, reset functions, and stored credentials from unauthorized access.

## Sanitization and publication notes

The public version intentionally omits:

- Student names, roll numbers, signatures, examiner/guide details, and institutional sign-off pages
- Blynk authentication tokens, template identifiers, device credentials, and network information
- IP addresses, Wi-Fi passwords, local configuration details, and identifiable household/facility traces

Any token or credential that appeared in the source material should be considered exposed and rotated. No such secret is included in this repository.

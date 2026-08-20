# The Hope Turtle Shell
### Our Open Source Printed Circuit Board for the Turtle Control Bottle

The Human2Human project aims to bring hope and humanity to the most hurting and isolated places on the planet — in a way that doesn't trouble the health and happiness of animals, fish and other our fellow creatures. To do so, we've developed the hope turtle: a non-capital, open-source, autonomous marine vehicle that embodies Earthen principles. This repository holds the designs for our "Turtle Shell" printed circuit board.  This is the PCB that holds of microprocessor, sensors and circuits to run our TurtleOS (https://github.com/h2h-project/turtleOS) navigation platform.  

Our vision is to create a simple and inexpensive PCB that anyone anywhere, keen to build a turtle, can put together themselves and set to sail for under 100$ using local and organic materials as much as possible.

## Philosophy

The design of our Turtle Shell PCB is shared under a CERN-OHL-S license.  While our license does not legally restrict military use, we ask that anyone building on this work honor the spirit it was created in — this design exists to bring aid to isolated and vulnerable communities, not for weapons or warfare.  That's the same principle behind releasing this repository at all: any group doing resonant human/ecological work — coastal monitoring, disaster response, ocean research, humanitarian delivery — should be able to take this board, understand exactly how and why it's built the way it is, and carry it further without waiting on us or paying anyone for the privilege.

The Turtle Shell is designed from the ground up to be assembled by hand, by people who have never assembled a circuit board before. Every component on it is through-hole — there is no surface-mount soldering, no solder paste, no reflow oven, nothing that requires equipment beyond a basic iron and a steady hand. Sensors connect via inexpensive, widely-available modules and JST cables rather than being permanently fixed to the board, which keeps the parts list cheap, keeps a broken sensor a five-minute swap rather than a rework job, and keeps the barrier to building one of these low enough that a volunteer, a partner workshop, or a local maker space anywhere in the world can put one together. 

## The PCB

The current version of the Turtle Shell (v2.4) is a compact, two-layer, 70×37mm control board built around the Seeed Studio XIAO ESP32-S3.  While you don't necessarily need a Xiao ESP32-S3 (turtleOS has a hardware abstraction layer that supports only microprocessors), we've decided to focus our PCB on this MP after extensively testing various alternatives.   While the Xiao ESP32-S3 is not nearly as equipped as navigation specific boards, it resonates fully with our principles of open source and low-cost decentralized replicability, and crucial to our larger project goal of keeping turtle creation cost at under 100$.

Loaded with its microprocessor, the turtle Shell essentially runs TurtleOS and coordinates everything the vessel does. It exposes seven generic 2.00mm JST sensor ports plus a dedicated GPS port, so the same board can carry whatever mix of instruments a given voyage needs — a magnetic angle encoder for rudder position, a combined accelerometer/gyroscope/compass/barometer for heading and weather, a current and voltage monitor for tracking the power budget, a temperature and humidity sensor to watch over the sealed enclosure's health — alongside dedicated sockets for a display and a real-time clock, breakout headers for the microcontroller's full pinout, and a servo connector kept deliberately isolated from the board's own power traces. It's a small board asked to do a lot, and every connector on it exists because a real sensor needed a reliable, correctly-oriented place to plug in.

Beyond the bare Turtle Shell board and its connectors, each unit is populated with the following components — all inexpensive, widely-stocked parts chosen specifically because they're easy to source and replace anywhere in the world.


| Component | Function | Interface | Approx. Cost (USD) |
|---|---|---|---|
| Seeed XIAO ESP32-S3 | Main microcontroller, runs TurtleOS | — | ~$7.50 |
| GPS module *(not yet finalized — e.g. u-blox NEO-6M)* | Position & UTC time | UART, GPS1 port | ~$7 |
| GY-87 10DOF (MPU6050 + HMC5883L/QMC5883 + BMP180) | Heading, attitude, barometric pressure | I²C, SEN port | ~$7 |
| AS5600 | Rudder/servo angle sensing | I²C, SEN port | ~$1.50 |
| INA219 (GY-219) | Battery current, voltage & power monitoring | I²C, SEN port | ~$2 |
| AHT20 | Enclosure temperature & humidity | I²C, SEN port | ~$2.50 |
| 1.3" OLED (SH1106) | Status display | I²C, SCREEN1 socket | ~$4.50 |
| DS3231 RTC (5-pin) | Spoof-resistant, GPS-independent timekeeping | I²C, RTC1 header | ~$3.50 |
| JST↔Dupont cables (×6, mixed lengths) | Connect modules to SEN ports | — | ~$3 |
| **Subtotal** | | | **~$38** |

> **Notes**
> - Prices are single-unit estimates from typical hobbyist suppliers as of this writing and will vary by seller, quantity, and region.
> - This total covers instrumentation only. Bare PCB fabrication and its connectors are quoted separately, and battery, solar panel, servo, and enclosure are **not** included here.
> - The GPS module has not yet been selected against the board's GPS1 pinout (GND, 3V3, RX, TX) — treat this line as a placeholder pending confirmation.

## Where We're Headed

As of August 2026 we're in full development, printing and prototyping mode-- so things are evolving fast!  

The next revision is aimed at making the board more self-contained and more reliable at sea, without giving up the simplicity that makes it buildable by hand. We're working out how to bring battery power directly onto the board — using spring-loaded contacts to reach the microcontroller module's own charging circuit rather than routing through a less efficient path — alongside dedicated, correctly-keyed sockets for the current sensor and the inertial measurement unit, and a permanent home for the solar charging circuit, so fewer loose modules and wires are rattling around inside a hull that will spend weeks rolling in ocean swell. None of this is finished, and some of it may not survive contact with the next prototype — but the goal stays the same: a board that's a little more finished each time, still cheap, still buildable without a lab, and still something anyone reading this repository can pick up and carry forward.

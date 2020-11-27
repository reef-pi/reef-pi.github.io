---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: touchscreen
title: Touchscreen display
draft: true
highlight: true
weight: 6
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

reef-pi can be configured to be used with the offical Raspberry Pi Touchscreen display to provide a direct access to reef-pi, without any network dependency. With a touchscreen it is possible to run reef-pi without any internet or even home wifi connection ( albeit modules like telemetry will not work). Activities like equipment on/off during water change, light intensity controls  are all possible with touchscreen. Workflows involving editing text (like the one involved in creating new timer or equipment) are harder to setup, but can be done using on screen keyboard software (e.g. matchbox-keyboard).

The touchscreen display is only tested with Raspberry Pi 3, not with pi zero.

### How this work

### Things to consider

- Touchscreen housing
- Power
- I2C wiring

### Bill of materials

- [Pi 3](https://www.adafruit.com/product/3055)
- [micro sd card](https://www.adafruit.com/product/2693)
- 5v 2.4 amp [adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- Raspberry Pi Official [Touchscreen display]()

### Wiring

![breadboard](/img/light/display.png)

### Installation & Configuration

- Follow reef-pi installation [guide](../../guides/intro) to setup reef-pi on Raspberry Pi 3.

- Enabling display in reef-pi configuration
- Auto-starting dashboard on-boot
- Adjusting rotation

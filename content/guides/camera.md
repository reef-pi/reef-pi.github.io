---
linktitle: lighting
author: "Ranjib Dey"
draft: true
date: 2017-09-25
title: Camera module
weight: 8
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- iot
---

The camera controller provides easy and convenient way to take reef tank photos on demand and at periodic intervals. reef-pi can also be configured to upload the images taken to google drive. This is useful when users are far from the tank for longer periods (like in vacation), the uploaded images can provide an easy way to stay up to date with current state of the tank. The camera controller does not involve any other electronics other than the official camera module.

### How this work

### Things to consider

- The camera cable that ships with pi camera is rather small (6 inches) and likely to be insufficient for most practical usage. Before ordering the bill of materials, consider where the actual raspberry pi controller will be located and where the camera itself will be mounted. Then choose camera flex cable of appropriate length.

### Bill of materials

- [Pi zero](https://www.adafruit.com/product/3400) or [Pi 3](https://www.adafruit.com/product/3055)
- [micro sd card](https://www.adafruit.com/product/2693)
- 5v 2.4 amp [adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- [Pi Camera board](https://www.adafruit.com/product/1367l)
- [Flex cable](https://www.adafruit.com/product/2144) for camera board

### Installation & Configuration

- Follow reef-pi installation [guide](../../guides/install) to setup reef-pi on Raspberry Pi zero.

- Install camera

- Enable camera capability from system tab and restart reef-pi

- Enable camera controller from camera tab and click on *take photo* button

- Setup periodic image capture

- Setup automatic image upload to google drive


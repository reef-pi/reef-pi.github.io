---
title: "0.0.7"
date: 2017-07-17T21:10:38-07:00
draft: false
---

#### Features

- DFRobot's photo electric sensor based ATO controller
- Temperature sensor & controller, based on ds18b20. Controller to switch on/off heater/cooler based on configuration
- Admin User Interface: Allow shutdown of raspberry pi, reboot from UI

#### Bugfix

- Lighting minimum threshold to ensure pwm value is set to 0
- Equipment state should reflect original state, instead of always "off" on tab change
- Fix exception during shutdown in dev_mode

#### Documentation

- Draft manual for reef-pi


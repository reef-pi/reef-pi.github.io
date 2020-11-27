---
draft: true
linktitle: power
title: Power controller
highlight: true
weight: 4
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- iot
- relay
---
Follow the beginner friendly [installation guide](https://learn.adafruit.com/reef-pi-installation-and-configuration) on learn.adafruit.com, it covers using reef-pi with American DJ power strip. This is not an option outside US or you want to customize your power controller further and have fine grained control over their behavior ([Normally Open/Normally Closed](https://en.wikipedia.org/wiki/Electrical_contacts), current rating, GFCI etc). This guide covers how to build a power controller from scratch, using individual relays and AC sockets and extra tips and tricks related to power controllers.


Automated power strips allow on-demand and timer based control of AC outlets (110v or 220v). They are one of the easiest to build yet most useful controllers using reef-pi. For example, a power controller can turn on/off light or skimmer daily as well as allow on-demand controls like switching off ATO and return pump during water changes. This guide will go through step by step process of building a four outlet power controller. A beginner friendly [guide](https://learn.adafruit.com/reef-pi-power-controller) is also available on adafruit.com.

### How this works

The reef-pi software uses the Raspberry Pi’s GPIO pins to control digital relays, which in turn controls high voltage, high current AC or DC equipment. This mechanism is used across timer or sensor based (like temperature or ATO controllers) equipment controls.


### Things to consider

- Choice of relay: Controlling high AC voltages via Raspberry Pi involves relays. Relays can be optocouplers, mechanical or solid state. Mechanical relays are cheapest, optocouplers are safest and expensive. Solid state relays are somewhere in the middle, safer, more expensive and last longer than mechanical relays but cheaper more readily available that optocoupler. We recommend optocoupler based relays where price is not a factor, solid state relays where current requirements are low (less than 2 amp) and mechanical relays for beginners or anything else. 

- Relay capacity: Almost all relays are rated to work with a voltage and current range. Most mechanical relays are rated for 10 amp, 240volt AC, while solid state relays are generally rated for 240volt AC, 2 amp. Depending upon what type of equipment you will be powering, choose appropriate relays. Equipment is generally rated in watts, and watt = volt x ampere. For example, a 100-watt heater will require at least 1 amp relay to be powered safely by 110volt AC.

- Number of relay channels: The number of channels in a relay board determines how many AC connections can be controlled. Since we are building a 4 outlet power strip, we’ll go with a 4 channel SSD relay. We’ll need one GPIO pin of Raspberry Pi for each channel on the relay. It is possible to control around 18 channel relays using the Raspberry Pi alone (it can be extended to thousands using an IO expander).


### Bill of Materials

- [Raspberry Pi Zero](https://www.adafruit.com/product/3400) or Raspberry Pi 3(https://www.adafruit.com/product/3055) 
- [microSD card](https://www.adafruit.com/product/2693)
- [5v 2.4 amp AC adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- [4 Channel SSD relay](https://www.amazon.com/gp/product/B00ZZVQR5Q/)
- [AC Power adapter with fuse](https://www.amazon.com/gp/product/B00ME5YAPK)
- [AC Power cord](https://www.amazon.com/gp/product/B00005113L/)
- [AC receptacles](https://www.amazon.com/gp/product/B002DQT5UK/)
- [Female-female jumper wires](https://www.amazon.com/gp/product/B00DJY4RS0)

### Wiring

![breadboard](https://reef-pi.github.io/img/power/breadboard.png)


### Install & Configure reef-pi

- Follow the reef-pi installation [guide](/guides/install) to setup reef-pi on Raspberry Pi zero.

- Enable equipment capability and turn off dev mode under setting section on system tab


![capability](https://reef-pi.github.io/img/power/capability.png)

- Click on the *Update* button to save settings followed by *Reload* button to ensure the changes are loaded immediately. Refresh your browser (since reef-pi is reloading, it may take few seconds). You should see the Equipments tab now.

- Navigate to System tab again and declare outlets. Use the GPIO pin numbers (*not serial number*) to define one outlet per relay channels. You can use the recommend pinout scheme to decide which GPIOs to use. They should mimic the exact wiring.


![add outlet](https://reef-pi.github.io/img/power/outlet_add.png)

- Since this guide uses a four channel relay, we are declaring 4 outlets.

![add outlets](https://reef-pi.github.io/img/power/outlet_all.png)


Note: the pin number represents the GPIO Pin number, not their position on the Raspberry Pi. Refer Raspberry Pi pinout [diagram](http://www.jameco.com/Jameco/workshop/circuitnotes/raspberry_pi_circuit_note_fig2.jpg) for GPIO numbers.

- The outlet declaration is one-time procedure; it will not change unless electronics are updated.

- Next declare equipments under the Equipment tab. Each equipment should have an assigned outlet. 

![add equipment](https://reef-pi.github.io/img/power/add_equipment.png)

- Since we have four outlets in this build, we are declaring four essential equipments for a pico reef tank.
![all equipment](https://reef-pi.github.io/img/power/all_equipment.png)

That's it, you should be able to use reef-pi to control all four equipments.

### Usage

#### Controlling equipment on-demand

Any equipment specified in the configuration file can be switched on or off any time using reef-pi web interface. Use the equipment tab to navigate to the list of equipment and click on the on/off button to switch the equipment on/off. Every equipment should have a dedicated button indicating the equipment's real-time state.

![on-demand ui](https://reef-pi.github.io/img/power/on-demand.png)

#### Controlling equipments using timers

Timers in reef-pi allows automation of an action on a piece of equipment on a defined schedule.

In the following example, we are setting up the heater to start at night 10:00 PM and stop at morning 6:00 AM. Use the "Timers" tab to define two timers. Each timer represents an action reef-pi takes. 

The first job starts the heater at night. reef-pi allows us to specify which equipment to take action against, time details (day of the month, hour, minute, second etc) and the action (on or off). Notice "\*" is used to denote every day of the month.

![timer start](https://reef-pi.github.io/img/power/timer_start.png)

And another job to stop the heater every morning 6 AM.

![timer start](https://reef-pi.github.io/img/power/timer_stop.png)

reef-pi uses [cron](https://en.wikipedia.org/wiki/Cron) style specification for denoting time schedule, this allows much more elaborate way of specifying schedules. 

A typical schedule specifies day and time related details for the timer.

Following is a summary of the specification

- "day of month" represents which day of every month the job will be triggered. Values can range from 1 to 31
- "hour" represents which hour of the day the job will be triggered. Values can range from 0 to 23
- "minute" represents which minute of the hour the job will be triggered. Value can range from 0 to 59
- "second" represents which second of the minute the job will be triggered. Values can range from 0 to 59


Other than their mentioned ranges, each of this field can also take few special entries.

They are:

- "\*" represents **every** possible value. If a \* is specified for a value, it will be triggered in every value for that specification. For example, a \* entered into the "hour" field will trigger the job every hour.
- "-" to represent **ranges**. For example, "hour" can be specified as "2-6" to trigger a job every hour from 2 to 6
- "/" to represent a **repeating period**. For example: an "hour" value of "\*/3" will cause the job to be triggered once every 3 hours.

More details can be found in  the underlying library's [documentation](https://godoc.org/github.com/robfig/cron#hdr-CRON_Expression_Format)

Timers can be used to automate use cases like two part dosing, refugium light etc.

### A note on outlet limits

reef-pi uses one GPIO  for rach outlet control. Thus, a single reef-pi can control at most 26 outlets (because there are 26 GPIOs). But a build using all 26 GPIO will not be able to support most other modules, since water level sensor (used for ATO) and mechanical swicthes/push buttons also uses GPIOs. But if you do want to use reef-pi this way, Disable spi, one wire , i2c and pwm via raspi-config utility to use all 26 GPIO.

It is safe to use reef-pi build can control at most 22 outlets. Enable i2c, pwm and disable spi,uart to use 22 GPIO pins. This leave 1 GPIO for water level sensor, 1 for temperature sensor and two for i2c communication (for pca9685 pwm IC).

If all GPIO pins are used up for relays, then none can will be left to be used for ATO or any other modules that require inlets (where GPIOs are used to read data). While planning, consider how many inlets (ATO, leak detector) or any other use (like mechanical push buttons, buzzers etc), total number of outlets and inlets has to be less or equal to total available GPIO pins. For example, a build for 2 ATO, 1 leak detector, 1 buzzer, 1 push button can support 17 outlet relays at max (2+1+1+1 + 17 == 22), while allowing temperature and ph probes.

### Notes for builds from scratch

- Always switch using the Hot wire, not with the neutral wire
- Stick to country specific color coding scheme. For US


### Resources

- [Fritzing project file](https://github.com/reef-pi/DesignFiles/raw/master/PowerStrip.fzz)
- [Cron syntax cheatsheet](https://healthchecks.io/docs/cron/)


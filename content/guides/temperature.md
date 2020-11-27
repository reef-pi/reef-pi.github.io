---
author: "Ranjib Dey"
date: 2017-09-27
linktitle: temperature
title: Temperature controller
highlight: true
draft: true
weight: 6
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
- temperature controller
- iot
---

Maintaining a stable temperature is a key requirement for a thriving reef tank. Most reef tanks maintain a stable temperature within 77 to 80 degree Fahrenheit for optimal coral growth. Depending upon the environment where reef tank is located this might require cooling down the tank using a chiller or heating it up with a heater. Because environmental temperature varies during day and night at most places, reef tank temperature is often monitored and controlled automatically using a controller. Heaters are also most frequently failed equipment in a reef tank, leading to tank crash. Temperature controller helps in avoiding such catastrophic situation as well. A beginner friendly [guide](https://learn.adafruit.com/reef-pi-guide-3-temperature-controller) is also available on adafruit.com as well.

In this guide we'll be using reef-pi to build a temperature controller that will monitor the temperature of reef tank and turn on the heater or cooler when the temperature goes above or below a specified range.

### How it works

reef-pi can monitor reef tank temperature using a DS18B20 temperature probe. The temperature controller inside reef-pi can be configured to check this sensor value periodically and if its goes above or below a certain range, reef-pi can switch on or off a specified heating or cooling equipment. Generally, a heater is used as a heating equipment and fan or chiller is used as a cooling equipment.

### Things to consider

- Temperature probe: There are many types of DS18B20 probes available. Go for the ones that are made for sub-merged usage. Also, pay attention to the outer coating material. Most submersible ds18b20 probes are made of steel but often time they show rust within the first couple of months of usage. There are ways to rust proof them without significantly altering the probing capability, like using a [heat shrink tube](https://www.adafruit.com/product/1020) or [plasti dip](https://www.amazon.com/dp/B00I9SK8XY/) or silicone dip. But there are also other submersible probes (like the ones from canakit and sparkfun) which has a black coating around them, they last longer but costlier compared to the bare steel probes.

- Heater and cooler choice: reef-pi internally only control relays which in turn control the cooling or heating equipment. In most cases, heaters are used as heating equipment. Generally, it is recommended to have two to five watts per gallon worth heating capacity, i.e. a 30 gallon tank should use at least an 100-watt heater. Multiple heaters can be used to for a single tank. For cooling, if the ambient temperature is not more than 3 to four degrees higher, fans work. Otherwise, a chiller is the best option.


### Bill of materials

- [Pi zero](https://www.adafruit.com/product/3400) or [Pi 3](https://www.adafruit.com/product/3055)
- [micro sd card](https://www.adafruit.com/product/2693)
- 5v 2.4 amp [power adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- [DS18B20 temperature probe](https://www.amazon.com/dp/B01B27R21Y/)
- One [4.7K resistor](https://www.amazon.com/dp/B072BL2VX1/)
- Relay, with at least 2 channels [example](https://www.amazon.com/dp/B00E0NTPP4)
- AC receptacles [example](https://www.amazon.com/gp/product/B002DQT5UK/)
- [3.5mm female, panel mount audio jack](https://www.amazon.com/dp/B013AP77T8)
- [3.5mm male audio jack](https://www.amazon.com/dp/B00MFRZ2SG/)
- [Jumper wires](https://www.amazon.com/dp/B00DJY4RS0)

### Wiring

![breadboard](/img/temperature/breadboard.png)


### Installation & Configuration

- Follow reef-pi installation [guide](../../guides/intro) to setup reef-pi on Raspberry Pi.

- Once reef-pi is installed, enable **temperature** sub-system under Configuration -> Settings tab. Click on the **Update** button, and **reload** reef-pi. Temperature sub-system depends upon **Equipments** sub-system, make sure it is enabled.
![temp-capability](/img/temperature/temp-capability.png)

- Reloading reef-pi takes a couple of seconds. Refresh your browser, temperature tab should appear in the reef-pi web interface.

- Go to the temperature tab, select **Enable** and click on **update** button to start temperature monitoring . The **Check interval** setting dictates how frequently reef-pi will read the temperature probe.
![temp-enable](/img/temperature/temp-enable.png)

- Temperature readings chart will appear in both temperature controller tab as well as main dashboard soon after the first check (1 minute by default)
![temp-chart](/img/temperature/temp-chart.png)


- Once temperature monitoring is enabled, you can also enable temperature control, by selecting the **Control** checkbox. Once temperature control is enabled, reef-pi will automatically turn on or off heater or cooler equipment when temperature goes outside specified range. Select heater and cooler equipment from dropdown box. You can also update the default temperature range.
![temp-control](/img/temperature/temp-control.png)

- The temperature controller can also be configured to send email alert if the temperature goes outside a specified range. To enable this, select **Enable alerting** checkbox. You can update the temperature threshold as well. You have to configure email alert under telemetry configuration for temperature alert to work. [Telemetry guide](/build-guides/telemetry) provides details  on how to do this.
![temp-alert](/img/temperature/temp-alert.png)

### Resources

- Adafruit [tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-11-ds18b20-temperature-sensing?view=all) on ds18b20 probe and Raspberry Pi
- [Fritzing project file](https://github.com/reef-pi/DesignFiles/raw/master/temperature.fzz)

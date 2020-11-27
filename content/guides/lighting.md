---
linktitle: lighting
author: "Ranjib Dey"
date: 2017-09-25
title: Lighting controller
draft: true
highlight: true
weight: 7
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- iot
- lighting controller
- kessil
---

Lighting is one of the key aspects of a maintaining a thriving reef tank. Most corals in reef tanks are photosynthetic and require lighting from a specific spectrum (400-700 nm). Different corals prefer different intensities of lighting for their optimal growth; these are generally specified in PAR (photosynthetically active radiation) values. For example, acropora species prefer higher PARs (250 and above) while acan and mushroom species prefer lower PARs (less than 150).

In a typical reef, tank lights are used to simulate diurnal cycle, which is also referred as sunrise to sunset effect. As part of this, lights are turned on a specific time followed by gradually increasing intensity to attain a peak, then gradually decreasing the intensity to finally switch off to simulate a 10 to 12 hour total lighting period.

Other than performing the diurnal cycle lighting intensity is also controlled while introducing new corals in the tank to ease the acclimation process. Corals acclimate easily in a new tank with low lights, so light intensity is brought down when new corals are added and then gradually adjusted to the normal diurnal settings over a period of few days.

reef-pi allows automation of T5 and metal halides using [equipments and timers](/power/), to gradually switch on/off multiple T5/metal halides since they do not offer intensity control.

This build guide specifically covers LED automation which allows intensity control, to simulate diurnal cycle or perform on-demand controls (for things like photography). Given there are a wide variety of LED lights available, we’ll only cover one of the most popular LED light, i.e Kessil. Though this guide walks through building a Kessil controller, reef-pi can easily control most of the popular LEDs with minimal changes on the electronics side, and without any software changes. A beginner friendly [light controller guide](https://learn.adafruit.com/reef-pi-lighting-controller) is also available on adafruit.com.

### How this work

reef-pi runs on Raspberry Pi and uses a separate breakout board (PCA9685) to generate 5 volts [PWM](https://en.wikipedia.org/wiki/Pulse-width_modulation). It is this PWM output that is used to simulate variable voltage, which in turn controls the intensity of LED lights.

Because Kessil lights expect 10-volt control signals instead of a 5-volt signal, an [NPN transistor](https://en.wikipedia.org/wiki/Bipolar_junction_transistor#NPN) is used to convert the 5-volt signal coming out of the PCA9685 board to 10-volt signal, provided by a 12-volt power adapter. A 1K and a 10K resistor is used to safeguard the signal. The resistor values do not need to be 1K and 10K, they can be anything as long as the resistor connected to PCA9685 signal is higher than the resistor connected to the 12v power adapter. Since Kessil lights have two control channels setup, we wire up two current control circuits, each with its own transistor and resistors to control the signal. Finally, we connect the two 10 volt PWM signals along with a ground connection to a female audio jack, since Kessil lights use audio jacks to supply control signal.

### Things to consider

- Because this guide covers Kessil light controller which has separate power and control signal inputs we use this specific transistor and resistor setup. The same logic can be used to generate almost any type of control signals using a different transistor or power MOSFETs. Choose a transistor or MOSFET that can operate at logic level (i.e. 5 volts) and withstand the expected output current.

- Though we are using only two channels for this guide, it should be noted that the PCA9685 board can generate up to 16 channels. Which means we can control as many as 16 channels using this board. Unlike Kessil, some of the LED lights provide more than two channels for control, having additional channels can help there. It is also possible to use additional channels to control more than one light independently or even control DC pumps (wavemakers or dosing systems).

- Some of the LED lights expect analog control signal instead of PWM. In such cases, a simple low pass filter circuit made of only resistors and capacitors can be used to convert the PWM signal coming out of PCA9685 to an analog signal. [This article](https://provideyourown.com/2011/analogwrite-convert-pwm-to-voltage/) provides guidance to create such a circuit.


### Bill of materials

- [Pi zero](https://www.adafruit.com/product/3400) or [Pi 3](https://www.adafruit.com/product/3055)
- [micro sd card](https://www.adafruit.com/product/2693)
- 5v 2.4 amp [adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- [PCA9685 breakout board](https://www.adafruit.com/product/815)
- Two [PN2222 transistors](https://www.adafruit.com/product/756)
- Two [10K resistors](https://www.adafruit.com/product/2784)
- Two [1K or 2.2K resistors](https://www.adafruit.com/product/2782)
- [3.5mm female, panel mount audio jack](https://www.amazon.com/dp/B013AP77T8)
- [3.5mm male audio jack](https://www.amazon.com/dp/B00MFRZ2SG/)
- [12v DC power adapter](https://www.amazon.com/dp/B01ICSD93Q/)
- [Jumper wires](https://www.amazon.com/dp/B00DJY4RS0)

### Wiring

![breadboard](/img/light/breadboard.png)


### Installation & Configuration

- Follow reef-pi installation [guide](../../guides/intro) to setup reef-pi on Raspberry Pi.

- Once reef-pi is installed and running go to systems page, enable lighting capability and reload reef-pi

![systems](/img/light/setup_1.png)

- PWM outputs such as the ones that used for light controls are called *jacks* in reef-pi. A jack can have multiple channels. Each channel is represented by the controlling pin number of the PCA9685 board. For a Kessil controller, we will be declaring a jack named *J1* with two pins, each pin number separated by a comma, under the system tab.

![jacks](/img/light/setup_2.png)

- Once the jack is declared we can head to lighting tab and declare lighting equipment. We’ll use an example [A80](http://www.kessil.com/aquarium/Saltwater_A80_Tuna_Blue.php) Kessil light and assign the J1 jack created above to it.

- reef-pi will now show corresponding control settings under the A80 light. Select the inverse checkbox to indicate that our actual generated control signal should be inverse of our specified values, this is a side effect of using an NPN transistor which operates in [sinking current](https://electronics.stackexchange.com/questions/74636/sinking-and-sourcing-current) mode.

![light](/img/light/setup_3.png)

### Usage

#### Making on-demand changes

reef-pi will show a single slider for each channel defined in a light. This can be used to control the signal of that channel. Users can use the slider to set a specific value and then hit the update button to see the effect. In this mode user directly control the value of the output signal.

![manual](/img/light/setup_4.png)

#### Setting up 24 hour light cycle

Alternatively, users can also choose the automatic mode, by selecting the *auto* checkbox, which will render 12 vertical sliders each representing expected control signal values at 2-hour intervals, thus providing the user with 24-hour automatic controls. Specify the desired diurnal cycle values and click on the *update* button. reef-pi will automatically compute the right values for current time and apply it.

![auto](/img/light/setup_5.png)

### Resources

- Adafruit [tutorial](https://learn.adafruit.com/adafruit-16-channel-servo-driver-with-raspberry-pi?view=all) on PCA9685 board and Raspberry Pi.
- [Fritzing project file](https://github.com/reef-pi/DesignFiles/raw/master/PowerStrip.fzz)
- [reef2reef build post](https://www.reef2reef.com/threads/reef-pi-1-0-release-building-a-kessil-controller.343672/#post-4281610)

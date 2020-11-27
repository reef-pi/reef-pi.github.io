---
author: "Ranjib Dey"
date: 2018-11-15
linktitle: Introduction
title: Overview
highlight: true
weight: 1
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

This section provides a high-level overview of build and maintenance process of a reef-pi controller and some tips and tricks around common build aspects such as [circuit](/guides/electronics) or [enclosure](/guides/housing) construction and individual modules. Please read through this documentation before starting with an actual build.

### Plan

reef-pi is a versatile and modular controller that allows users to customize their controller for their specific needs, tuned to their particular hardware and aquarium setup. Decide on the features you want to build first. A set of target features can then easily be broken down to required components and other build work. The build process involves installing software on Raspberry Pi, soldering electronics and fabricating an enclosure (housing). None of this is hard to do, and one can definitely learn on the go, but the overall effort and time involved in this project will highly depend upon your skill and prior experiences with such projects. reef-pi is aimed for beginners in computers, electronics, and reef keeping. *You don't need to know software programming* to build and operate reef-pi. reef-pi build process will require tools for soldering circuits, fabricating enclosure and keyboard/TV to configure Raspberry Pi. The parts list associated with each guide does not include these tools. Due to the complexity of this project and various parts involved, error and setbacks are very common, but rarely a show stopper. Don't be dishearted, use the [troubleshooting guide](/guides/troubleshooting/) when needed. Users are also encouraged to ask questions in their preferred method from all the available options (email, reef2reef forum, GitHub issue or slack channel). Generally, it takes a few days to a few weeks to build a fully functional reef-pi controller. This does not include the time spent in reading/researching or ordering the components. Include this time requirement when you plan your build. But this is worth it. For most of us, it has been a good learning experience as well.

### Order components

Individual reef-pi build guides provide links to purchase required components. Other than Raspberry Pi, reef-pi mainly uses [Adafruit](https://www.adafruit.com) products. There are few ancillary components that are sourced from Amazon. If you are in the US, I recommend using Adafruit, since the guides and my personal builds are tested against their products. Users are welcome to use alternatives (e.g. different vendors or salvaging older electronics). When the software requires a specific component, we explicitly call it out. We also highly recommend salvaging older electronics. reef-pi assumes users are making judicious choices and are aware of the risks when choosing alternative components. Almost all the components can be ordered in steps. Users can get started with just a Raspberry Pi, and order components later on, incrementally working on the build. This allows iterative build process.

### Build the physical controller

During the actual build process, follow the module specific build guide. Refer to the [circuit guide](/guides/electronics) for wiring specific instructions. This is the most exciting part of the build. Make sure you have all required tools (e.g. soldering iron, drill kit etc) beforehand. There are few existing reef-pi build threads in reef2reef that users can refer to for getting locality specific supply chain information or alternatives.

Following is a list of introductory guides on how to build reef-pi controller. Start with the [first guide](https://learn.adafruit.com/reef-pi-installation-and-configuration) that covers software installation & cofiguration and then use the individual feature specific guides to build your physical controller. Some of the features such as [Auto Top Off](https://learn.adafruit.com/reef-pi-water-level-controller) or [Temperature controller](https://learn.adafruit.com/reef-pi-guide-3-temperature-controller) relies on other features, like [Power controller](https://learn.adafruit.com/reef-pi-power-controller).

  - [Software installation & configuration](https://learn.adafruit.com/reef-pi-installation-and-configuration)
  - [Power controller](https://learn.adafruit.com/reef-pi-power-controller)
  - [Temperature controller](https://learn.adafruit.com/reef-pi-guide-3-temperature-controller)
  - [Auto Top Off]( https://learn.adafruit.com/reef-pi-water-level-controller)
  - [Light controller](https://learn.adafruit.com/reef-pi-lighting-controller)
  - [pH Monitor](https://learn.adafruit.com/reef-pi-guide-7-ph-monitoring)
  - [Dosing controller](https://learn.adafruit.com/reef-pi-guide-5-dosing-controller)

In addition to these guides, further documentation around customization and troubleshooting is provided in the [guides](/guides) section here.

### Test the functionalities you'll be using

Thoroughly test your reef-pi controller after it is built, before putting in action to safeguard your livestock. reef-pi is under active development, and like all software can contain bugs, the DIY nature of reef-pi controller makes it more vulnerable to errors and inefficiencies in the due process, this is the risk that comes with its customizability. For every module, test the features you will be using and validate it with at circuit level (multimeter or equivalent) and functionally (attaching test equipment, in spare water container or tank, etc).

### Deployment for permanent installation

Once tested, secure your circuit and all electronics component in a suitable housing. We have a [dedicated guide on building housing](/guides/housing). We strongly recommend fixing reef-pi housing in a stable platform. The exact options for fixing will depend on the enclosure. Most plastic enclosure based builds weigh fairly less and can be secured using Velcro strips on the wall or your aquarium cabinets. After this, your reef-pi controller is pretty much ready for use. Unless there are some hardware maintenance or upgrades, you are unlikely to touch the controller enclosure.

### Maintainence and other operations

reef-pi runs on Raspberry Pi, which uses Linux operating systems. Just like reef-pi Linux is also under active development, and we recommend users to update their Linux/Raspbian installation quarterly and do a full OS upgrade (new version of Raspbian or Noobs, whatever you are going for) after every two years at least. reef-pi major releases happen every year near Thanksgiving, we strongly recommend you to consider upgrading your reef-pi software during this time. Smaller releases happen every quarter to sometimes after every two weeks (bug fixes, experimental features etc.. we are big on developing small steps and releasing frequently).
Other than updating/upgrading your build software, you may need to do some troubleshooting when you encounter any hardware failure or software bug or during the update/upgrade process of software or hardware. We have [a dedicated guide on troubleshooting](/guides/troubleshooting) that covers most frequently encountered problems. For general build and reefing related help use reef2reef. We also encourage you to start a build thread in reef2reef if possible, so that others can learn from your experience as well.

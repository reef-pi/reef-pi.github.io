---
author: "Ranjib Dey"
date: 2018-08-24
linktitle: values
title: Values
highlight: true
weight: 6 
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- iot
- adafruit
---

reef-pi project has three core values: affordable, modular and extensible. These are the guiding force behind key decisions and development strategies. This section of the documentation details how reef-pi project interpretes these values

## Affordable

- Prefer easy to source parts.
- Be frugal, encourage salvaging older electronics component.
- Encourage  user specific hacks and workaround that may significantly lower the build cost or time.
- Safety and reliability of the controller is not a yes or no question, its a compromise and we only encourage the current best practices.
- reef-pi project may deliberatly compromise some feature and perfromance to avoid expensive and propreitory components.


## Modular

- reef-pi software will always allow individual modules to be run independantly
- Only exception to these rule is where one module is functionally dependant on another module
- reef-pi will allow and provide avenue for maximum utilization the hardware features even with module specific builds whenever it is possible.

## Extensible

- reef-pi will always provide UI based on API. API is the cornerstone of reef-pi's extensibility.
- reef-pi project will always be open to all usage of the API, including out of tree UI or mobile clients.
- reef-pi development will always thrive to preserve API stability by sticking to semver. This will ensure components that extend reef-pi using API can gurantee their correctness for a fixed timer period against a fixed reef-pi version(s).


Note, other than these three core values reef-pi project also respect and abide [Opensource](https://opensource.org/) ethos, [Contributor covenant code of conduct](https://www.contributor-covenant.org/) and [reef2reef](https://www.reef2reef.com/help/terms) community guidelines whenever they are applicable. These are apriori and not detailed here.


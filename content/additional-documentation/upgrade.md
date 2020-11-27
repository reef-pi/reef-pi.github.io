---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: upgrade
title: Upgrade
highlight: true
weight: 2
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

- A running reef-pi controller version is always visible from the dashaboard footer.

![reef-pi version](/img/upgrade/version.png)

- Determine appropriate reef-pi version based on raspberry pi (3 or zero) from the [release](https://github.com/reef-pi/reef-pi/releases/) page. Choose latest relase if you are unsure. For this documentation we'll use 1.0 release version on pi zero.

- Open a terminal window using the ssh software of your choices.  SSH into your raspberry pi, then login into reef-pi and upgrade by entering the following commands in the terminal window

- Download the release package on reef-pi (remember to use the correct pi-x.x package number)
```
wget -c https://github.com/reef-pi/reef-pi/releases/download/0.5/reef-pi-1.0-pi0.deb
```

- Install the downloaded reef-pi version
```
sudo dpkg -i reef-pi-1.0-pi0.deb
```

- Check reef-pi is running suscessfully using
```
sudo systemctl status reef-pi.service
```


- NOTE: If using wifi change go to the configuration tab and change interface setting to wlan0

- Or you can use the procedure listed here: http://reef-pi.github.io/additional-documentation/development

- Clear browser cache to reload the new UI

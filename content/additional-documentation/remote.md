---
author: "HM3105"
date: 2017-09-15
linktitle: remote
title: Remote Access
highlight: true
weight: 5
---

This guide  meant to assist in establishing a remote connection to your reef-pi main control page using one of the two popular options, [RealVNC](https://www.realvnc.com) and [Tor](https://www.torproject.org/projects/torbrowser.html.en). reef-pi is normally accessible only within the home wifi network, using any of these two approaches you can access reef-pi from anywhere.


### RealVNC

The first option is to use software such as Real VNC. They offer a cloud option that will allow you to access your Raspberry Pi from anywhere. Please note, this option logs you into the Pi like a remote desktop connection. From there you would be able to use Chromium in the Pi to access reef-pi. 

This solution is available for both Android and iOS. Installation is easy, just follow the directions on the links below.

- Raspberry Pi [instructions](https://www.realvnc.com/en/connect/docs/raspberry-pi.html#raspberry-pi-setup)
- Software [download](https://www.realvnc.com/en/connect/download/viewer/)

### TOR

The other option is to use Tor. Tor has a nifty function that is fairly secure and relatively easy to set up called *Hidden Services*

- We recommend following the [directions](https://www.symantec.com/connect/blogs/tor-hidden-services-home-device-and-services-security-and-privacy) provided by Symantec. At various place the guide gives you the code to enter in the command prompt. 

- On step 3 where it tells you to "Edit file /etc/tor/torrc" you'll have to use the command "sudo nano /etc/tor/torrc".

- For step 4, follow the directions *except* make the following changes.

```
HiddenServiceDir /home/debian-tor/hidden_service/
HiddenServicePort 8080 192.168.1.78:8080
HiddenServiceAuthorizeClient stealth user1
```

You'll notice the IP address matches the local address used to access reef-pi via your local network, just make sure it matches with what you use to access the reef-pi over your local network.

You can change the "user1" entry to whatever you want. Remember, the *stealth* entry right before the "user1" is important,  that entry makes your hidden service only viewable by people with the specific key (which you'll get in step 7. The "user1" generates a new key. If you want to have multiple users, just change the "user1" entry and you'll end up with a new key.

Follow the rest of the directions for getting a Tor client and browser for your computer and Andriod device (haven't been able to locate an iOS option for this yet) and you will be ready to go.

Please note: Tor is slow. Right after you've created your Hidden Service it may take 10 minutes for the Tor network to populate and allow the connection. In addition, it may take 1 minute for the reef-pi page to load. Once it's loaded them the delays are considerably reduced.

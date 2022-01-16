---
author: "HM3105"
date: 2022-01-16
linktitle: remote
title: Remote Access
highlight: true
weight: 5
---
Accessing reef-pi control pages when away from home can present a challenge as by default reef-pi will only be accessible when connected to your home network.

The [Tailscale](https://www.tailscale.com) VPN service provides and easy to use and secure way to access to your reef-pi remotely without requiring additional hardware or complicated setup.


### Tailscale

Tailscale enables encrypted point-to-point connections using the open source WireGuard protocol. The service is free for personal use and setup is considerably more straight forward than other approaches such as setting up port forwarding or a 'traditional' VPN. 

- [Create a free Tailscale account](https://login.tailscale.com/start) 
- Install and start the Tailscale software onto your raspberry pi following the [instructions](https://tailscale.com/download/linux/rpi) 
- Install the Tailscale app on the other devices from which you want to be able to access your reef-pi.. Apps are available for iOS, Android, Windows, Mac and other operating systems.
- Once everything is up and running, you can connect to Tailscale and access reef-pi using the IP address shown on the [machines](https://login.tailscale.com/admin/machines) tab of the Tailscale dashboard.

### Port Forwarding
Using of "port forwarding" to allow access to your reef-pi over a public IP address is not recommended. It's quite easy to mistakenly make your reef-pi instance or underlying raspberry pi available to the whole world. This could put the security of your home network at risk.

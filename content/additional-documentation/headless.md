---
author: "Andy McKay"
date: 2017-10-30
linktitle: headless
title: Headless
highlight: true
weight: 6
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

There are times when you want to get your Raspberry Pi up and running completely headlessly. Maybe you typically use a laptop and don't have an extra keyboard. Maybe you don't have an easy way to connect to an HDMI monitor. This guide will show you how you to set up your Pi to be completely headless. This will allow your Pi to connect to your wireless network and connect via SSH on its first boot. 

Please read all steps before starting the process so that you're familiar with what will be required.

Before we begin, we need to gather a couple of pieces of information. We will need the following:

a. The SSID and Password for your wireless network.  
b. The IP address of your gateway and DNS server. In a home environment, these addresses will be the same IP. To check this information, you can type *ipconfig* at the command prompt of a Windows computer on the network, or *ifconfig* on a Linux/Mac computer.

1. Download and install your Raspbian image. This process is covered in detail on the Raspberry Pi site. Please visit https://www.raspberrypi.org/documentation/installation/installing-images/ for more detail on the process. As I will never be connecting to a desktop instance on this Pi, I downloaded the Raspian Stretch Lite image. If you plan on connecting to your Pi in a method other than SSH or reef-pi's web interface, please consider the Raspian Stretch with Desktop image.

2. To get your Pi up and running on your wireless network, with SSH enabled, We will need to modify some files on the memory card you just created. This will present a small challenge because, unless you're running Linux, you will not be able to read the Ext4 filesystem that is on the card. In fact, if you attempt to read this partition with a Window computer, it will prompt that you need to format the partition before you can use it. Please do not format it. You will just need to start over at step 1. 

   We have a couple of options to do this:

   A. Boot into Linux using a LiveCD or bootable USB stick. Creating a bootable USB stick is probably the easiest method. For instructions on how to create a bootable USB stick, please visit one of the following links:

   Windows: https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-windows  
   macOS: https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-macos

   B. There are software packages that will allow you to read/write Ext4 filesystems on Windows and Macintosh computers. If you choose this options, please read the instructions and any applicable warnings and caveats for each piece of software.

   **Windows:** Ext2FSD can be found at https://sourceforge.net/projects/ext2fsd  
   **macOS:** Fuse can be found at https://osxfuse.github.io/

   **NOTE:** I recommend using the bootable USB option over installing the software file system drivers.

3. We will now create and modify some files to both enable SSH and WiFi. When you plug your cardreader with the card you just created for the Raspberry Pi in it into the computer after booting into Linux (or after installing on of the filesystem drivers) you will see two partitions. We have a task in each partition:

   A. In the root of the "boot" partition, create an empty file with the filename "ssh". This will enable SSH on the Pi.

   B. In the main Ext4 partition on the card, we will need to modify 2 files:
   ```
   /etc/wpa_supplicant/wpa_supplicant.conf
   /etc/dhcpcd.conf
   ```

   **Editing /etc/wpa_supplicant/wpa_supplicant.conf:**

   By default, the file will contain the following:
   ```
   ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
   update_config=1
   ```

   We will need to add the following lines to the file:
   ```
   network={
   ssid="SSID"
   psk="PASSWORD"
   }
   ```

   Replace SSID and PASSWORD with the proper SSID and password for your wireless network.

   **Editing /etc/dhcpcd.conf:**

   We will need to add the following lines to the bottom the file:
   ```
   interface eth0
   static ip_address=192.168.1.100/24
   static routers=192.168.1.1
   static domain_name_servers=192.168.1.1

   interface wlan0
   static ip_address=192.168.1.101/24
   static routers=192.168.1.1
   static domain_name_servers=192.168.1.1
   ```

   You will need to change the router and domain_name_servers IP addresses to the address(es) you gathered above. You will need to change the ip_address for each interface to a value that will be unique on your network. The first 3 numbers will be the same as your gateway, with the fourth being a number between 1 and 255 that is unused. You should be able to see the addresses in use via the interface of your router. 

   For example, if your router's IP is 192.168.1.1, then you could use 192.168.1.100 and 192.168.1.101. 

4. Once all changes have been saved, you can now insert the memory card into your Raspberry Pi and power it on. 

5. Using the SSH client of your choice, open an SSH connection to the IP address you entered for the wlan0 interface above. You should now connect to your Raspberry Pi, where you can log in with the default username "pi" and default password "raspberry". 

6. You should now update your Pi's system with the following commands:
   ```
   sudo apt-get update -y && sudo apt-get upgrade -y
   ```

7. We will now use Raspberry Pi Software Configuration Tool to modify some options. Enter the following command:
   ```
   sudo rapsi-config
   ```

   A. Change your user password using option 1.  
   B. Set the hostname of your Pi to something meaningful on your network with option 2.  
   C. I recommend setting the system to boot to the console, requiring the user to log in with option 3, and then B1.  
   D. Set up your locale, time zone, and WiFi country with option 4.  
   E. Select "Finish" to save changes and exit the tool.

8. Enable i2c, onewire, spi, and uart by editing the file /boot/config.txt. The following lines will need to be added:
   ```
   dtparam=i2c_arm=on
   dtparam=spi=on
   dtparam=audio=on
   enable_uart=1
   dtoverlay=w1-gpio
   ```

9. Enable NTP to synchronize the Pi's date and time. Enter the following commands:  
   ```
   sudo systemctl start ntp.service
   sudo systemctl enable ntp.service
   ```

10. System configuration is now complete. It's now time to reboot the Pi with the following command:  
   ```
   sudo reboot
   ```

11. Once the Pi has rebooted, re-establish an SSH connection and log in using the new password you set in step 7A above.

12. We can now download and install the reef-pi software. Download the software with the following command:  
   ```
   wget https://github.com/reef-pi/reef-pi/releases/download/0.7/reef-pi-<Version and Platform>.deb
   ```
   Check the following site for the latest version: https://github.com/reef-pi/reef-pi/releases. "Platform" refers to the download for the Raspberry Pi 3 or the Raspberry Pi Zero.

13. Once downloaded, install the software with the following command:  
   ```
   sudo dpkg -i reef-pi-<Version and Platform>.deb
   ```

14. Check that reef-pi is running with the following command:  
   ```
   sudo systemctl status reef-pi.service
   ```

   You should now be able to connect to the web interface using a web browser on another computer on your network at the following address:
   ```
   http://<ipaddress>:8080
   ```

   <ipaddress> will be the IP address for wlan0 set in set 3B and the IP address used to to SSH into the Raspberry Pi.

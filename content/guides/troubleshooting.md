---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: Troubleshooting
title: Troubleshooting
highlight: true
weight: 12
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

- Check if reef-pi is running

```
sudo systemctl status reef-pi.service
```

- Check for errors in log

```
sudo journalctl -fu reef-pi.service
```

- Connecting reef-pi using a TTL cable. Adafruit has an excellent [tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable?view=all) on how to use USB TTL cable to configure raspberry pi, in cases where display and keyboard is not available.


- Check reef-pi version (helps in bug reports)

```
reef-pi -version
```

- Resetting reef-pi's database

```
sudo systemctl stop reef-pi.service
sudo rm -rf /var/lib/reef-pi/reef-pi.db
sudo systemctl start reef-pi.service
```

- One of the common reason gotcha is dev_mode being enabled. Dev mode allows reef-pi development in non-raspberry pi system and it mask all physical control (they are faked out). Make sure dev_mode is disabled or unchecked, under **Configuration -> Settings -> Capabilities**. Note: changing any of the capabilities will require a reload to take effect.

- Troubleshooting circuits: A common mistake is to have loose connection acros jumper wires or pins. A systematic way to identify and fix them is to check for continuity using a multimeter. Another common mistake is to have shorted or mismatched wiring (such as transistor based circuits), which can be identified by checking expected voltage at every connection.

- reef-pi uses the time settings from raspberry pi/raspbian. If timer are not acting as expected check if system time is configured correctly. Make sure timezone is configured correctly using **raspi-config**. 

- reef-pi API can be used for a variety of troubleshooting purpose, specifically when the UI is problematic. To use the API, use curl. reef-pi uses cookie based authentication, users have to create a auth cookie first and then use it for all further API based operations. API covers all aspects of reef-pi and powers the UI. Here is an example of listing number of equipments

```
curl -X POST -c cookie.txt -d '{"user":"reef-pi", "password":"reef-pi"}' http://reef-pi.local/auth/signin
curl -b cookie.txt http://reef-pi.local/api/equipment
```
API can be used to create backup, check a specific equipment, ato, ph probe etc, or to automate more complex workflows using ancillary scripts. 



- Using reef-pi db command

`reef-pi db` is a sub command made to update and retrive reef-pi data from the database itself bypassing controller and UI layer. It is intended to be used
for troubleshooting and fixing reef-pi from data induced issues.
```
reef-pi db --help
```
```
Usage of db:
  -input string
    	Input json file
  -output string
    	Output json file
  -store string
    	Database storage file (default "/var/lib/reef-pi/reef-pi.db")
```
All configuration and controller data in reef-pi are stored as elements in distinct buckets. Individual modules have their own buckets. For example, equipment details are stored
inside the "equipment" bucket. reef-pi db command operates on buckets and elements inside a bucket. It is not aware of any other controller level details.

Example use of the *db* command:

List buckets:
```
sudo reef-pi db buckets
```
```
analog_inputs
ato
ato_usage
doser
doser_usage
drivers
```

List elements inside a bucket. Here each element in ato bucket represent individual ato's defined by the user.
```
sudo reef-pi db list ato
```
Show details of ato with id "1"
```
sudo reef-pi db show ato 1
```
Update details of ato with id 1
```
cat ato.json | sudo reef-pi db update
```

Delete analog input connector with id 1
```
sudo reef-pi db delete analog_inputs 1
```


- What information to share when asking for help? If you are still stuck, feel free to reach out to reef2reef thread on reef-pi. Please note down reef-pi version, Pi version, circuit details (an image will be very helpful) and shared those details while asking question. They help deducing the issues faster.



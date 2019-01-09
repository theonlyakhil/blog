---
title:  "Simple Home Automation using Pi Zero W, Particle.io, Google assistant and IFTTT"
search: true
categories: 
  - Raspberry Pi
  - Home Automation
last_modified_at: 2018-12-17T08:05:34-05:00
header:
  teaser: /assets/images/blog/simple-home-automation/simple-home-automation.png
---
![simple-home-automation](/assets/images/blog/simple-home-automation/simple-home-automation.png)

# Introduction

Almost everyone's dream is to have an automated home. But, automated home is expensive and developing on your own is a major task until now. Today we will make simple home automation device using Raspberry Pi Zero W that can automate a switch using relays.

# Hardware Requirements

1. Raspberry Pi Zero W - 1
2. 2 - Channel relay
3. Some wires

# Software Requirements

1. Particle.io account
2. IFTTT application

# Things to know before the build

## Particle.io Pin diagram

The pin numbering of particle.io on Raspberry Pi is different from the standard one. The below diagram will explain.

![Particle.io Pin Diagram](/assets/images/blog/simple-home-automation/particle-io-pin-diagram.png)

# Instructions

## 1. Initial step

1. Log in to github and to [this link](https://github.com/Sashuu6/my-room-automation-project) and fork the github repository.
2. Download the repository to your computer.

## 2. Particle.io

1. Goto to particle.io webIDE using [this link](https://build.particle.io/build/new).
![Particle.io Pin Diagram](/assets/images/blog/simple-home-automation/particle-io-1.png)

2. Add title and copy the code from the downloaded repository (present in code/main_program/main_program.ino) and paste it on the code editor.

3. Click on the compile ( present at left, above the folder symbol).

## 3. Setup Raspberry Pi Zero W

1. Download [etcher](https://www.balena.io/etcher/) and install it on your system.
2. Download raspberry pi stretch [image](https://downloads.raspberrypi.org/raspbian_lite_latest).
3. Flash the image to an SD card via the etcher.
4. Remove and insert sdcard into the system.
5. Create a file ssh inside boot.
6. Create another file named wpa_supplicant.conf inside boot and add the following code to insert Wi-Fi credentials.
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="YOUR_NETWORK_NAME"
    psk="YOUR_PASSWORD"
    key_mgmt=WPA-PSK
}
```
Replace YOUR_NETWORK_NAME with your WiFi's ssid and YOUR_PASSWORD with it's password.
7. Now, insert the sdcard inside the Raspberry Pi Zero W and fire up the Pi.
8. Find the Raspberry Pi's IP address. You can do that by using applications like Fling.
9. now ssh to the Pi using your Linux or Mac system. If you are using Windows ( First of all goto hell because you are using Windows), then download putty to ssh to the Pi.
10. To SSH into the Pi.
```
$ ssh pi@ipaddress
```
11. Now, update and upgrade the Pi.
```
$ sudo apt update && apt upgrade
```
12. Install particle.io client into the Pi.
```
$ bash <( curl -sL https://particle.io/install-pi )
```
You will be asked to enter your particle.io username and password. Also add the name of the Pi. Now the Pi is setup.
13. Now upload the code to the Pi (Present on the left side of the WebIDE).
![Particle.io Pin Diagram](/assets/images/blog/simple-home-automation/particle-io-2.png)

## 4. Connecting relay with Raspberry Pi Zero W

1. Connect D0 of Raspberry Pi (Refer pin diagram from above) to relay 1.
2. Connect D1 of Raspberry Pi to relay 2.
3. Connect 5v for relay's power.
4. Connect GND of Pi to GND of the 2 relays.

![Final image](/assets/images/blog/simple-home-automation/complete-image.jpg)

## 5. Setup IFTTT

1. Click '+' from the app.
![Final image](/assets/images/blog/simple-home-automation/0.jpg)
2. Click 'this'.
![Final image](/assets/images/blog/simple-home-automation/1.jpg)
3. Search google assistant and click on it.
![Final image](/assets/images/blog/simple-home-automation/2.jpg)
4. Click 'say a simple phrase'.
![Final image](/assets/images/blog/simple-home-automation/3.jpg)
5. Specify the credentials as below.
![Final image](/assets/images/blog/simple-home-automation/4.jpg)
6. Click 'that'.
![Final image](/assets/images/blog/simple-home-automation/5.jpg)
7. search and select 'particle.io'.
![Final image](/assets/images/blog/simple-home-automation/6.jpg)
8. Specify the function name.
![Final image](/assets/images/blog/simple-home-automation/7.jpg)
9. Repeat the same for the other functions functions like bulboff, tubelight on and tubelight off.

It's done. Now command your google assistant to turn on tubelight and see the wonder.
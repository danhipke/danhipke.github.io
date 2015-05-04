---
layout: post
title: "Week 5 Report"
description: ""
category: 
tags: []
---
{% include JB/setup %}

### Application GUI
This week, we finalized our frontend application design and configuration structure.  We simplified our design to include 3 tabs: "Status", "Hardware Setup" and "System Setup".  The "Status" tab will contain information about which wearables are present in which zones.  This tab will open by default when the application starts up.  The "Hardware Setup" tab will be where all of the hardware devices are configured within the application.  In this tab, the user can add or remove wearables, zone modules and electronic devices (Bluetooth outlet in our case) by having the USB dongle scan for them.  In the "System Setup" tab, the user can configure rules for which electronic devices are turned on/off when a wearable enters a specific zone.  The GUI is in place and now we are working on adding functionality to the GUI.

### Application Backend
On the application backend, we were able to get two way serial communication working between the USB dongle (an Arduino with USB serial capabilities) and the python application on the computer.  We also worked on getting the Python API for our Bluetooth outlet working in Python 3.4.

### Hardware
For the hardware, we designed and ordered a PCB for our wearable.  One side contains the wireless module while the other side contains the Arduino chip, battery leads/regulator and resistors to allow us to correctly program the Arduino.

<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/PCB1.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/PCB2.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">

We also finalized our wireless message structure for communication between the wearable, zone module and USB dongle.

<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/wireless_message_format.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">

Lastly, we created our enclosure in Solidworks.  The current dimensions are 1.25" by 1.75" by .35".  This should allow more than enough space for our PCB and battery.

<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/enclosure.JPG" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
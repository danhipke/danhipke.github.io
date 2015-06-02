---
layout: post
title: "Week 4 Report"
description: ""
category: 
tags: []
---
{% include JB/setup %}

### Hardware POC

This week in lab we finally had a chance to start building a POC with the parts we ordered.  Using the two RFM12B radio transceivers we ordered with two Arduino ATMega328 chips we already owned, we were able to communicate at 915 MHz between the two modules.  We also were able to utilize the analog signal strength values on the RFM12B to get readings with one transceiver being at the far end of the lab while the other was outside the lab with the door open.  These signal strength readings will allow us to measure proximity between the wearable and the zone modules, just as we initially planned.  The rest of the week, Ben continued developing the Arduino code that will live in the zone modules and wearable.

### Desktop Application

On Thursday, we met to do some storyboarding for the desktop application.  We established the general interface which will allow the user to perform a few key activities:

* create multiple profiles per device to save settings for which electronics (in our case a Bluetooth outlet) respond to the proximity of the user
* configure the zone modules and tagging them with a location name
* view the current status of the user's proximity to the various zone modules

We also met to establish which frameworks we would be using.  We initially went with pyGUI but found that it was rather limited in its features.  We will continue moving application development going forward with pyQt, a third-party Python binding for the Qt application framework.  Since our Bluetooth outlet has an open-source Python API, we figured that a Python-based framework would be easiest.  

During the week, Daniel, Teddy and Wes continued working on various aspects of the desktop application.  Teddy worked on learning pyGUI which lead to making the switch to pyQt to continue frontend application development. Wes worked on the application backend and storing configurations made by the user in XML, to be later combined with the frontend application. Daniel worked on writing the Arduino code for the USB dongle that would communicate with the computer over serial using pySerial.

### Next Steps

This next week, we plan to finalize the application storyboard and start working together as a group to combine the work we did separately.  We also plan to order the final parts on our BOM and designing the actual wearable enclosure and PCB to fit those components.
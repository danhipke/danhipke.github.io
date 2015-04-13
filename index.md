---
layout: page
title: CSE477 Hardware Capstone
tagline: D.R.E.W.
---
{% include JB/setup %}

## Project Proposal 
Home automation is a continuously growing field. As more and more home appliances and electronics are becoming "smart", it is important to minimize energy waste. Our product "D.R.E.W." is an attempt to solve this problem. We envision our product as a way to turn on and off various devices and electronics in your home based on how close you are to them.

### Product Details
Our product will utilize RFID tags as a way to track the proximity of users in their homes. Specifically, users will be able to put the RFID tags around their house in rooms or other key locations in the house. The wearable device will be able to measure proximity to to these tags, or (with enough tags in a room) be able to triangulate the user's exact position in a room. The user will be able to configure which devices in the room are automatically turned off when the user is far enough from the room.

#### The Tags
The tags will be active RFID tags requiring battery power. These tags can be placed in rooms across the house, with the option of multiple tags per room to allow for more fine-grained location pinpointing.

#### The Wearable
The wearable will be a bracelet which acts as an RFID reader/writer. From the bracelet, the user can program the RFID tags. The bracelet will use the signal strength from the active RFID tags to measure proximity. A higher signal strength means the user is closer to the tag and as a result, closer to the room. A lower signal strength means the user is far away from the tag/room. The bracelet will handle all programming and reading of tag signals.

#### Energy Regulator
The regulator will initially be a device that plugs into an existing home outlet and acts as an outlet for any electronic. It will control whether or not the device is turned on by regulating the flow of electricity from the outlet to the electronic to be controlled. This will be a bluetooth/wireless device that can be controlled through some external signal.

#### The Mobile Application
The mobile application will be used to control the actual home electronics and appliances. It will communicate with the energy regulator and wearable through bluetooth. When the wearable sends a signal that the user has left/entered a room, the application will send a signal to all energy regulators in the room to turn on/shut off all regulated electronics appropriately. This application will also let users configure which tags and energy regulators correspond to which rooms.

In the future, it will also allow for more precise pinpointing of user location in the room by leveraging the data from multiple tags.

### Putting It All Together
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/block_diagram.png" style="width:800px" border="5">

## Bill of Materials
* x8 RFM12B Radio Transceiver ($6.67 from http://moderndevice.com/product/rfm12b-radio/)
* x8 AVR 28 Pin 20MHz 32K 6A/D - ATMega328P ($4.30 from https://www.sparkfun.com/products/9061) 
* x1 Plugable® Bluetooth Controlled AC Power Switch for Home Automation with Android, iOS and Python Open-Source Applications ($35.00 from http://www.amazon.com/Plugable-Controlled-Automation-Open-Source-Applications/dp/B00PG50OSM/ref=sr_1_5?ie=UTF8&qid=1428885007&sr=8-5&keywords=bluetooth+power+switch)
* Batteries ($5)
* PCB
* Case 

## Journal

Here is a list of our weekly journals so far:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>




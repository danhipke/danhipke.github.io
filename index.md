---
layout: page
title: CSE477 Hardware Capstone
tagline: D.R.E.W.
---
{% include JB/setup %}

## Project Proposal 
Home automation is a continuously growing field. As more and more home appliances and electronics are becoming "smart", it is important to minimize energy waste. Our product "D.R.E.W." is an attempt to solve this problem. We envision our product as a way to dramatically reduce energy waste by turning on and off various devices and electronics in your home based on your proximity to them.

### Product Details
Our product utilizes 915MHz RF transceivers as a way to measure the relative proximity of users in their homes to central "zones". Specifically, users can to put these RF transceiver modules around their homes in rooms or other key locations in the house. The wearable device will be able to measure proximity to to these modules using relative signal strength. Through a computer application, the user will then be able to associate specific home electronics appliances, such as lights, with each zone.  

For demo purposes, we will be controlling an outlet connected to a lamp in a room with a single RF module for that zone.  When the user enters the room (is near the RF module), the outlet will be powered on and the lamp will turn on.  When the user leaves the room, the outlet will be powered off and the lamp with it.

<center><div class="video">
<iframe width="820" height="492" modestbranding="1" src="https://www.youtube.com/embed/ZIReNE54x5g" frameborder="0" allowfullscreen></iframe>
</div></center>

#### The Zone Modules
The zone modules will be RF transceivers connected to an ATMega328 chip and battery. These modules will be placed centrally in a room to allow for an easy calculation of the boundaries of the room.  These zone modules will be sending out an RF signal at 915 MHz.  The frequency and strength of the signal is high enough to accommodate large room sizes. The wearable will communicate with these modules to detect when a user has entered a specific zone.

We original envisioned these zone modules being passive or active RFID tags, but due to the high price of an ultra-high frequency RFID reader/writer, we were not able to meet the project budget using the RFID approach. 

#### The Wearable
The wearable will be a bracelet with an RF transceiver, ATMega328 chip and battery similar to the zone modules. The bracelet will use the signal strength from the zone modules to measure proximity. A higher signal strength means the user is closer to the zone module and as a result, closer to the zone. A lower signal strength means the user is far away from the zone. The amount of signal strength required for a user to be "in" a zone will be configurable through the desktop application to accommodate varying room sizes.  The only purpose of the wearable is as a way to track the user's position and communicate it back to the desktop application/central module.

<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/render.jpg" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">

<p style="text-align:center"><i>Wearable housing design allows for the use of any 18mm watch band.</i></p>

<div style="padding-top:8px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/wearablediagram.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
</div>

<p style="text-align:center"><i>Circuit Schematic - The wearable device uses an Atmega 328 microprocessor connected to the RF module with the SPI interface.  Power is regulated from the battery to 3V.  The battery on board charging circuitry allows the battery to be charged through the USB connection.</i></p>

<div style="padding-top:8px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/cse477wearable-1.jpg" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
</div>

<p style="text-align:center"><i>Assembled PCB for Wearable Module</i></p>

#### Energy Regulator
The regulator will initially be a Bluetooth-controlled outlet that plugs into an existing home outlet.  By communicating with the desktop application through Bluetooth connection, this Bluetooth-controlled outlet will regulate the flow of electricity from the outlet to the electronic to be controlled. For our demo, we will be using a lamp/light source plugged into this outlet.

#### The D.R.E.W. System Tool 
The central control application will serve two main purposes: provide a graphical interface that allows users to set system configurations, and run back end logic that controls the hardware. After loading any previously saved configurations, the D.R.E.W. System Tool start background processes and show the GUI to the user. The user can monitor the state of the system, as well as make changes to the current configuration. These configs will be saved when exiting the program. The logic that drives the system can be broken down into two main parts: the <b>Serial Reader</b>, and the <b>Bluetooth Controller</b>. Here was the preliminary <a href="https://github.com/danhipke/danhipke.github.io/raw/master/images/storyboard.pdf" target="_blank">UI storyboard</a>.

<b>Serial Reader:</b>
The Serial Reader is responsible for the initial reading and processing of messages from the hardware. It is connected over serial to the USB module, and constantly reads any messages that the USB module receives. It then proceeds to do some initial processing, such as ignoring unknown hardware. It then attempts to determine if the system state has changed. If any actions need to be taken, it puts a work item into a queue that tells the bluetooth controller which actions to take.

<div style="padding-top:20px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/serial_reader.png" style="width:800px;border:none;display:block;margin-left:auto;margin-right:auto">
</div>

<b>Bluetooth Controller:</b>
The bluetooth controller reads items from a work queue, each of which contains information regarding the relavent zone and entry/exit action. The controller then finds all controllable devices in the zone, and attempts to change their state the new state. It will attempt to connect to disconnected devices, but will only do so a few times to avoid hanging the system.

<div style="padding-top:20px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/bluetooth_controller.png" style="width:800px;border:none;display:block;margin-left:auto;margin-right:auto">  
</div>

***

### Putting It All Together
<div style="padding-top:8px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/block_diagram.jpg" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
</div>
<ol>
<li>The wearable periodically (once a second) broadcasts a signal containing its unique werable ID to all zone modules in range.</li>
</br>
<li>When a zone module receives a signal from a wearable, it then relays a message to the central system containing its unique zone ID as well as the ID of the wearable that sent the initial signal and a measure of the strength of that signal.</li>
</br>
<li>Based on messages from the zone modules, the central system determines whether any wearables have entered or exited any zones. If any such changes have occurred, the central system will determine what commands need to be sent to the connected Bluetooth devices. The threshold of zones, which Bluetooth devices are associated with each zone, and what actions those device should take on zone entry/exit are all defined by the user using the D.R.E.W. System Tool software.</li>
</ol>

<div style="padding-top:20px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/exc.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
</div>

### Project Extensions
If we accomplish our goals listed above before the project deadline is reached, we will attempt to implement one or a few of the following goals:
* daisy-chaining the zone modules with the USB dongle to allow for messages to be sent from the wearable when it can't directly contact the USB dongle
* visual location tracking throughout your house
* communication with RFID tags and the RFM12B transceivers 

***

## Bill of Materials

<div style="padding-top:20px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/CostAnalysis.PNG" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
</div>
<!--
<table border="1" cellpadding="5" style="width=100%">
  <tr style="text-align:center">
    <td><b>Quantity</b></td>
    <td><b>Item</b></td>
    <td><b>Price</b></td>
  </tr>
  <tr>
    <td>7</td>
    <td><a href="http://moderndevice.com/product/rfm12b-radio">RFM12B Radio Transceiver</a></td>
    <td>$6.67</td>
  </tr>
  <tr>
    <td>5</td>
    <td><a href="https://www.sparkfun.com/products/9261">ATMega328 - TQFP</a></td>
    <td>$3.43</td>
  </tr>
  <tr>
    <td>1</td>
    <td><a href="http://www.amazon.com/Plugable-Controlled-Automation-Open-Source-Applications/dp/B00PG50OSM">Plugable Bluetooth-Controlled AC Power Switch</a></td>
    <td>$35.00</td>
  </tr>
  <tr>
    <td>2</td>
    <td><a href="https://www.adafruit.com/products/1317">Lithium Ion Polymer Battery - 3.7v 150mAh</a></td>
    <td>$5.95</td>
  </tr>
  <tr>
    <td>1</td>
    <td><a href="https://www.adafruit.com/products/1905">Adafruit Mini Lipo w/Mini-B USB Jack - USB LiIon/LiPoly charger - v1</a></td>
    <td>$6.95</td>
  </tr>
  <tr>
    <td>2</td>
    <td><a href="http://store.arduino.cc/product/A000059">USB 2 Serial Converter (USB Mini)</a></td>
    <td>$10.58</td>
  </tr>
  <tr>
    <td>3</td>
    <td><a href="http://en.wikipedia.org/wiki/Printed_circuit_board">Wearable PCB</a></td>
    <td>$5.00</td>
  </tr>
  <tr>
    <td>3</td>
    <td><a href="http://en.wikipedia.org/wiki/Printed_circuit_board">Zone Module PCB</a></td>
    <td>$5.00</td>
  </tr>
  <tr>
    <td></td>
    <td><a href="http://www.envplastics.com/sites/www.envplastics.com/files/styles/product_image/public/pcb_enclosure_uu_plastic_housing_black_1.jpg?itok=wl9KPsqr">3D Printed Plastic Enclosure</a></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>TOTAL (so far)</td>
    <td>$188.40</td>
  </tr>
</table>
-->	
***

## Project Schedule
<table border="1" cellpadding="5" style="width=100%">
  <tr style="text-align:center">
    <td><b>Week Of</b></td>
    <td><b>Tasks</b></td>
  </tr>
  <tr>
    <td>04/12</td>
    <td>
      <ul>
        <li>order components</li>
        <li>start experimenting with components (when they arrive)</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>04/19</td>
    <td>
      <ul>
        <li>implement/test basic communication between: central system & outlet switch, 
        central system & wearable, wearable & zone modules</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>04/26</td>
    <td>
      <ul>
        <li>flesh out communication protocol</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>05/03</td>
    <td>
      <ul>
        <li>start working on configuration software (i.e. the program running on central system)</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>05/10</td>
    <td>
      <ul>
        <li>[contingency time]</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>05/17</td>
    <td>
      <ul>
        <li>[contingency time]</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>05/24</td>
    <td>
      <ul>
        <li>finalize configuration software</li>
        <li>draft/print casing</li>
        <li>work on project extensions if ahead of schedule</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>05/31</td>
    <td>
      <ul>
        <li>polish everything</li>
        <li>prep for demo</li>
      </ul>
    </td>
  </tr>
</table>

## Journal

Here is a list of our weekly journals so far:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>




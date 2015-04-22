---
layout: page
title: CSE477 Hardware Capstone
tagline: D.R.E.W.
---
{% include JB/setup %}

## Project Proposal 
Home automation is a continuously growing field. As more and more home appliances and electronics are becoming "smart", it is important to minimize energy waste. Our product "D.R.E.W." is an attempt to solve this problem. We envision our product as a way to dramatically reduce energy waste by turning on and off various devices and electronics in your home based on your proximity to them.

### Product Details
Our product will utilize RF transceivers as a way to measure the relative proximity of users in their homes to central "zones". Specifically, users will be able to put these RF transceiver modules around their homes in rooms or other key locations in the house. The wearable device will be able to measure proximity to to these modules using relative signal strength. Through a computer application, the user will then be able to associate specific home electronics appliances with each zone.  

For demo purposes, we will be controlling an outlet connected to a lamp in a room with a single RF module for that zone.  When the user enters the room (is near the RF module), the outlet will be powered on and the lamp will turn on.  When the user leaves the room, the outlet will be powered off and the lamp with it.

#### The Zone Modules
The zone modules will be RF transceivers connected to an ATMega328 chip and battery. These modules will be placed centrally in a room to allow for an easy calculation of the boundaries of the room.  These zone modules will be sending out an RF signal at 915 MHz.  The frequency and strength of the signal is high enough to accommodate large room sizes. The wearable will communicate with these modules to detect when a user has entered a specific zone.

We original envisioned these zone modules being passive or active RFID tags, but due to the high price of an ultra-high frequency RFID reader/writer, we were not able to meet the project budget using the RFID approach. 

#### The Wearable
The wearable will be a bracelet with an RF transceiver, ATMega328 chip and battery similar to the zone modules. The bracelet will use the signal strength from the zone modules to measure proximity. A higher signal strength means the user is closer to the zone module and as a result, closer to the zone. A lower signal strength means the user is far away from the zone. The amount of signal strength required for a user to be "in" a zone will be configurable through the desktop application to accommodate varying room sizes.  The only purpose of the wearable is as a way to track the user's position and communicate it back to the desktop application/central module.

<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/case.jpg" style="width:300px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">  
Preliminary wearable housing design.

#### Energy Regulator
The regulator will initially be a Bluetooth-controlled outlet that plugs into an existing home outlet.  By communicating with the desktop application through Bluetooth connection, this Bluetooth-controlled outlet will regulate the flow of electricity from the outlet to the electronic to be controlled. For our demo, we will be using a lamp/light source plugged into this outlet.

#### The Central Control Application 
The application will be used to control the actual home electronics and appliances. It will communicate with the energy regulator and wearable. When the wearable sends a signal that the user has left/entered a room, the application will send a signal to all energy regulators in the room to turn on/shut off all regulated electronics appropriately. This application will also let users configure which zone modules and energy regulators correspond to which rooms. If time allows, the application will connect to IFTTT and be able to be used in IFTTT recepies. At a high level, this process can be broken down into three main phases: <b>Receive</b>, <b>Process</b>, and <b>Send</b>.

<b>Receive:</b>
When in this stage, the central hub is waiting for a signal from a wearable device.  Using a transceiver (RF or Bluetooth) as the input device, it waits until a properly formatted signal is sent from the wearable to the computer.  This signal will contain information about the wearable (device ID, location, etc).  Upon receiving this signal, the program moves to processing stage.
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/Receive_Flowchart.png" style="width:600px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">  


<b>Process:</b>
The processing stage is concerned with translating the signal received into an action to be performed.  Using the unique ID of the wearable, the central control unit will lookup user defined preferences, and create a list of possible actions to take.  Then based on the location (or possibly changes in location) one of these actions will be selected.  For example if the processing stage receives an ID of "1", and a location of "Hallway" then it might choose an action of "turn hallway lights on".
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/Process_Flowchart.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">  


<b>Send:</b>
This is the final stage of the program.  After a signal is received and processed, the central control unit now has an action to take.  This action will be converted into an output signal (RF or Bluetooth), and sent to the device it wishes to control.  This stage of the program is concerned with transforming "actions" into signals, and ensuring these signals are sent correctly.  After sending this signal it will move to the Receive stage, and wait for another incoming signal.
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/Send_Flowchart.png" style="width:500px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">  

***

### Putting It All Together
<div style="padding-top:8px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/block_diagram.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
</div>
<ol>
<li>The wearable device periodically sends out discovery signals to determine if any zone modules are in range. If a zone module receives such a signal, it sends back to the wearble an acknowledgement signal containing its unique identifier.</li>
</br>
<li>When the wearable receives an acknowledgement signal from a zone module, it sends a message to the central system which contains the unique identifier of the acknowledging zone module as well as the strength of the signal received by the wearable. The central system uses this information to determine the relative location of the device-wearing user. (Note: For the current development phase, the central system is a general purpose computer with RF and Bluetooth transceivers.)</li>
</br>
<li>By checking the user's current location against the user-defined software settings, the central system determines whether messages must be sent to any electronics to manipulate their energy usage. (Note: For the current development phase, we will be using Bluetooth-controlled power outlet switches which will allow the central system to power on/off simple electronics, such as lamps or TVs.)</li>
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
<table border="1" cellpadding="5" style="width=100%">
  <tr style="text-align:center">
    <td><b>Quantity</b></td>
    <td><b>Item</b></td>
    <td><b>Price</b></td>
  </tr>
  <tr>
    <td>8</td>
    <td><a href="http://moderndevice.com/product/rfm12b-radio">RFM12B Radio Transceiver</a></td>
    <td>$6.67</td>
  </tr>
  <tr>
    <td>8</td>
    <td><a href="https://www.sparkfun.com/products/9261">ATMega328 - TQFP</a></td>
    <td>$4.25</td>
  </tr>
  <tr>
    <td>1</td>
    <td><a href="http://www.amazon.com/Plugable-Controlled-Automation-Open-Source-Applications/dp/B00PG50OSM">Plugable Bluetooth-Controlled AC Power Switch</a></td>
    <td>$35.00</td>
  </tr>
  <tr>
    <td>2</td>
    <td><a href="http://www.ebay.com/itm/Lithium-Ion-Polymer-3-7v-Rechargeable-Battery-150mAh-Electronic-Projects-Arduino-/171267166692?pt=LH_DefaultDomain_0&hash=item27e05191e4">Lithium Ion Polymer 3.7v Rechargeable Battery 150mAh*</a></td>
    <td>$5.95</td>
  </tr>
  <tr>
    <td>2</td>
    <td><a href="http://www.ebay.com/itm/5V-Mini-USB-1A-Lithium-Battery-Charging-Lipo-Charger-Module-for-Arduino-A866-/131304520047?pt=LH_DefaultDomain_0&hash=item1e925bf96f">5V Mini USB 1A Lithium Battery Charger</a></td>
    <td>$1.49</td>
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
\*The ATMega328 uses ~3.6 mA of current, while the RF module uses about ~25 mA when transmitting and ~0.6 µA when on standby. We estimate that about 5% of the time, the RF module will be transmitting. Therefore, the whole wearable will draw about 4.85 mA of current, requiring 24 hours \* 4.85 mA = 116.4 mAh of charge to last a full day
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




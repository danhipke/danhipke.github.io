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
<div style="padding-top:8px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/block_diagram.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
</div>
<ol>
<li>The wearable device periodically sends out discovery signals to determine if any tags are in range. If a tag receives such a signal, it sends back to the wearble an acknowledgement signal containing its unique identifier.</li>
</br>
<li>When the wearable receives an acknowledgement signal from a tag, it sends a message to the central system which contains the unique identifier of the acknowledging tag as well as the strength of the signal received by the wearable. The central system uses this information to determine the relative location of the device-wearing user. (Note: For the current development phase, the central system is a general purpose computer with RF and Bluetooth transceivers.)</li>
</br>
<li>By checking the user's current location against the user-defined software settings, the central system determines whether messages must be sent to any electronics to manipulate their energy usage. (Note: For the current development phase, we will be using Bluetooth-controlled power outlet switches which will allow the central system to power on/off simple electronics, such as lamps or TVs.)</li>
</ol>

<div style="padding-top:20px;padding-bottom:12px">
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/exc.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">
</div>


## Bill of Materials
<table border="1" style="width:100%;text-align:center">
  <tr>
    <td>Quantity</td>
    <td>Item</td>
    <td>Price</td>
  </tr>
  <tr>
    <td>8</td>
    <td><a href="http://moderndevice.com/product/rfm12b-radio">RFM12B Radio Transceiver</a></td>
    <td>$6.67</td>
  </tr>
  <tr>
    <td>8</td>
    <td><a href="https://www.sparkfun.com/products/9061">ATMega328P</a></td>
    <td>$4.30</td>
  </tr>
  <tr>
    <td>1</td>
    <td><a href="http://www.amazon.com/Plugable-Controlled-Automation-Open-Source-Applications/dp/B00PG50OSM">Plugable Bluetooth-Controlled AC Power Switch</a></td>
    <td>$35.00</td>
  </tr>
  <tr>
    <td></td>
    <td><a href="http://en.wikipedia.org/wiki/Battery_%28electricity%29">batteries</a></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td><a href="http://en.wikipedia.org/wiki/Printed_circuit_board">PCB</a></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td><a href="http://www.envplastics.com/sites/www.envplastics.com/files/styles/product_image/public/pcb_enclosure_uu_plastic_housing_black_1.jpg?itok=wl9KPsqr">plastic enclosure</a></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td>TOTAL (so far)</td>
    <td>$122.76</td>
  </tr>
</table>

## Journal

Here is a list of our weekly journals so far:

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>




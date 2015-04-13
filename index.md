---
layout: page
title: CSE477 Hardware Capstone
tagline: D.R.E.W.
---
{% include JB/setup %}

## Project Proposal 
Home automation is a continuously growing field. As more and more home appliances and electronics are becoming "smart", it is important to minimize energy waste. Our product "D.R.E.W." is an attempt to solve this problem. We envision our product as a way to turn on and off various devices and electronics in your home based on how close you are to them.

### Product Details
Our product will utilize RF modules as a way to track the proximity of users in their homes. Specifically, users will be able to put the RF modules around their house in rooms or other key locations in the house. The wearable device will be able to measure proximity to to these tags and place the user in a specific zone. The user will then be able to configure specific rules for each zone.  For example, you could have all of the lights turn on when you enter the zone, and turn off whne you leave.  

#### The Tags
The tags will be RF modules requiring battery power. These tags will be placed centrally in a room to allow for the most accurate zones.

#### The Wearable
The wearable will be a bracelet with an RF module similar to the tags. The bracelet will use the signal strength from the active RFID tags to measure proximity. A higher signal strength means the user is closer to the tag and as a result, closer to the room. A lower signal strength means the user is far away from the tag/room.

#### Energy Regulator
The regulator will initially be a device that plugs into an existing home outlet and acts as an outlet for any electronic. It will control whether or not the device is turned on by regulating the flow of electricity from the outlet to the electronic to be controlled. This will be a bluetooth/wireless device that can be controlled through some external signal.

#### The Central Control Application 
The application will be used to control the actual home electronics and appliances. It will communicate with the energy regulator and RF modules distributed throughout the house. When the RF module sends a signal that the user has left/entered a room, the application will send a signal to all energy regulators in the room to turn on/shut off all regulated electronics appropriately. This application will also let users configure which tags and energy regulators correspond to which rooms. If time allows, the application will connect to IFTTT and be able to be used in IFTTT recepies. At a high level, this process can be broken down into three main phases: <b>Receive</b>, <b>Process</b>, and <b>Send</b>.

#### Receive
When in this stage, the central hub is waiting for a signal from a wearable device.  Using a transceiver (RF or Bluetooth) as the input device, it waits until a properly formatted signal is sent from the wearable to the computer.  This signal will contain information about the wearable (device ID, location, etc).  Upon receiving this signal, the program moves to processing stage.
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/Receive_Flowchart.png" style="width:600px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">

#### Process
The processing stage is concerned with translating the signal received into an action to be performed.  Using the unique ID of the wearable, the central control unit will lookup user defined preferences, and create a list of possible actions to take.  Then based on the location (or possibly changes in location) one of these actions will be selected.  For example if the processing stage receives an ID of "1", and a location of "Hallway" then it might choose an action of "turn hallway lights on".
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/Process_Flowchart.png" style="width:800px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">

#### Send
This is the final stage of the program.  After a signal is received and processed, the central control unit now has an action to take.  This action will be converted into an output signal (RF or Bluetooth), and sent to the device it wishes to control.  This stage of the program is concerned with transforming "actions" into signals, and ensuring these signals are sent correctly.  After sending this signal it will move to the Receive stage, and wait for another incoming signal.
<img src="https://github.com/danhipke/danhipke.github.io/raw/master/images/Send_Flowchart.png" style="width:500px;border:2px solid black;display:block;margin-left:auto;margin-right:auto">


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
    <td><a href="http://en.wikipedia.org/wiki/Battery_%28electricity%29">Batteries</a></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td><a href="http://en.wikipedia.org/wiki/Printed_circuit_board">PCB</a></td>
    <td></td>
  </tr>
  <tr>
    <td></td>
    <td><a href="http://www.envplastics.com/sites/www.envplastics.com/files/styles/product_image/public/pcb_enclosure_uu_plastic_housing_black_1.jpg?itok=wl9KPsqr">3D Printed Plastic Enclosure</a></td>
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




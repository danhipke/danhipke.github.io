---
layout: post
title: "Week 2 Journal"
description: ""
category: 
tags: []
---
{% include JB/setup %}

This week, we focused on refining our design largely based on the availability of materials and budget of the project.  We met as a group on Sunday to refine our product design and come up with a doable implemntation of our idea for proximity-controlled energy regulation.  Throughout the days leading up to our meeting, Ben and Wes researched possible hardware to use for accomplishing our goal.  Teddy worked on a block diagram to better visual how our product will work while Daniel worked on brainstorming application ideas while also revising the website to make it easier to maintain.

#### Reworking Our Idea
In our Sunday meeting, we spent the first hour or two browsing the web and looking at hardware we could use to create our product.  This meant going through the list that Ben and Wes created as a group to determine which hardware we liked and what we didn't like.  Unfortunately, we discovered that it would be near impossible to use RFID tags and an RFID reader/writer to accomplish our goal.  An ultra-high frequency reader/writer that was small enough to fit in a wearable was around $1000 to $2000, and anything less than that did not meet the range requirements (being able to read at a distance equal to the width of a doorway at least).

With RFID out of the picture, we moved our focus to RF transceivers.  After some debate, we decided to go with 915 MHz RF transceivers for both the wearable and zone/room detection modules.  They are cheap at around $7 a piece and very small, coming in at around the size of a quarter.  Specifically, we went with an <a href="http://moderndevice.com/product/rfm12b-radio/">RFM12B Radio</a>, which can transmit/receive a signal while also measuring signal strength.  To control these modules, we went with the ATMega328 chip, since it is easy to work with and very small.  Both these pieces of technology will live inside the wearable and the zone modules.

We also decided to move away from a phone application for configuring the zone modules and wearable.  By going with a desktop application, we figured it would be easier to create a wireless USB dongle to communicate with our wearable.  The USB dongle for the desktop application will be almost identical to the zone modules, although have the ability to send information to the computer over a serial connection.  The desktop application will then use bluetooth to control our Bluetooth-controlled outlet.

To see our project plan and BOM, <a href="http://danhipke.github.io/hardware-capstone">go here</a>

Outside of solidifying our project plan, we have some minor updates as well.

#### Updated Website
We updated our website to use Jekyll for ease of adding pages and blog posts and moved it from http://danhipke.github.io/hardware-capstone to http://danhipke.github.io/.  This framework also supports a mixture of markdown and HTML, making it very easy to work with.  Our previous site was built using a straight HTML with no organizational logic, making it hard to add add journals and pages.  By using Jekyll which integrates quite well with GitHub, we will be drastically reducing the time spent mainaining and formatting our site. 

#### Updated Product Name
We also updated our product name.  It is now called D.R.E.W.  This stands for

**D**rastically<br/>
**R**educe<br/>
**E**nergy<br/>
**W**aste<br/>

The name F.R.E.D. was just a random assortment of letters with no meaning, so at least now we have an acronym we can come up with words for.

#### Final Thoughts
We were a bit worried as to why we weren't just using Bluetooth and a phone for this now that we weren't using RFID, but our reasoning is that it's more convenient to have a wearable.  Since not all people have Bluetooth in their phones or carry their phone around the house, this is a more universal solution and won't get in the way or cause issues if you don't have your phone with you.

Now that we have our hardware picked out, this project definitely feels a lot more doable. It's unfortunate that we weren't able to find a cost-effective solution using RFID tags, since they are fairly cheap and very small in some cases.  However, our modules and wearable will be just as small using a more standard RF transceiver.

This week, we plan on ordering our parts so we can get started on building a protoype!



---
layout: post
status: publish
published: true
title: Bluetooth + GPS + Python + ActionScript - Part 2 - Hooking Up
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "<strong>Overview</strong>\r\n\r\nAfter having built the hardware in
  Part 1, it is fairly useless without a way to get the GPS data from the device somewhere
  else in order to do something useful with it.&Acirc;&nbsp; For this project, the
  end result will be a visualization of the GPS data in Flash Player on a Mac.&Acirc;&nbsp;
  There are myriad ways to accomplish this, however very few approaches can easily
  encapsulate all of these steps in a single language.&Acirc;&nbsp; This is because
  both low-level system access (to read the serial data) and some sort of server (to
  serve the data to Flash Player) are required.&Acirc;&nbsp; While it is definitely
  possible to use any number of other languages such as Java, Processing, C++, etc.,
  performing all of these tasks with those languages would require significant amounts
  of code.\r\n\r\nWith that said, I opted for Python not only because I love it, but
  also because it is quite straightforward to use it to read from a serial port using
  the <a href=\"http://pyserial.wiki.sourceforge.net/pySerial\" target=\"_blank\">pyserial
  module</a> and also to establish any number of different types of servers including
  standard HTTP and socket servers.&Acirc;&nbsp; While there are built-in libraries
  for creating and managing servers, I ultimately decided on creating a socket server
  using <a href=\"http://twistedmatrix.com/trac/\" target=\"_blank\">Twisted</a>.&Acirc;&nbsp;
  Twisted is an enormously powerful networking framework that simplifies the creation
  of all sorts of servers.\r\n\r\nWhy add another framework when a standard HTTP server
  would suffice for serving up data to the Flash Player?&Acirc;&nbsp; The implementation
  of a standard HTTP server would require Flash Player polling the service to determine
  if data had been updated.&Acirc;&nbsp; So, rather than rely on that sub-par solution,
  Twisted makes the creation of socket servers very easy, which then allows the Flash
  Player to receive data in real-time via an XMLSocket connection.&Acirc;&nbsp; Not
  only that, but one of the coolest aspects of Twisted is that it makes it fairly
  easy to write multi-user socket servers, which will be a nice addition for future
  enhancements\r\n\r\nHere is what the overall system architecture ends up looking
  like when all of that is considered:\r\n\r\n<a href=\"http://phy5ics.com/blog/wp-content/uploads/2008/11/gps_bt_sys_arch.jpg\"><img
  class=\"alignnone size-full wp-image-62\" title=\"gps_bt_sys_arch\" src=\"http://phy5ics.com/blog/wp-content/uploads/2008/11/gps_bt_sys_arch.jpg\"
  /></a>\r\n\r\nHowever, before diving into these details, the first step
  is to hook up the device to the Mac via a serial Bluetooth connection and verifying
  that everything is working so far.\r\n\r\n"
wordpress_id: 58
wordpress_url: http://phy5ics.com/blog/?p=58
date: 2008-11-06 21:10:42.000000000 -05:00
categories:
- AS3
- GPS
- Physical Computing
- Bluetooth
- Python
- Twisted
tags:
- Python
comments:
- id: 3945
  author: john
  author_email: abc@hotmail.com
  author_url: http://Website
  date: !binary |-
    MjAwOS0wMy0xMiAwODozMzozOSAtMDQwMA==
  date_gmt: !binary |-
    MjAwOS0wMy0xMiAxNjozMzozOSAtMDQwMA==
  content: Great site for GPS!!!
- id: 3946
  author: varboreaxia
  author_email: enelsbiossign@gmail.com
  author_url: http://Website
  date: !binary |-
    MjAwOS0wMy0xMiAwODo0MjowNSAtMDQwMA==
  date_gmt: !binary |-
    MjAwOS0wMy0xMiAxNjo0MjowNSAtMDQwMA==
  content: Thank you!
- id: 3947
  author: grhabyt
  author_email: gwyan.rhabyt@csueastbay.edu
  author_url: http://Website
  date: !binary |-
    MjAwOS0wMy0xNCAxMToxMDoxNyAtMDQwMA==
  date_gmt: !binary |-
    MjAwOS0wMy0xNCAxOToxMDoxNyAtMDQwMA==
  content: ! "I'm waiting eagerly to see the Twisted and Flash portions of the system.
    Please post when you can.\r\nThanks"
- id: 3965
  author: Adam
  author_email: cl.adamwang@gmail.com
  author_url: http://east3yrswest3yrs.blogspot.com/
  date: !binary |-
    MjAwOS0xMS0xMiAwOTowMTo1NCAtMDUwMA==
  date_gmt: !binary |-
    MjAwOS0xMS0xMiAxNzowMTo1NCAtMDUwMA==
  content: I found you have been introduced roughly contents about using ActionScript
    proposed to control wireless device, it's a great idea for someone who may have
    his or her ideas to have fun. I just want to say that it's good artical. Thanks.
---
<strong>Overview</strong>

After having built the hardware in Part 1, it is fairly useless without a way to get the GPS data from the device somewhere else in order to do something useful with it.&Acirc;&nbsp; For this project, the end result will be a visualization of the GPS data in Flash Player on a Mac.&Acirc;&nbsp; There are myriad ways to accomplish this, however very few approaches can easily encapsulate all of these steps in a single language.&Acirc;&nbsp; This is because both low-level system access (to read the serial data) and some sort of server (to serve the data to Flash Player) are required.&Acirc;&nbsp; While it is definitely possible to use any number of other languages such as Java, Processing, C++, etc., performing all of these tasks with those languages would require significant amounts of code.

With that said, I opted for Python not only because I love it, but also because it is quite straightforward to use it to read from a serial port using the <a href="http://pyserial.wiki.sourceforge.net/pySerial" target="_blank">pyserial module</a> and also to establish any number of different types of servers including standard HTTP and socket servers.&Acirc;&nbsp; While there are built-in libraries for creating and managing servers, I ultimately decided on creating a socket server using <a href="http://twistedmatrix.com/trac/" target="_blank">Twisted</a>.&Acirc;&nbsp; Twisted is an enormously powerful networking framework that simplifies the creation of all sorts of servers.

Why add another framework when a standard HTTP server would suffice for serving up data to the Flash Player?&Acirc;&nbsp; The implementation of a standard HTTP server would require Flash Player polling the service to determine if data had been updated.&Acirc;&nbsp; So, rather than rely on that sub-par solution, Twisted makes the creation of socket servers very easy, which then allows the Flash Player to receive data in real-time via an XMLSocket connection.&Acirc;&nbsp; Not only that, but one of the coolest aspects of Twisted is that it makes it fairly easy to write multi-user socket servers, which will be a nice addition for future enhancements

Here is what the overall system architecture ends up looking like when all of that is considered:

<a href="http://phy5ics.com/blog/wp-content/uploads/2008/11/gps_bt_sys_arch.jpg"><img class="alignnone size-full wp-image-62" title="gps_bt_sys_arch" src="http://phy5ics.com/blog/wp-content/uploads/2008/11/gps_bt_sys_arch.jpg" /></a>

However, before diving into these details, the first step is to hook up the device to the Mac via a serial Bluetooth connection and verifying that everything is working so far.

<a id="more"></a><a id="more-58"></a>

<strong>Bluetooth Pairing</strong>
Obviously, the first step is to power up the board.&Acirc;&nbsp; After that, pairing the BlueSMiRF with the Mac.&Acirc;&nbsp; This is a very straightforward process.&Acirc;&nbsp; From the Bluetooth preference pane in System Preferences, click the "+" icon to add a new Bluetooth device.&Acirc;&nbsp; Advance through the dialog boxes, configuring the device that shows up as <strong><em>SparkFun-BT</em></strong>.&Acirc;&nbsp; The passkey for BlueSMiRF module is <strong><em>default</em></strong>, so type that in when prompted.

<a href="http://phy5ics.com/blog/wp-content/uploads/2008/11/bt_pairing.jpg"><img class="alignnone size-full wp-image-59" title="bt_pairing" src="http://phy5ics.com/blog/wp-content/uploads/2008/11/bt_pairing.jpg" /></a>
Once that's been done, by checking the serial interfaces in <strong><em>/dev</em></strong>, it can be verified that it is now active as a serial device.&Acirc;&nbsp; That is done by opening a terminal window and typing <strong><em>ls /dev/tty.*</em></strong>.&Acirc;&nbsp; That will list out all available serial interfaces.&Acirc;&nbsp; The BlueSMiRF should show up as something like <strong><em>tty.SparkFun-BT-COM0-1</em></strong>.

<a href="http://phy5ics.com/blog/wp-content/uploads/2008/11/ls_tty.jpg"><img class="alignnone size-full wp-image-60" title="ls_tty" src="http://phy5ics.com/blog/wp-content/uploads/2008/11/ls_tty.jpg" /></a>

<strong></strong>

<strong>Screen</strong>
Screen is a Unix application that allows one to attach a terminal session to a particular process.&Acirc;&nbsp; To view the serial communication that is happening on the serial port that the BlueSMiRF is attached to, this is a good option.&Acirc;&nbsp; This can be done by typing the following command into the terminal to view the serial communication on that port in realtime:

<strong><em>screen /dev/tty.SparkFun-BT-COM0-1 9600</em></strong>

Note that the <strong><em>9600</em></strong> at the end of that command is the baud rate.&Acirc;&nbsp; That command should yield some cryptic messages being printed in Terminal like the following if everything else is wired up properly:

<a href="http://phy5ics.com/blog/wp-content/uploads/2008/11/nmea.jpg"><img class="alignnone size-full wp-image-61" title="nmea" src="http://phy5ics.com/blog/wp-content/uploads/2008/11/nmea.jpg" /></a>

To exit screen, hit <strong><em>control-a</em></strong>, then <strong><em>control-\</em></strong>.

The strings that are seen here are NMEA strings, which are derived from a specification that standardizes the way that marine electronics communicate with each other.&Acirc;&nbsp; For additional information on this, check out <a href="http://www.gpsinformation.org/dale/nmea.htm">http://www.gpsinformation.org/dale/nmea.htm</a>.&Acirc;&nbsp; If the GPS has a location fix, then numerous lines beginning with $GPGGA will be displayed, which precedes messages that contain the location fix data.&Acirc;&nbsp; Otherwise, there will be mostly $GPGSV, which represents data regarding the GPS satellites themselves.

<strong>OK, Now What?</strong>

Now that there is data coming in over a virtual serial port, the next step is writing the software.&Acirc;&nbsp; The next article in this series will examine the Twisted socket server and Flash XMLSocket connection along with providing the source code for those systems.

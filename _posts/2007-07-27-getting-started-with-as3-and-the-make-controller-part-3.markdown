---
layout: post
status: publish
published: true
title: Getting Started with AS3 and the Make Controller - Part 3
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "Please be sure to read <a href=\"http://phy5ics.com/blog/2007/07/27/getting-started-with-as3-and-the-make-controller-part-2/\">Part
  2</a>, and download the classes from that example otherwise the following example
  will not work as expected.\r\n\r\nThis article will cover how to read OSC messages
  that are sent from the Make Controller into FLOSC and then into Flash using the
  modified FWiidom classes.  Before getting started, this is where I have to point
  out that the manner in which the Flash Player receives the XML converted from OSC
  is by polling FLOSC, which is far from ideal. Polling is an inefficient and wasteful
  way of checking to see if any state has changed on the controller. This, however,
  is the way that OSC works - by querying the connected device to determine if the
  state of any inputs has changed. I'm not sure if this characteristic applies to
  the Make Controller in general, if for example, using other protocols over USB,
  but I have a feeling that it doesn't. I'll have to look at some of the code written
  for the controller in other languages and also read up on OSC to determine if this
  is the case. In any case, we're stuck with polling in ActionScript.\r\n\r\n"
wordpress_id: 11
wordpress_url: http://phy5ics.com/blog/2007/07/27/getting-started-with-as3-and-the-make-controller-part-3/
date: 2007-07-27 13:33:58.000000000 -04:00
categories:
- AS3
- Make Controller
tags: []
comments: []
---
Please be sure to read <a href="http://phy5ics.com/blog/2007/07/27/getting-started-with-as3-and-the-make-controller-part-2/">Part 2</a>, and download the classes from that example otherwise the following example will not work as expected.

This article will cover how to read OSC messages that are sent from the Make Controller into FLOSC and then into Flash using the modified FWiidom classes.  Before getting started, this is where I have to point out that the manner in which the Flash Player receives the XML converted from OSC is by polling FLOSC, which is far from ideal. Polling is an inefficient and wasteful way of checking to see if any state has changed on the controller. This, however, is the way that OSC works - by querying the connected device to determine if the state of any inputs has changed. I'm not sure if this characteristic applies to the Make Controller in general, if for example, using other protocols over USB, but I have a feeling that it doesn't. I'll have to look at some of the code written for the controller in other languages and also read up on OSC to determine if this is the case. In any case, we're stuck with polling in ActionScript.

<a id="more"></a><a id="more-11"></a>

That being said, the goal of this article is to illustrate using a Timer object for sending OSC messages from the Make Controller now that we've hacked the FWiidom classes and can connect to and receive data from the Make Controller's analog inputs. We'll start with connecting a slide potentiometer to analogin4 (any other analog input is fine, just change the code if you connect it to another input) like so:

[You'll have to use your imagination until I stop slacking and take a photo]

This might also be a good time to mention that these same techniques can be applied to any sensor that is connected to the analog ins.

Now that the sensor is connected, time to code.  We'll be reusing some of the code from <a href="http://phy5ics.com/blog/2007/07/22/getting-started-with-as3-and-the-make-controller-part-1/">Part 1</a>, so starting with the constructor from that class, a new event listener needs to be added to the OSCConnection object in order to listen for incoming packets from FLOSC because the code in Part 1 was only concerned with sending packets:
<pre lang="actionscript">
oscConn.addEventListener(OSCConnectionEvent.ON_PACKET_IN, onPacketIn);</pre>
<pre lang="actionscript"></pre>
Also, so that the output of OSC can be examined for debugging purposes, another event listener can be added as well:
<pre lang="actionscript">
oscConn.addEventListener(OSCConnectionEvent.ON_PACKET_OUT, onPacketOut);</pre>
<pre lang="actionscript"></pre>
Now that the listeners have been added, the handler functions need to be fleshed out.  To start with, we'll just trace the input and output to the FLOSC server in the following functions:
<pre lang="actionscript">
private function onPacketIn(evtOSC:OSCConnectionEvent):void {
trace(this + ": onPacketIn: " + evtOSC.data.name + " " + evtOSC.data.data);
}

private function onPacketOut(evtOSC:OSCConnectionEvent):void {
trace(this + ": onPacketOut: " + evtOSC.data.name + " " + evtOSC.data.data);
}</pre>
<pre lang="actionscript"></pre>
To dissect this a bit and see what's really going here, we'll have to follow the OSCConnectionEvent object that is passed into the function.  Looking at the OSCConnectionEvent class (org.fwiidom.osc.OSCConnectionEvent), it's very straightforward and contains nothing but static variables that define the events and a data variable.  The data variable is the one that is most interesting.  The data variable, while typed as a generic object, is actually an OSCPacket object that is created by the parseXml() function in the OSCConnection class when an OSC message is received from FLOSC.  As a result, the data variable contains all of the information associated with the OSC message, as illustrated by evtOSC.data.name and evtOSC.data.data.

After that little detour, what we're going to do is to monitor the input of the slide potentiometer on a timed basis, so rather than sending an OSC packet with an MouseEvent.CLICK event as Part 1 did, we'll hook it up to a Timer object that will start when a button is clicked.  The code to do that is really pretty simple:
<pre lang="actionscript">
private function onTimerStartClick(evtClick:MouseEvent):void {
timerStart();
}

private function timerStart():void {
if (!tmrTimer) {
tmrTimer = new Timer(250, 0);
tmrTimer.addEventListener("timer", onTimerIncrement);
}
tmrTimer.start();
}

private function timerStop():void {
tmrTimer.reset();
}

private function onTimerIncrement(evtTimer:TimerEvent):void {
oscConn.sendOSCPacket(new OSCPacket("/analogin/4/value", [""], STR_REMOTE_IP, NUM_PORT));
}</pre>
<pre lang="actionscript"></pre>
The important thing to look at here is the last function: onTimerIncrement.  This is the function that is called by every timer event.  To poll for the value of the potentiometer, or any other analog input, an OSC address is sent without an associated value, which in this case is /analogin/4/value.  The Make Controller then responds with a packet that contains that same OSC address with an associated value corresponding to the position of the slider on the  potentiometer.

If your project doesn't need to monitor the inputs frequently, for efficiency, you can limit the polling to individual OSC packets by sending them according to other events such from user input such as MouseEvent.CLICK or other events fired off within your application.

In Part 4, I'll show some practical examples to get started now that we're able to send and receive OSC packets.

<a href="http://phy5ics.com/blog/wp-content/uploads/2007/07/makecontroller_as3_part3_examples2.zip" title="Download Make Controller AS3 Part 3 Example Files">Download Make Controller AS3 Part 3 Example Files</a>

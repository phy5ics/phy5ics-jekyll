---
layout: post
status: publish
published: true
title: Getting Started with AS3 and the Make Controller - Part 4
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "<strong>Doing Something \"Useful\" With Sensor Input </strong>\r\n\r\nIn
  Parts 1-3, we spent some time examining the basics of the Make Controller, OSC and
  how it works with (or in some cases doesn't work) ActionScript 3.   Now, we can
  start to do some things that might actually be construed as being useful for a project.
  \ To start, let's get the hardware set up by hooking up a light sensor to analogin0.
  \ With that done, we can write some code to use the input from the light sensor
  as it detects ambient light levels to control the opacity of a sprite on the stage
  of our SWF.\r\n\r\n"
wordpress_id: 20
wordpress_url: http://phy5ics.com/blog/2007/08/03/getting-started-with-as3-and-the-make-controller-part-4/
date: 2007-08-03 16:26:16.000000000 -04:00
categories:
- AS3
- Make Controller
tags: []
comments: []
---
<strong>Doing Something "Useful" With Sensor Input </strong>

In Parts 1-3, we spent some time examining the basics of the Make Controller, OSC and how it works with (or in some cases doesn't work) ActionScript 3.   Now, we can start to do some things that might actually be construed as being useful for a project.  To start, let's get the hardware set up by hooking up a light sensor to analogin0.  With that done, we can write some code to use the input from the light sensor as it detects ambient light levels to control the opacity of a sprite on the stage of our SWF.

<a id="more"></a><a id="more-20"></a>
In keeping with the grand tradition of laziness, ahem, I mean re-usable code, we'll start with the code from the last example, as that provides a decent framework to start with.  In the last example, the values passed along by OSC from the sensor were simply traced out to Flash's output console.  To do something useful with it, the key is to look at the incoming packets and parse out the ones that we need to pass on to other functions.  This can be done adding a switch statement in the onPacketIn event handler as follows:
<pre lang="actionscript">
private function onPacketIn(evtOSC:OSCConnectionEvent):void {
switch(evtOSC.data.name) {
case "/analogin/0/value":
changeBackgroundAlpha(evtOSC.data.data);
break;
}
}</pre>
<pre lang="actionscript"></pre>
Note: It is of course possible to use an else/if statement to accommodate this same functionality.  In general, I opt for case statements, as I know the explicit values that are to be expected in the switch.  This is also more efficient, as the AVM knows what values to look for and ignores the rest, whereas in an else/if statement, all values must be evaluated regardless of whether or not they are relevant to that piece of code.  That being said, to "listen" to another input, another case would be added that contains the address of the input being listened to and also a function to handle that input.

Here, as an OSCConnectionEvent object is passed into the function, we look for the name of a specific address on the application board (evtOSC.data.name) that sent the OSC packet.  When that address matches something that is needed by our application, we can then send the value of that input to a function that does something useful with it.  In this case, we'll pass the value sent by the light sensor to a function called changeBackgroundAlpha().  That function looks like:
<pre lang="actionscript">
private function changeBackgroundAlpha(intValue:int):void {
var nAlphaRatio:Number = (1 / 1024);
var nNewAlpha = nAlphaRatio * intValue;
this.getChildAt(0).alpha = nNewAlpha;
}</pre>
<pre lang="actionscript"></pre>
Take a look and notice that I'm setting up a ratio between the input value, which could be anywhere from 0-1023 and an alpha value, which can only be 0-100.  After that relationship is established with some simple math, we can set the value of our sprite on the stage to a new value that is directly proportional to the value determined by the sensor.

<a href="http://phy5ics.com/blog/wp-content/uploads/2007/08/makecontroller_as3_part4_examples_2.zip" title="Make Controller AS3 Part 4 Example Files">Make Controller AS3 Part 4 Example Files</a>

In the next article, we'll look at using ActionScript to mediate communication between sensors and an output devices that are attached to the Make Controller.

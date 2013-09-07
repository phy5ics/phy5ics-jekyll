---
layout: post
status: publish
published: true
title: Getting Started with AS3 and the Make Controller - Part 1
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "A couple months back I picked up a Make Controller from <a href=\"http://makingthings.com\"
  target=\"_blank\">Making Things</a> to do some experimentation with Flash Media
  Server and physical computing. I'm just now getting around to writing up my experiences
  about getting set up with the Make Controller. While the <a href=\"http://www.makingthings.com/resources/tutorials/flash/index_html/overview\"
  target=\"_blank\">tutorial on the Making Things site</a> was great for getting
  started using AS2 with their .mxp extension, it didn't offer up anything on how
  to get started with what I really wanted to do, which was a project that would benefit
  from the performance of AS3 and Flash Player 9, so I had to take matters into my
  own hands.\r\n\r\n"
wordpress_id: 10
wordpress_url: http://phy5ics.com/blog/2007/07/22/getting-started-with-as3-and-the-make-controller-part-1/
date: 2007-07-22 13:31:37.000000000 -04:00
categories:
- AS3
- Make Controller
tags: []
comments:
- id: 2
  author: Stephen
  author_email: sgarci@mac.com
  author_url: http://www.stephengarcia.com/blog
  date: !binary |-
    MjAwNy0wNy0yNiAwODowMjo0NyAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wNy0yNiAxNjowMjo0NyAtMDQwMA==
  content: Very nice! Have you thought of contributing this work to the Makingthings.com
    guys and getting an AS3 version of their API going?
- id: 3
  author: Barton
  author_email: jb@phy5ics.com
  author_url: http://phy5ics.com
  date: !binary |-
    MjAwNy0wNy0yNyAwODoyMToxMCAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wNy0yNyAxNjoyMToxMCAtMDQwMA==
  content: I just looked and Liam already added this to the Tutorials page on MakingThings.com.  As
    for working on an AS3 version of their API, I've actually already ported the MakingThings
    AS2 version over to AS3.  I'll be posting the source and an article on that as
    soon as I manage to finish it.
- id: 89
  author: hydrotik | flash/design/photography &raquo; Blog Archive &raquo;
    Making Things + AS3 - Part 1 and 2 LED Sound Visualizer
  author_email: ''
  author_url: http://blog.hydrotik.com/2007/09/04/making-things-as3-part-1-and-2-led-sound-visualizer/
  date: !binary |-
    MjAwNy0wOS0wNCAxODoyODoyNSAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0wNSAwMjoyODoyNSAtMDQwMA==
  content: ! '[...] and has gone through a few more trials and tribulations over this
    then myself. Check out his blog here. Make sure you go through all his posts first
    as there is a progression and you will have a good [...]'
- id: 97
  author: Donovan Adams
  author_email: donovan@hydrotik.com
  author_url: http://blog.hydrotik.com
  date: !binary |-
    MjAwNy0wOS0wNSAwOTo1MjoyMyAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0wNSAxNzo1MjoyMyAtMDQwMA==
  content: ! "Hi John! I added a couple examples based on your port.\r\nhttp://blog.hydrotik.com/2007/09/04/making-things-as3-part-1-and-2-led-sound-visualizer/\r\nhttp://blog.hydrotik.com/2007/09/04/making-things-as3-part-3-serial-lcd/"
- id: 3939
  author: stc
  author_email: stc@basilar.net
  author_url: http://binaura.net
  date: !binary |-
    MjAwOC0xMi0yOCAwMDo0OTozMCAtMDUwMA==
  date_gmt: !binary |-
    MjAwOC0xMi0yOCAwODo0OTozMCAtMDUwMA==
  content: ! "nice! thanks.\r\n\r\ni connected flash with pd on localhost. working
    well for me."
- id: 3943
  author: Using Flash for MIDI &laquo; boringBlog
  author_email: ''
  author_url: http://theboringblog.wordpress.com/2009/02/01/using-flash-for-midi/
  date: !binary |-
    MjAwOS0wMi0wMSAxMToyMTowMSAtMDUwMA==
  date_gmt: !binary |-
    MjAwOS0wMi0wMSAxOToyMTowMSAtMDUwMA==
  content: ! '[...] of what I have found regarding FLOsc has been using Flash to talk
    with MAKE&Acirc;&nbsp;boards. This turtorial&Acirc;&nbsp;over at phy5ics.com got
    me started. He was using the FWiidom FLOsc AS3 Classes, which were [...]'
- id: 3994
  author: ! 'code review:: : &laquo; summer placement::2010/dublin'
  author_email: ''
  author_url: http://kavisummer.wordpress.com/2010/08/05/code-review/
  date: !binary |-
    MjAxMC0wOC0wNSAwMTo0Njo1MyAtMDQwMA==
  date_gmt: !binary |-
    MjAxMC0wOC0wNSAwOTo0Njo1MyAtMDQwMA==
  content: ! '[...] are needed for particular tasks. i downloaded them from internet.
    SendOSC class i downloaded from this site. it was very hard to find any tutorials
    or &Acirc;&nbsp;discussions on how to write osc signal sending [...]'
---
A couple months back I picked up a Make Controller from <a href="http://makingthings.com" target="_blank">Making Things</a> to do some experimentation with Flash Media Server and physical computing. I'm just now getting around to writing up my experiences about getting set up with the Make Controller. While the <a href="http://www.makingthings.com/resources/tutorials/flash/index_html/overview" target="_blank">tutorial on the Making Things site</a> was great for getting started using AS2 with their .mxp extension, it didn't offer up anything on how to get started with what I really wanted to do, which was a project that would benefit from the performance of AS3 and Flash Player 9, so I had to take matters into my own hands.

<a id="more"></a><a id="more-10"></a>
Before we get started on what exactly that involved, if you are interested in the Make Controller, I would definitely recommend buying not only the board itself, but also the Accessory Pack.  I made the mistake of initially getting just the controller, which without electronics for input and output is cool, but turning on and off the four LEDs on the board is not very exciting nor practical.  I suppose that I could have built some, but I wasn't quite sure of all of the possibilities yet and wanted to grasp the basics by building a couple prototype projects based on some working sensors before firing up the soldering iron.  The Accessory Pack contains some basic controls that you can use out of the box to get started such as several motors, a slide pot, and a distance measuring sensor among other goodies.  The other nice thing that the kit contains is an AC power adapter so that it becomes unnecessary to have USB connected to power the board.

I'm not going to go into great detail of OSC, because I know very little about it, but I will give some background on why it is necessary.  The Make Controller allows communication in several ways, one is via USB and the other is using its on-board ethernet controller.  For connecting the Make Controller to a computer running an instance of the Flash Player, ethernet is the only way that it is possible.  When using ethernet, UDP packets are sent and received via TCP/IP from the Make Controller to the computer that it is connected to using something called OSC - Open Sound Control which, from what I gather, somewhat resembles MIDI.

However, because Flash cannot connect and send OSC directly to the Make Controller, an intermediary is required. In this case, it is a Java socket server called FLOSC (Flash OSC) that is a piece of middleware that accepts XML socket connections from the Flash Player and enables TCP/IP networking with the Make Controller. Once the socket connection is established, XML packets that contain OSC commands are created with ActionScript and then sent to FLOSC.  FLOSC then converts those XML packets into OSC packets and passes them to the Make Controller.  Basically the same process happens in reverse when input is generated from the Make Controller.

After downloading the Flash-specific packages from <a href="http://prdownloads.sourceforge.net/makingthings/mc-flash-0.1.zip" target="_blank">SourceForge</a>, the first step was to get the FLOSC server running, which is as simple as executing the following from the command line (on OS X) to fire it up:
<pre lang="actionscript">java Gateway 10000 10000</pre>
<pre lang="actionscript"></pre>
This command starts up the socket server and configures it to send and receive packets on port 10000. The only gotcha is to remember that you might have to change your network settings in order to communicate with the Make Controller over ethernet. Being a Mac user, I just set up an alternate network profile to enable easy switching between my usual AirPort setup and one that works with the Make Controller.  After getting that set up, I connected the board via ethernet, connected the AC adapter and ran some of the Making Things examples using AS2 and everything worked. I then wanted to really get down to business which would mean either finding AS3 classes for OSC or porting over the existing ones from Making Things.

Fortunately, after poking around a bit looking for AS3 OSC classes, I ran across the <a href="http://fwiidom.org" target="_blank">FWiidom project</a>, which besides being a totally cool project, also happens to use the same technique with FLOSC as the Make Controller for communicating with a Wiimote using AS3.  I grabbed the best-named release I've seen in a long time, the <a href="http://www.fwiidom.org/?page_id=11" target="_blank">"FWiidom [pre-alpha very nasty hacky version]"</a> from their site, which also, by the way, contains the FLOSC server.

The Fwiidom package contains several classes that are specific to the Wiimote implementation, so you can either remove them, or just ignore them when working with the Make Controller.  The classes that are required for OSC are the three in the org.fwiidom.osc package. After grabbing those, and looking through them, it was time to see if they would actually work, being as how there is actually no documentation that I could find about using these classes for the Make Controller, so that is where this article comes in.  Fortunately, they're well written and use events, so that made the first test I wanted to run with the classes fairly easy. I decided to code up the Make Controller equivalent of the ubiquitous "hello world" as a test, which is turning on LED0 on the application board.

So, after firing up the FLOSC server and knowing what I was going to do with the Make Controller, the next step was to attempt an XML socket connection to the server.  In taking a look at the OSCConnection class, the constructor is very straightforward, accepting two arguments representing the IP address and port number:
<pre lang="actionscript">public function OSCConnection(inIp:String, inPort:Number)</pre>
<pre lang="actionscript"></pre>
So, the instantiation in my test class looks like the following:
<pre lang="actionscript">oscConn = new OSCConnection(STR_LOCAL_IP, NUM_PORT);</pre>
<pre lang="actionscript"></pre>
Easy, right? In this case I've assigned constants for the local IP (the one assigned to the computer connecting to the Make Controller) and port that I then pass to the constructor.  However, before calling the connect() method, in order to make sure that a connection is actually taking place, there are some events to listen for that are dispatched from the OSCConnection object:
<pre lang="actionscript">oscConn.addEventListener(OSCConnectionEvent.ON_CONNECT, onConnect);
oscConn.addEventListener(OSCConnectionEvent.ON_CONNECT_ERROR, onConnectError);
oscConn.addEventListener(OSCConnectionEvent.ON_CLOSE, onClose);
oscConn.connect();</pre>
<pre lang="actionscript"></pre>
Those were all very straightforward, so after writing out the event handlers for those event, a quick publish indicated a successful connection to the Make Controller.  Woohoo!  But wait, there's a problem - for some reason the ON_CONNECT_ERROR event is always dispatched once, then ON_CONNECT is received.  This looks like a problem with Line 40 in the OSCConnection class:
<pre lang="actionscript">if (!mSocket.connect(mIp,mPort)) onConnectError();</pre>
<pre lang="actionscript"></pre>
I changed this to the following, which seems to work just fine:
<pre language="actionscript">mSocket.connect(mIp,mPort);</pre>
<pre language="actionscript"></pre>
<pre language="actionscript"></pre>
Although you can just leave it and ignore the ON_CONNECT_ERROR event, but that wouldn't exactly be a recommended best practice now would it?  Now on to actually doing something - sending the OSC message to the board. As mentioned previously, I want to turn on LED0 on the application board, which represented by the following OSC message:
<pre lang="actionscript">/appled/0/state 1</pre>
<pre lang="actionscript"></pre>
In ActionScript, this OSC message will be represented using an instance of the OSCPacket class, which is just a value object that stores the message:
<pre lang="actionscript">var oscPacket:OSCPacket = new OSCPacket("/appled/0/state", [1], STR_REMOTE_IP, NUM_PORT);</pre>
<pre lang="actionscript"></pre>
After constructing the OSC packet, sending it to FLOSC is super-easy and can be done like so:
<pre lang="actionscript">oscConn.sendOSCPacket(new OSCPacket("/appled/0/state", [0], STR_REMOTE_IP, NUM_PORT));</pre>
<pre lang="actionscript"></pre>
That's all there is to it.  Here's the entire class coded up (<a href="http://phy5ics.com/blog/wp-content/uploads/2007/07/makecontrolleras3_article1.zip" title="AS3 and Make Controller Part 1 Source Code">download source</a>):
<pre lang="actionscript">
package com.phy5ics.make {

import flash.display.Sprite;
import flash.display.MovieClip;
import flash.events.MouseEvent;
import org.fwiidom.osc.*;

public class MakeLEDTest extends MovieClip {
private var oscConn:OSCConnection;
private static const STR_LOCAL_IP:String = "192.168.5.210";
private static const STR_REMOTE_IP:String = "192.168.5.200";
private static const NUM_PORT:Number = 10000;

public function MakeLEDTest() {
//Initialize connection to the FLOSC server
oscConn = new OSCConnection(STR_LOCAL_IP, NUM_PORT);
oscConn.addEventListener(OSCConnectionEvent.ON_CONNECT, onConnect);
oscConn.addEventListener(OSCConnectionEvent.ON_CONNECT_ERROR, onConnectError);
oscConn.addEventListener(OSCConnectionEvent.ON_CLOSE, onClose);
oscConn.connect();
}

private function onConnect(evtEvent:OSCConnectionEvent):void {
trace("Connection established");
//Draw a sprite in the middle of the stage and assign a listener
var btnSendOSC:Sprite = new Sprite();
btnSendOSC.graphics.beginFill(0x666666);
var uintWidth:uint = 100;
var uintHeight:uint = 30;
btnSendOSC.graphics.drawRect(stage.stageWidth / 2 - uintWidth / 2, stage.stageHeight / 2 - uintHeight / 2, uintWidth, uintHeight);
btnSendOSC.buttonMode = true;
btnSendOSC.addEventListener(MouseEvent.CLICK, onSendOSCClick);
addChild(btnSendOSC);
}

private function onConnectError(evtEvent:OSCConnectionEvent):void {
trace("Connection error");
}

private function onClose(evtEvent:OSCConnectionEvent):void {
trace("Connection closed");
}

private function onSendOSCClick(evtClick:MouseEvent):void {
//Send the actual OSC packet
oscConn.sendOSCPacket(new OSCPacket("/appled/0/state", [1], STR_REMOTE_IP, NUM_PORT));
}

}

}</pre>
<pre lang="actionscript"></pre>
<pre lang="actionscript"></pre>
Sending an OSC message to the Make Controller is really quite simple and can be done in just a few lines of code.  In the next installment, I'll be looking at how to get the values of inputs from the Make Controller.

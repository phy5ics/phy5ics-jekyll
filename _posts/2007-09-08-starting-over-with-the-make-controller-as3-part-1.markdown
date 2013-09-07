---
layout: post
status: publish
published: true
title: Starting Over with the Make Controller + AS3 - Part 1
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "MakingThings just released a bunch of software updates involved with Flash
  and the Make Controller that nullifies a lot of my previous work with AS3 and flosc.
  \ While some of the components still seem a bit buggy, they represent some major
  improvements.  The best news to come out of this round of releases is that the <em>flosc</em>
  socket server can now be ditched (sorry, Ben Chun) in favor of connecting to the
  Make Controller using a new version of <em>mchelper</em>.  Additionally it is
  now possible, from Flash,  to connect to a board using either USB or Ethernet.  As
  a result, I'm starting my series over to take these latest developments into account.\r\n"
wordpress_id: 30
wordpress_url: http://phy5ics.com/blog/2007/09/08/starting-over-with-the-make-controller-as3-part-1/
date: 2007-09-08 11:22:49.000000000 -04:00
categories:
- AS3
- Make Controller
tags: []
comments:
- id: 3638
  author: Shaun Gilbert &raquo; Blog Archive &raquo; John Barton
  author_email: ''
  author_url: http://www.shaungilbert.com/blog/?p=55
  date: !binary |-
    MjAwOC0xMC0yMiAwNTozNzozNCAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0xMC0yMiAxMzozNzozNCAtMDQwMA==
  content: ! '[...] http://phy5ics.com/blog/2007/09/08/starting-over-with-the-make-controller-as3-part-1/
    [...]'
---
MakingThings just released a bunch of software updates involved with Flash and the Make Controller that nullifies a lot of my previous work with AS3 and flosc.  While some of the components still seem a bit buggy, they represent some major improvements.  The best news to come out of this round of releases is that the <em>flosc</em> socket server can now be ditched (sorry, Ben Chun) in favor of connecting to the Make Controller using a new version of <em>mchelper</em>.  Additionally it is now possible, from Flash,  to connect to a board using either USB or Ethernet.  As a result, I'm starting my series over to take these latest developments into account.
<a id="more"></a><a id="more-30"></a>
To get stared, grab the latest versions of the following files from <a href="http://makingthings.com/resources/downloads" target="_blank">MakingThings</a>:

- mchelper 2.0
- heavy 1.2 rc4
- New AS3 classes

<strong>Step 1: Erase the Current Firmware</strong>
To do this, connect power to the board and use a jumper on the 2 pins marked "ERASE" near the JTAG connector on the board.  This will erase everything on the board including the firmware.  Turn off the power, remove the jumper, then reconnect the power to restart the board.  This will put the board into receive mode.

<a href="http://phy5ics.com/blog/wp-content/uploads/2007/09/erase_board.gif" title="Erase Pins"><img src="http://phy5ics.com/blog/wp-content/uploads/2007/09/erase_board.gif" alt="Erase Pins" /></a>
<strong>
Step 2: Upload heavy 1.2 rc4</strong>
There seems to be a bug in <em>mchelper 2.0</em> in that the option to upload firmware to the Make Controller is always grayed-out.  So you'll need to use a previous version in order to install the new <em>heavy 1.2 rc4</em> firmware.  To do this, fire up <em>mchelper 1.2</em> then simply select the .bin file and click upload.  Restart the board after the firmware has updated.

<strong>Step 3: Connecting to Flash</strong>
Close <em>mchelper 1.2</em> and open up <em>mchelper 2.0</em>.  Send a test message to the board to make sure that everything is setup properly.

<em>mchelper 2.0</em> now has an XML socket server built into it (unfortunately not a binary socket server), so rather than connecting to flosc as we did in the past, we connect to mchelper.  This is straightforward enough:

<code>var mcfConnection:McFlashConnect = new McFlashConnect();</code>

From there, it's just a matter of setting up a bunch of event listeners, which isn't all that different from my previous examples:

<code>mcfConnection.addEventListener(McEvent.ON_CONNECT, onConnect);</code>
<code>mcfConnection.addEventListener(McEvent.ON_CONNECT_ERROR, onConnectError);</code>
<code>mcfConnection.addEventListener(McEvent.ON_CLOSE, onClose);</code>
<code>mcfConnection.addEventListener(McEvent.ON_MESSAGE_IN, onMessageIn);</code>
<code>mcfConnection.addEventListener(McEvent.ON_BOARD_ARRIVED, onBoardArrived);</code>
<code>mcfConnection.addEventListener(McEvent.ON_BOARD_REMOVED, onBoardRemoved);</code>
<code>mcfConnection.connect();</code>

One of the primary differences between the new MakingThings AS3 classes and the others that I've written about is the addition of some methods to not only connect to <em>mchelper</em> (previously <em>flosc</em>), but also to determine when a controller board is actually connected.  This is a significant improvement, as then you can be sure that you're actually connected to the board.  Additionally, the way the new classes are written opens up the possibility of connecting multiple boards, as they can be addressed individually by IP address, USB address, name (i.e. <code>/system/name</code>) or serial number, which is a super cool feature.

Once the connection to <em>mchelper</em> is established and a board is detected, sending and receiving OSC packets is rather straightforward.  Here's an example of how to send an OSC packet:

<code>mcfConnection.send("/system/name", []);</code>

A really cool feature of <em>mchelper 2.0</em> is that OSC packets that are being sent and received from Flash are traced out to the dialog window in <em>mchelper</em>, which helps tremendously with debugging.  After compiling a SWF that sends an OSC packet containing <code>/system/name</code> you should see the following in mchelper:

<code>XML server --- New XML Connection</code>
<code>XML server --- /system/name</code>
<code>USB --- /system/name Make Controller Kit</code>

That's really all there is to it.  Thankfully, the new MakingThings code is much less unwieldy and ditches flosc, so kudos to them for making much-needed improvements.

<strong>Step 4: Conclusion - Let the Hacking Begin</strong>
I haven't had a chance to look at the new AS3 classes in great detail, but there are some nice new features.  However, one thing that I noticed that was a bit disappointing was that all of the XML parsing is being done using <code>XMLDocument</code> objects, which have been deprecated in AS3.  There's no reason why this shouldn't be using Flash Player 9's native E4X capabilities, so that'll be one of the first things that I rewrite, being as how I already did that in the MakingThings AS2 classes that I ported to AS3 a while back.

<a href="http://phy5ics.com/blog/wp-content/uploads/2007/09/ConnectionTest.as">Download the full sample class here</a>

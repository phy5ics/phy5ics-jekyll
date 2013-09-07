---
layout: post
status: publish
published: true
title: AS3 + Make Controller Important Update (AKA Not Part 5)
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "As those of you that have been reading along with the series might extrapolate,
  this post is supposed to be Part 5.  However, given some things that I've discovered
  in the Fwiidom AS3 implementation as well as some issues in the MakingThings AS2
  classes, which I then ported to AS3 and in the process propogated those bugs, this
  is now an update on some progress made with some collaboration and refactoring.\r\n\r\n"
wordpress_id: 28
wordpress_url: http://phy5ics.com/blog/2007/08/20/as3-make-controller-important-update-aka-not-part-5/
date: 2007-08-20 19:13:41.000000000 -04:00
categories:
- AS3
- Make Controller
tags: []
comments:
- id: 38
  author: Donovan Adams
  author_email: donovan@hydrotik.com
  author_url: http://blog.hydrotik.com
  date: !binary |-
    MjAwNy0wOC0yOCAxMTo0NTo1NyAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOC0yOCAxOTo0NTo1NyAtMDQwMA==
  content: ! "I've also been noticing strange things when testing the files with my
    current setup. Certain times things will work, and other times they will not.
    I noticed even adding a private variable to the class would prevent the board
    from responding.  After tinkering for a while I started to get the impression
    that using core Flash types would break the transmission of commands but I managed
    to add a private array variable and it worked. I was finally able to get the LED's
    to sequence using the time class. I feel your frustration in trying to get something
    so easy happening in flash now becomes tricky with the board with all the possible
    issues in the flow of data. I would certainly love to hear what you come up with
    since this seems to be what's creating my issues. Sometimes I get packet listeners
    working and sometimes they don't.\r\n\r\nI also plan on seeing if I can set up
    the controller so that it works with my network settings as well as creating a
    class specifically for configuring the network settings using the\r\n\r\n/network/dhcp
    1\r\n/network/address\r\n\r\nCommands. Resetting my network settings is
    a pain when you are tryng to access the net for resources while getting this thing
    behaving:) I'm also thinking of including a reset method using\r\n\r\n/system/reset
    1 \r\n/system/active \r\n\r\nI plan on putting some examples of my as3
    experiments with the kit so keep me posted.  I'm also eagerly waiting on my accessory
    kit;) Thanks so much for these posts. They have been very helpful in jumping into
    this!"
- id: 96
  author: Nacho
  author_email: nacho@h-umus.it
  author_url: ''
  date: !binary |-
    MjAwNy0wOS0wNSAwNTowNToyNSAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0wNSAxMzowNToyNSAtMDQwMA==
  content: ! "Hi Barton!\r\n\r\nstrangely today i came up with your blog (as these
    days I couldn't believe there's still no one who has updated FLOSC server so I'm
    still searching). I'm happy to see that the changes I made where helpful at least
    for someone. These days I've been working on an AS3 OSC library that should help
    developers to create new Flash-OSC connected apps (I'm using it as underground
    layer for a AS3 TUIOClient, if wanna know more google for \"reactivision\"). It's
    still work in progress but works pretty well. If you contact me I'll be happy
    to share my work with you. Who knows, maybe someone should made a \"Flosc 2.0\"
    site ;)\r\n\r\nPD: Nacho stands for Ignacio (an Spanish male name)"
- id: 98
  author: Donovan Adams
  author_email: donovan@hydrotik.com
  author_url: http://blog.hydrotik.com
  date: !binary |-
    MjAwNy0wOS0wNSAwOTo1NzoxOCAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0wNSAxNzo1NzoxOCAtMDQwMA==
  content: ! "Here are the changes I made to your OSC port:\r\n\r\n\r\n<code>\r\npublic
    function sendOSCPacket(outPacket:OSCPacket) : void {\r\n\t\t\tvar xmlOut:XMLDocument
    = new XMLDocument();\r\n\t\t\t\t\r\n\t\t\tvar osc:XMLNode = xmlOut.createElement(\"OSCPACKET\");\r\n\t\t\tosc.attributes.TIME
    = 0;\r\n\t\t\tosc.attributes.PORT = outPacket.port;\r\n\t\t\tosc.attributes.ADDRESS
    = outPacket.address;\r\n\t\t\r\n\t\t\tvar message:XMLNode = xmlOut.createElement(\"MESSAGE\");\r\n\t\t\tmessage.attributes.NAME
    = outPacket.name;\r\n\t\t\r\n\t\t\tfor (var i:Number=0;i\r\n\r\n\r\nI added two
    methods to reorder the attributes and changing the type to \"i\" made it work.
    Any ideas on why?\r\n\r\n\r\nhttp://blog.hydrotik.com/2007/09/04/making-things-as3-part-1-and-2-led-sound-visualizer/\r\nhttp://blog.hydrotik.com/2007/09/04/making-things-as3-part-3-serial-lcd/\r\n\r\nHey
    Nacho!\r\nIs your work using the Binary Socket classes?"
- id: 99
  author: Donovan Adams
  author_email: donovan@hydrotik.com
  author_url: http://blog.hydrotik.com
  date: !binary |-
    MjAwNy0wOS0wNSAwOTo1ODo0OCAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0wNSAxNzo1ODo0OCAtMDQwMA==
  content: ! "Code didn't translate.\r\n\r\nin OSCConnection I added:\r\n\r\nprivate
    function setType(arg:XMLNode, str:String):void{\r\n\t\t\targ.attributes.TYPE =
    str;\r\n\t\t}\r\n\t\t\r\n\t\tprivate function setValue(arg:XMLNode, str:String):void{\r\n\t\t\targ.attributes.VALUE
    = str;\r\n\t\t}\r\n\r\nand changed:\r\npublic function sendOSCPacket(outPacket:OSCPacket)
    : void {\r\n\t\t\tvar xmlOut:XMLDocument = new XMLDocument();\r\n\t\t\t\t\r\n\t\t\tvar
    osc:XMLNode = xmlOut.createElement(\"OSCPACKET\");\r\n\t\t\tosc.attributes.TIME
    = 0;\r\n\t\t\tosc.attributes.PORT = outPacket.port;\r\n\t\t\tosc.attributes.ADDRESS
    = outPacket.address;\r\n\t\t\r\n\t\t\tvar message:XMLNode = xmlOut.createElement(\"MESSAGE\");\r\n\t\t\tmessage.attributes.NAME
    = outPacket.name;\r\n\t\t\r\n\t\t\tfor (var i:Number=0;i"
- id: 100
  author: Donovan Adams
  author_email: donovan@hydrotik.com
  author_url: http://blog.hydrotik.com
  date: !binary |-
    MjAwNy0wOS0wNSAxMDowMDozMyAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0wNSAxODowMDozMyAtMDQwMA==
  content: ! "I wish you could post code in the comments and have it work normally;)
    \ Sorry for the mutiple messages. Check out my edits here:\r\n\r\nhttp://blog.hydrotik.com/2007/09/04/making-things-as3-part-3-serial-lcd/"
- id: 112
  author: Nacho
  author_email: nacho@h-umus.it
  author_url: ''
  date: !binary |-
    MjAwNy0wOS0wNiAwMDo1MjowMCAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0wNiAwODo1MjowMCAtMDQwMA==
  content: ! "Hi!\r\n\r\nDonovan, no, I'm not using binary sockets (I thought for
    a little about doing it but as XML with EAX4 seems so powerful in AS3 and is much
    easer to read I discarded it, as a new server should also be done xD)\r\n\r\nI
    rewrote(and still rewriting) the OSC Classes I sent to Adam Robertson to be more
    efficient and easer to use (for example there's a new class called OSCMessage
    so an OSCPacket stores and Array of messages and Arguments are part of a Message
    and not part of a packet, also the attribute \"name\" from OSCPacket is conceptually
    wrong as a every Message has it's own \"name\" and a packet can contains more
    than one message if it's an  OSC bundle).\r\n\r\nI've created a \"google poject\"
    account to upload source, you can fnf it at http://code.google.com/p/flosc/"
- id: 114
  author: Nacho
  author_email: nacho@h-umus.it
  author_url: ''
  date: !binary |-
    MjAwNy0wOS0wNiAwMjowOToxNSAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0wNiAxMDowOToxNSAtMDQwMA==
  content: did I wrote EAX4 ??? LOL, I really meant E4X
- id: 157
  author: Barton
  author_email: jb@phy5ics.com
  author_url: http://phy5ics.com/blog/
  date: !binary |-
    MjAwNy0wOS0xMiAxMToyNjoyMSAtMDQwMA==
  date_gmt: !binary |-
    MjAwNy0wOS0xMiAxOToyNjoyMSAtMDQwMA==
  content: Thanks for the input Nacho and Donovan.  I think that in an effort to make
    sure that everyone has access to the latest changes and code that I've been working
    on, I'll be setting up a Subversion repository.  That way, I can then work with
    you guys to get your code integrated in a more organized fashion and allow for
    the creation of different branches and such.
---
As those of you that have been reading along with the series might extrapolate, this post is supposed to be Part 5.  However, given some things that I've discovered in the Fwiidom AS3 implementation as well as some issues in the MakingThings AS2 classes, which I then ported to AS3 and in the process propogated those bugs, this is now an update on some progress made with some collaboration and refactoring.

<a id="more"></a><a id="more-28"></a>

A couple weeks back I received some updates to the Fwiidom classes and the FLOSC server that a guy name Nacho (that's all I know about him or her) did via Adam at <a href="http://dustypixels.com/blog/" target="_blank">Dusty Pixels</a> (who created <a href="http://fwiidom.org" target="_blank">Fwiidom</a>).  I was super busy and didn't have time to put them through their paces until over the weekend.  When I did, I started noticing some really strange bugs where certain OSC commands would work (using the original FLOSC server - version 0.3.1), then by simply inserting a trace statement, they would cease working and other OSC commands that were previously broken miraculously started working.

This drove me to the brink of insanity for about 4 hours during which I tested the Fwiidom classes, my ported MakingThings AS3 classes and the original MakingThings AS2 classes.  Then it dawned on me that the order of the <code>type</code> and <code>value</code> attributes in the XML that was being sent from the Flash Player to the FLOSC server was getting reversed and this was causing the issues.  After that, I remembered the update to the FLOSC server and referred back to the email from Adam.   Looking at that email again, I see the forwarded message from Nacho where he mentions that the FLOSC server was updated to parse the XML using the DOM, so that the order of attributes in the XML-formatted OSC messages sent to FLOSC didn't matter.  Doh!  Apparently he encountered the same problem as I and corrected it at the server level, rather than in ActionScript, as I had been attempting to do.

So, I'm going to work a bit more on some testing of the updated classes and refactoring of my ported AS3 classes and release mine and then work to coordinate with Adam and the mysterious Nacho to figure out the best way to share these updates.  From there, I'll continue on with Part 5 and go back to update some of the previous articles with relevant changes.

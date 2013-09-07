---
layout: post
status: publish
published: true
title: Make Controller, mchelper 2.0 and /serial/ Issues
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "I've been attempting to hook up a serial GPS device to my Make Controller
  and read in data using OSC commands from mchelper prior to interfacing it with AS3
  (as an aside, it's really nice to be able to do this with the new version of mchelper).
  While I've been able to write to the serial port successfully using both /serial/char
  and /serial/block, reading from it always yields some sort of disaster.\r\n"
wordpress_id: 32
wordpress_url: http://phy5ics.com/blog/2007/10/02/make-controller-mchelper-20-and-serial-subsytem-issues/
date: 2007-10-02 20:06:34.000000000 -04:00
categories:
- Make Controller
- GPS
tags: []
comments:
- id: 3929
  author: Kevin Groce
  author_email: kevin.groce@asurion.com
  author_url: http://Website
  date: !binary |-
    MjAwOC0xMS0yMyAwNDoyODozMCAtMDUwMA==
  date_gmt: !binary |-
    MjAwOC0xMS0yMyAxMjoyODozMCAtMDUwMA==
  content: Did you ever get this working?
- id: 3959
  author: Bill Bartmann
  author_email: claricekxj@gmail.com
  author_url: http://Website
  date: !binary |-
    MjAwOS0wOS0wMiAwMjowNzoxMSAtMDQwMA==
  date_gmt: !binary |-
    MjAwOS0wOS0wMiAxMDowNzoxMSAtMDQwMA==
  content: Excellent site, keep up the good work
- id: 4004
  author: Dollie
  author_email: kingspottery@atomic.net
  author_url: http://www.bing.com/
  date: !binary |-
    MjAxMS0wNC0xMSAxNzo0OTo0OCAtMDQwMA==
  date_gmt: !binary |-
    MjAxMS0wNC0xMiAwMTo0OTo0OCAtMDQwMA==
  content: You've hit the ball out the park! Increbdile!
---
I've been attempting to hook up a serial GPS device to my Make Controller and read in data using OSC commands from mchelper prior to interfacing it with AS3 (as an aside, it's really nice to be able to do this with the new version of mchelper). While I've been able to write to the serial port successfully using both /serial/char and /serial/block, reading from it always yields some sort of disaster.
<a id="more"></a><a id="more-32"></a>Initially I thought that perhaps the level shifter was not functioning properly. However, checking it out with a multimeter I found it to be otherwise. Then, I verified that the level shifter was indeed reversing TX/RX as it does, and it was indeed. I then connected the GPS device directly to my computer using a RS232/USB converter and was successfully able to read the serial data, so that eliminated the actual GPS receiver as the problem. Checking on those things seemed to eliminate what I figured were circuit or hardware problems, which left only the Make Controller and mchelper as the issue.

So here are a couple use cases where I run into issues:

Attempting to set the baud rate using /serial/baud 4800 is apparently successful, until I type in /serial/baud to return the value and it is inexplicably set to 4828!? Any other number that I pick at random results in it being set correctly. I have no idea what to make of this behavior.

As an additional problem, when I type in /serial/readable I receive a value of 1048760. If I then enter /serial/block to attempt to read that data, mchelper crashes [Exception: EXC_BAD_ACCESS (0x0001) Codes: KERN_PROTECTION_FAILURE (0x0002) at 0x00000000)]. If I then try /serial/block 128 (or any other int), then I get a /serial/error Bad Data response.

<strong>Note: </strong>I posted the above to the <a href="http://www.makingthings.com/forum/discussion/view_topic?topic_id=1169">MakingThings forum</a> last night, and Liam promptly responded that this is indeed a problem with mchelper 2.0 and its implementation of OSC blobs that are returned by /serial/block.  As for the incorrect baud rate issue, he's not quite sure, but hopefully that will be resolved soon as well.  I'll be posting some how-to articles on bidirectional serial communication and using GPS devices with the Make Controller, OSC and AS3 once those bugs get straightened out.

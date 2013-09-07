---
layout: post
status: publish
published: true
title: Getting Started with AS3 and the Make Controller - Part 2
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "In attempting to wire up a slide potentiometer to the Make Controller
  and poll for its values using AS3, which was supposed to be Part 2 of this series
  of articles, I ran into a significant problem. (To understand what exactly I was
  trying to do, check out Getting Started with AS3 and the Make Controller - Part
  3 - Determining Input Values.) After coding up my example for the article in AS3,
  I expected that when publishing the .SWF, everything would be working, right?  No,
  of course not.  That would be far too easy.  After checking and double-checking
  my code thinking that I probably just did something stupid while working on it late
  at night, I was stumped.  I slept on it and still couldn't figure it out.  After
  much frustration, I opted to revert back to AS2 to see if maybe there was an issue
  with the potentiometer and re-wrote the example using AS2 and the MakingThings AS2
  classes and it worked a treat.\r\n\r\n"
wordpress_id: 13
wordpress_url: http://phy5ics.com/blog/2007/07/27/getting-started-with-as3-and-the-make-controller-part-2-let-the-hacking-begin/
date: 2007-07-26 11:02:08.000000000 -04:00
categories:
- AS3
- Make Controller
tags: []
comments:
- id: 3963
  author: links for 2009-10-04 at adam hoyle presents suckmypixel
  author_email: ''
  author_url: http://www.adamhoyle.com/blog/?p=708
  date: !binary |-
    MjAwOS0xMC0wNCAwNDoyOToyMiAtMDQwMA==
  date_gmt: !binary |-
    MjAwOS0xMC0wNCAxMjoyOToyMiAtMDQwMA==
  content: ! '[...] phy5ics &Acirc;&raquo; Blog Archive &Acirc;&raquo; Getting Started
    with AS3 and the Make Controller - Part 2 (tags: as3 osc) [...]'
---
In attempting to wire up a slide potentiometer to the Make Controller and poll for its values using AS3, which was supposed to be Part 2 of this series of articles, I ran into a significant problem. (To understand what exactly I was trying to do, check out Getting Started with AS3 and the Make Controller - Part 3 - Determining Input Values.) After coding up my example for the article in AS3, I expected that when publishing the .SWF, everything would be working, right?  No, of course not.  That would be far too easy.  After checking and double-checking my code thinking that I probably just did something stupid while working on it late at night, I was stumped.  I slept on it and still couldn't figure it out.  After much frustration, I opted to revert back to AS2 to see if maybe there was an issue with the potentiometer and re-wrote the example using AS2 and the MakingThings AS2 classes and it worked a treat.

<a id="more"></a><a id="more-13"></a>

This led me to believe that the culprit had to be somewhere in the FWiidom classes, which wouldn't be all that surprising, given that they were designed and tested for use with a Wiimote.  The other possibility was that it might have been a bug with Flash Player 9 or the Flash 9 Alpha that I was using at the time. To eliminate this possibility, I did a direct port of the MakingThings classes over to AS3.  I didn't spend any time making any improvements to it because I was only curious to see if it would actually work, which it actually did.  All of a sudden I was receiving OSC packets from the Make Controller.

That being said, I haven't done all that much testing on the AS3 version of those classes, but I'll make them available here for download without any promises as to its reliability:

<a href="http://phy5ics.com/blog/wp-content/uploads/2007/07/makingthings_flosc_as3.zip" title="MakingThings FLOSC Classes AS3 Port">Download MakingThings FLOSC Classes AS3 Port</a>

I'll be sending these over to the MakingThings guys to check out, but if you download these and use them, I'd love to get input on any issues that are discovered.

Not being easily discouraged, I was still determined to figure out what the issue was with the FWiidom classes.  So, I began to examine the incoming and outgoing OSC packets and saw that there were actually packets being returned from the Make Controller.  This was good news and allowed me to follow the packets through the FWiidom classes.  I realized that the datatypes that are sent from the Make Controller are slightly different that what is expected to be received from a Wiimote.  In this case, the Make Controller sends a type "i" packet as a float, whereas the Wiimote sends a type "f" as a float.  In the Fwiidom classes, there was not a type=="i" in the conditional statement and no else statement, so it was not being evaluated anywhere.

Once I figured this out, to fix this issue, I added the following code to the OSCConnection class after line 109:
<pre lang="actionscript">} else if (type=="i") {
data.push(parseFloat(child.attributes.VALUE));</pre>
<pre lang="actionscript"></pre>
Compiling the SWF for the 39396216th time, I was amazed to see it was actually working.  So, as a result, I'll be getting in touch with the fine folks at FWiidom to see if they'll add this to their classes so that when people download them from their site to use with the Make Controller, they won't go insane trying it to figure out like I did.  In the meantime, here is the Fwiidom OSC package with my modification:

<a href="http://phy5ics.com/blog/wp-content/uploads/2007/07/fwiidom_flosc_makecontroller.zip" title="FWiidom Make Controller Update">Download FWiidom Make Controller Update</a>

Furthermore, I'll probably end up writing OSC bundles into the FWiidom classes, being as how they would be quite useful in complex projects.  I'm assuming that they were not included in the FWiidom version because bundles are not implemented for the Wiimote.

Now that we have that all straightened out, we can get back to the examples in Part 3 - Determining Input Values.

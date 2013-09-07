---
layout: post
status: publish
published: true
title: FlexQuake
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "I just attended Adobe's on AIR Bus Tour the other day on its stop in Los
  Angeles.  While typically those types of event don't delve deep enough into details
  to be of much interest, I figured that I'd attend anyway since I've been away from
  the computer for so long on vacation and needed to catch up on some new stuff.  The
  vast majority of the talks were JavaScript-centric which was interesting and perhaps
  highlights Adobe's desire to sway over the current generation of standards- and
  open-source centric client-side developers to a proprietary technology, but more
  on that in another post.\r\n\r\nAnyway, I had hopes of converting an app that I
  had been working on over to an AIR app for desktop deployment.  The app that I was
  going to port over was a quick and rather silly app that I threw together using
  the Yahoo! Maps API and an geoRSS feed constructed using Yahoo! Pipes to filter
  earthquake data from the USGS.  However, I quickly remembered that developing against
  an alpha release of anything can be tedious at best.\r\n\r\n"
wordpress_id: 6
wordpress_url: http://phy5ics.com/blog/?p=6
date: 2007-07-20 07:44:50.000000000 -04:00
categories:
- Flex
tags: []
comments: []
---
I just attended Adobe's on AIR Bus Tour the other day on its stop in Los Angeles.  While typically those types of event don't delve deep enough into details to be of much interest, I figured that I'd attend anyway since I've been away from the computer for so long on vacation and needed to catch up on some new stuff.  The vast majority of the talks were JavaScript-centric which was interesting and perhaps highlights Adobe's desire to sway over the current generation of standards- and open-source centric client-side developers to a proprietary technology, but more on that in another post.

Anyway, I had hopes of converting an app that I had been working on over to an AIR app for desktop deployment.  The app that I was going to port over was a quick and rather silly app that I threw together using the Yahoo! Maps API and an geoRSS feed constructed using Yahoo! Pipes to filter earthquake data from the USGS.  However, I quickly remembered that developing against an alpha release of anything can be tedious at best.

<a id="more"></a><a id="more-6"></a>

Being as how I had implemented Yahoo! Maps in the app, which is apparently still being fully ported to AS3 and uses a wrapper to interface with the AS2 version of the mapping APIs and actual map SWF, I immediately encountered an error on publish:

<code class="prettyprint">Error: Error #2067: The ExternalInterface is not available in this container. ExternalInterface requires Internet Explorer, ActiveX, Firefox, Mozilla 1.7.5 and greater, or other browsers that support NPRuntime</code>

So, until I get a chance to code an HTML/JS version of the API using the new HTML component, I'm stuck with FlexQuake, not the intended AIRQuake:

<a href="http://phy5ics.com/flexquake" title="FlexQuake"><img src="http://phy5ics.com/blog/wp-content/uploads/2007/07/flexquake.thumbnail.jpg" alt="FlexQuake" height="125" width="171" /></a>

It's still kinda cool if you live in California and want to see the earthquakes over M 2.5 that have occurred over the last 7 days.

<a href="http://phy5ics.com/flexquake">http://phy5ics.com/flexquake</a>

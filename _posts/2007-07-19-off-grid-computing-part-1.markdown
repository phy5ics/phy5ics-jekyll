---
layout: post
status: publish
published: true
title: ! 'Off-Grid Computing: Part 1'
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "The goal of this article is to relate several strategies and technologies
  to improve the efficiency in the collection, analysis and presentation of field
  data.  I have limited the suggestions to only technologies that are free (but not
  necessarily open-source) and/or utilize public APIs so as to make them accessible
  to an audience who constantly finds their budgets diminishing.  However, prior to
  getting into that, allow me to relate the context of some of these recommendations...\r\n\r\n"
wordpress_id: 3
wordpress_url: http://phy5ics.com/blog/?p=3
date: 2007-07-19 19:58:17.000000000 -04:00
categories:
- General Technology
tags: []
comments: []
---
The goal of this article is to relate several strategies and technologies to improve the efficiency in the collection, analysis and presentation of field data.  I have limited the suggestions to only technologies that are free (but not necessarily open-source) and/or utilize public APIs so as to make them accessible to an audience who constantly finds their budgets diminishing.  However, prior to getting into that, allow me to relate the context of some of these recommendations...

<a id="more"></a><a id="more-3"></a>

On the last leg of summer vacation I recently paid a visit to my brother in Northern Arizona. He doesn't live there, but rather co-habitates with a bunch of other hippies during the course of the summer and has done so for the last 3 consecutive summers. Now don't get the wrong idea, while he is a hippy, this isn't some weirdo commune. Actually, it does resemble one - with it's small town of multi-colored tents and contrasting bandannas.

This is actually a USGS study being conducted in the Coconino National Forest that surrounds Flagstaff. He occupies the rather dubious position as one of the senior researchers on the project. As part of his responsibilities, he's helping 20-some-odd college students through a summer of banding birds, conducting vegitation surveys and manning the Forest Service walkie-talkie for signs of fire danger.

While thoroughly enjoying spending my vacation virtually off-the-grid through a series of hiking, climbing and camping escapades, I couldn't help but fall back into some of my usual thinking regarding workflow, data, networking and interactivity. The event the really drew me back into this line of thinking was when checking in on a nesting site with my brother. Cresting over Rim Road, we encountered a thin plume of smoke not 20 meters from the nesting site. We immediately were struck by a moment of wonder of flames licking upwards, instilling a primal fascination, followed immediately by the more rational, sobering twinge of danger at what we were actually encountering - this being the ultimate in bad news for anyone with a crew in a tinder-dry National Forest.

I recalled my GPS receiver that I had taken to toting around with me to passively record my adventures in the form of GPS coordinates. I marked the coordinates of the fire and wrote them on a scrap of paper, which I then handed to my brother. Picking up the Forest Service radio, he called in the coordinates to the Moqui Fire Lookout in accordance with regulations and what is to be expected from someone who earned their "Red Card" out of a requirement for working in the Alaskan wilderness.

With little else to do other than head back to Bird Camp, as they call it, to make certain that all of the researchers were back from their days, that is exactly what we did. While rolling back in the giant Suburban marked with a University of Montana logo, mostly listening to the Forest Service radio for news of our fire and the 12 others that had been reported thus far that day, my mind wandered considering how else technology could be applied to a traditionally disconnected field.

While I'm not involved in academia, I deal quite a bit with data. As a result, numerous parallels between developing system architectures and conducting scientific studies are immediately striking.  The most notable being, the underlying shared characteristics involving what is essentially the collection, analysis and presentation of data.  From my brief experience in the field with my brother and his colleagues, it became apparent that they still very much have at least one foot strongly set in the punch card era.

First, in looking at how survey plots are defined (although in their defense, this particular study was started 23 years ago), it is clear that this most fundamental layer of data in the form of geographic data is in the form of paper maps.  When one considers that the researches are gathering information on bird populations and the locations of their nests within physical spaces, it should be obvious that the correlation of gathered data to a location is of high importance.  So, let me introduce my first suggestion: a mapping API.

The introduction of Google Maps opened up a great number of possibilities with regard to visualization of data as it relates to physical locations.  One of the earliest (in)famous mash-up applications was the Chicago Crime Map (http://chicagocrime.org).  While perhaps there are examples in academia of this sort of application, the ones that are best known are developed by nerds with an idea to create something new.  However, after several releases of the Google Maps API that made it more-and-more accessible to the average user, development has culminated in the My Maps feature.  The latest iteration that allows users to create and save maps with data overlays without writing a single line of code.

While Google Maps is perhaps more well known than its Yahoo! conterpart, Yahoo! Maps have made great strides with their development and API, surpassing Google's in my opinion.  One of the great features of Yahoo! Maps are the API offerings in not only HTML/CSS/JS version, but also in a Flash versions that include AS2, AS3 and Flex libraries (see FlexQuake for an example).

Regardless of  which one a researcher deems easier or more appropriate to implement, they are both free and provide an excellent starting point for the collection and visualization of data that relates to physical space.

<strong>References:</strong>
<ul>
	<li>http://www.google.com/apis/maps/</li>
	<li>http://developer.yahoo.com/maps/</li>
</ul>
In Part 2, I will investigate additional mapping technologies, data collection and analysis.

---
layout: post
status: publish
published: true
title: Flex 2 and WSDL Overloading
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "On a project that I am currently working on, the team was having some
  issues consuming JBoss SOAP services.  The root of the problem took a while to figure
  out, as apparently there are very few people that try to consume SOAP services experience
  the same issue we were encountering and The Google revealed few clues.  At first
  we thought that perhaps the difference was between WSDL 1.1 and WSDL 2.0 and Flex's
  lack of support for WSDL 2.0, as that is what the SOAP services were generating.
  \ After some initial investigation, we thought we eliminated that as a possibility.
  \ Then we discovered that the WSDL that we were consuming contained overloaded methods.
  \ Some reinvestigation at the W3C was done to see if  perhaps a difference between
  the WSDL 1.1 or 2.0 specifications was support for WSDL overloading.  It turns out
  the the specs are silent on this issue, so again we eliminated the difference in
  WSDL versions.  Some additional searching after that determined that Flex definitely
  lacks support for WSDL overloading.\r\n"
wordpress_id: 29
wordpress_url: http://phy5ics.com/blog/2007/08/21/flex-2-and-wsdl-overloading/
date: 2007-08-21 13:55:11.000000000 -04:00
categories:
- Flex
- Web Services
tags: []
comments: []
---
On a project that I am currently working on, the team was having some issues consuming JBoss SOAP services.  The root of the problem took a while to figure out, as apparently there are very few people that try to consume SOAP services experience the same issue we were encountering and The Google revealed few clues.  At first we thought that perhaps the difference was between WSDL 1.1 and WSDL 2.0 and Flex's lack of support for WSDL 2.0, as that is what the SOAP services were generating.  After some initial investigation, we thought we eliminated that as a possibility.  Then we discovered that the WSDL that we were consuming contained overloaded methods.  Some reinvestigation at the W3C was done to see if  perhaps a difference between the WSDL 1.1 or 2.0 specifications was support for WSDL overloading.  It turns out the the specs are silent on this issue, so again we eliminated the difference in WSDL versions.  Some additional searching after that determined that Flex definitely lacks support for WSDL overloading.
<a id="more"></a><a id="more-29"></a>
In our case, we couldn't change the WSDL or the services themselves to remove the overloaded methods because we had no control over the SOAP services as they were part of a software package produced by an external vendor.  The vendor had upgraded their core APIs from a previous version of their software.  To accommodate backwards compatibility these changes were made without having to modify any of the actual method names by overloading several methods in their API.  The WSDL was then auto-generated from the Java classes that comprise the web services.  While Java conveniently supports methods overloading, despite clamoring for it for the last several releases of ActionScript, we still don't have it natively in either Flex nor ActionScript.  As a result, we needed a workaround.

<strong>The Easy Way</strong>
While not exactly the most ideal, for a short-term hack, we copied the XML in the WSDL that was generated, copied it into a empty file, and removed the offending methods manually.  This was then placed on our servers and called in place of the overloaded WSDL.  While it is not terribly clean nor reliable, as any time the web services change the WSDL is not updated, it happens to work without any server-side modifications.

<strong>The Hard Way</strong>
For the longer-term solution we will be implementing a service proxy in .NET and Windows Communication Foundation (WCF) because it is necessary for future iterations of the project.  A service proxy is an extra layer in an SOA architecture that essentially acts as a broker between web services.  The service proxy in our case accomplishes several things:
<ul>
	<li>Consolidation of multiple web services from multiple vendors into a single public-facing SOAP endpoint that the Flex client can then consume instead of attempting to integrate with them directly</li>
</ul>
<ul>
	<li>Allows for mapping between a single SOAP call into the service proxy by the Flex client to be mapped to multiple web services to be</li>
</ul>
<ul>
	<li>Allows for web service transactions whereby SOAP calls can be rolled back depending upon results from various calls to various external services</li>
</ul>
<ul>
	<li>Gives the ability to implement MSMQ for scalability and reliability, as SOAP messages can then be stored in a queue for later in the case of external services being down or overloaded</li>
</ul>
<ul>
	<li>Best of all, it allows us to author the SOAP API and the WSDL that the Flex client will connect to and removes the issue of attempting to consume an overloaded WSDL from Flex</li>
</ul>

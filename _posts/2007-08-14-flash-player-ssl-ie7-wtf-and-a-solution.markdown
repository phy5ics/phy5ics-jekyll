---
layout: post
status: publish
published: true
title: Flash Player + SSL + IE7 = WTF (and a solution)
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "<strong>Use Case</strong>\r\nI've been working on a project with a
  team of some of our really talented Flash developers (props Ben, Leon and Gabriel)
  where a Flex app being served from a non-secure URL via plain HTTP needs to connect
  to and consume data from another server via HTTPS and have run into some issues
  and a workaround that I'd like to share.  For that particular project, the other
  server is a SOAP service running behind SSL with a Flex app served over HTTP consuming
  those services.  However, these concepts also apply to any external data consumed
  by the Flash Player.  A simplified diagram of the system is below:\r\n\r\n"
wordpress_id: 25
wordpress_url: http://phy5ics.com/blog/2007/08/14/flash-player-ssl-ie7-wtf-and-a-solution/
date: 2007-08-14 17:05:30.000000000 -04:00
categories:
- Flex
- AS3
tags: []
comments:
- id: 834
  author: Internet Explorer &raquo; phy5ics " Blog Archive " Flash Player + SSL +
    IE7 = WTF (and a&#8230;
  author_email: ''
  author_url: http://internet-explorer.blogyblog.info/?p=1060
  date: !binary |-
    MjAwNy0xMi0yNCAwOTo0NToxNSAtMDUwMA==
  date_gmt: !binary |-
    MjAwNy0xMi0yNCAxNzo0NToxNSAtMDUwMA==
  content: ! '[...] Firefox Download Site- Get Mozilla Firefox Free wrote an interesting
    post today on phy5ics &amp;quot; Blog Archive &amp;quot; Flash Player + SSL +
    IE7 = WTF (and a&#8230;Here&#8217;s a quick excerpt&#8230;that will be a pain
    if you test in Firefox and then try to get it to work in any version of Internet
    Explorer, as it will fail silently in IE. [...]'
- id: 835
  author: Internet Explorer &raquo; phy5ics " Blog Archive " Flash Player + SSL +
    IE7 = WTF (and a
  author_email: ''
  author_url: http://internet-explorer.blogyblog.info/?p=1085
  date: !binary |-
    MjAwNy0xMi0yNCAxMTowODo0NiAtMDUwMA==
  date_gmt: !binary |-
    MjAwNy0xMi0yNCAxOTowODo0NiAtMDUwMA==
  content: ! '[...] Firefox Download Site- Get Mozilla Firefox Free wrote an interesting
    post today on phy5ics &amp;quot; Blog Archive &amp;quot; Flash Player + SSL +
    IE7 = WTF (and aHere&#8217;s a quick excerpt&#8230;that will be a pain if you
    test in Firefox and then try to get it to work in any version of Internet Explorer,
    as it will fail silently in IE. [...]'
- id: 838
  author: Thierry
  author_email: thierrybertossa@gmail.com
  author_url: ''
  date: !binary |-
    MjAwNy0xMi0yNiAwODowMzowMiAtMDUwMA==
  date_gmt: !binary |-
    MjAwNy0xMi0yNiAxNjowMzowMiAtMDUwMA==
  content: ! "I have some probleme with a tomcat servlet over https with IE 7, for
    you there is no probleme with the flex streaming class ...\r\nthe probleme come
    from the response header ?"
- id: 1509
  author: ! 'IE7 + SSL + XML? = Flex &#8220;Error #2032: Stream Error&#8221; &laquo;
    I don&#8217;t like computers.'
  author_email: ''
  author_url: http://faindu.wordpress.com/2008/04/18/ie7-ssl-xml-flex-error-2032-stream-error/
  date: !binary |-
    MjAwOC0wNC0xOCAxMDoyMzoyNyAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNC0xOCAxODoyMzoyNyAtMDQwMA==
  content: ! '[...] search could go on. Barton has some nice input and proposes to
    tamper the HTTP header: remove Pragma and set Cache-Control: [...]'
- id: 3998
  author: JeakeloockLal
  author_email: kaziuskiswerkanis@gmail.com
  author_url: http://Website
  date: !binary |-
    MjAxMS0wNC0wMiAwMTo0MDo1OCAtMDQwMA==
  date_gmt: !binary |-
    MjAxMS0wNC0wMiAwOTo0MDo1OCAtMDQwMA==
  content: ! 'Thanks in behalf of you attention, delight pop in our site: http://tlumaczenia.compare.com.pl
    - T&#322;umaczenia przysi&#281;g&#322;e'
---
<strong>Use Case</strong>
I've been working on a project with a team of some of our really talented Flash developers (props Ben, Leon and Gabriel) where a Flex app being served from a non-secure URL via plain HTTP needs to connect to and consume data from another server via HTTPS and have run into some issues and a workaround that I'd like to share.  For that particular project, the other server is a SOAP service running behind SSL with a Flex app served over HTTP consuming those services.  However, these concepts also apply to any external data consumed by the Flash Player.  A simplified diagram of the system is below:

<a id="more"></a><a id="more-25"></a>

<a href="http://phy5ics.com/blog/wp-content/uploads/2007/08/system_architecture.jpg" title="HTTP/HTTPS Architecture Example"><img src="http://phy5ics.com/blog/wp-content/uploads/2007/08/system_architecture.jpg" alt="HTTP/HTTPS Architecture Example" /></a>

Pretty basic use case, right?  Should be pretty straightforward once the usual suspects are addressed as follows, right?  No, of course not, otherwise this article wouldn't actually be helpful.  I'll start with the server environment and SSL certificates.

<strong>SSL Certificates</strong>
On the development boxes that I've been using, self-signed certificates are installed, which means that an SSL certificate is created DIY on the server rather than purchasing one from a certificate authority like Verisign, Thawte, etc.  This is a common practice for development systems, internal systems and others where end-users may not be concerned that the certificate was not issued by a certificate authority.

Because of that, when pointing a browser (in this case Safari, FF or IE6 are the ones that I'm testing against) at for example https://dev.services.com/, a pop-up application window with a security warning appears asking if the certificate should be accepted.  (This is an important point that I'll be coming back to)  Clicking yes acknowledges that you are aware of the security implications of interacting with a server that has one or more of the following characteristics:
<ul>
	<li>The SSL certificate has expired</li>
	<li>The domain of the server does not match the domain of the SSL certificate</li>
	<li>The SSL certificate is not signed by a certificate authority</li>
</ul>
There may be other instances when this security dialog appears, but these are the most common.

<strong>A Special Browser from Special People</strong>
With IE7, the above is almost identical, with one important distinction.  That is that IE7 does not use a different application window to display the security warning.  It redirects to a local page that displays the security warning as the following screen capture illustrates:

<a href="http://phy5ics.com/blog/wp-content/uploads/2007/08/ie7_cert_warning.png" title="IE7 Certificate Warning"><img src="http://phy5ics.com/blog/wp-content/uploads/2007/08/ie7_cert_warning.thumbnail.png" alt="IE7 Certificate Warning" /></a>

As we'll see later, this comes back to bite us in the ass.  However, let's take at all the pieces that need to come together to make this work.

<strong>Crossdomain.xml File</strong>
As with all server-to-server communication, a crossdomain.xml file is required on the https://dev.services.com so that the Flex app on http://dev.application.com can talk to it.  For testing on the development box, the crossdomain.xml as such:

<allow-access-from domain="http://dev.application.com" secure="false"></allow-access-from>

In this case, the secure="false" attribute is allegedly supposed to signal the Flash Player to ignore certificate warnings and allow the loading of content from the secure context.  I have found a wealth of contradictory information on this topic and because it doesn't really seem to be clear, since this is a development server, I'm just going to leave it in there because I know that the certificate does not match the domain and is self-signed.  This attribute should be removed on production servers, as according to <a href="http://kb.adobe.com/selfservice/viewContent.do?externalId=tn_14213&amp;sliceId=1">Adobe</a>, it may compromise security:

"A secure server that allows access to movies hosted via a non-secure protocol
It is not advisable to permit HTTP content to access HTTPS content. This practice can compromise the security offered by HTTPS."

This comment is seemingly contradictory, so I'm not entirely certain that it is true.  I can understand how loading from HTTP into HTTPS is a security issue, but not the other way around.

<strong>HTTP Headers</strong>
So, despite having this configured with secure="false", there is another aspect to this that will be a pain if you test in Firefox and then try to get it to work in any version of Internet Explorer, as it will fail silently in IE.  That is the issue of HTTP headers that are sent by a web server in response to a request from a browser.  In IE, because it is the short bus of browsers, any HTTP responses sent from a secure context to an insecure one are ignored.  I don't know enough about the inner workings of IE to know why, however, it fails silently.

To get around this and allow HTTP responses to be received over SSL from a server, it is necessary to change either configuration at the web server level on https://dev.services.com or set the headers at a code level to ensure that the proper headers are being sent with HTTP responses.  That HTTP header is as follows:

<code>Cache-Control: no-store</code>

There is a great deal of disagreement and contradiction on this topic, as can be seen with nearly every comment related to this <a href="http://www.blog.lessrain.com/?p=276">blog post</a>.  However, according to my testing, and the word of my esteemed colleague, <a href="http://www.flashsupport.com/">Robert Reinhardt</a>, this is the one that indeed works.

<strong>The IE7 Issue</strong>
Now, with all of that set up, it should be possible to load data into the Flex app from the secured domain via HTTPS.  In testing this with Firefox, Safari and IE6, once the crossdomain.xml is requested, a security warning is triggered that then asks the user to accept the certificate for the secure domain that the Flash Player is attempting to communicate with.  If the certificate is accepted, the crossdomain.xml file is loaded and then the Flash Player can access resources on that server.

In attempting this in a server environment where the certificate triggers the certificate security warning, the following following error is thrown (if the debug version is installed or errors are trapped and traced out, otherwise it just fails silently):

<code>[RPC Fault faultString="Security error accessing url" faultCode="Channel.Security.Error" faultDetail="Destination: DefaultHTTP"]</code>

Using a tool like <a href="http://www.blunck.se/iehttpheaders/iehttpheaders.html">IEHTTPHeaders</a> or <a href="http://www.iewatch.com/ieprofessional.aspx">IEWatch Professional</a> and looking at the HTTP headers and what requests are made, it becomes apparent that the crossdomain.xml is not being loaded at all.  It shows its status as "aborted", meaning that IE7 refuses to actually load it.  As a result, this is the reason that the call is failing.  The only ways around this that I have found are:
<ol>
	<li>Navigate to the server that is hosting the crossdomain.xml file manually and accept the certificate then navigate back to the page with the Flash Player and then try to access the other server.</li>
	<li>Make sure that the server that is being connected to does not throw any certificate security warnings in IE7.</li>
</ol>
Hopefully these tips save someone else's time and blood pressure levels, it definitely affected both of mine negatively.

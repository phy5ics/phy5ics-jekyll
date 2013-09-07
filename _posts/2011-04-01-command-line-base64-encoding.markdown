---
layout: post
status: publish
published: true
title: Command Line Base64 Encoding
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
wordpress_id: 95
wordpress_url: http://blog.phy5ics.com/?p=95
date: 2011-04-01 09:07:03.000000000 -04:00
categories:
- Uncategorized
tags: []
comments: []
---
I'm currently authoring an AIR 2.5 application in HTML/CSS/JS and ran into some issues with @font-face embedding where no matter what I did the fonts would not load and render correctly despite trying both TTF and OTF versions. &Acirc;&nbsp;After that, I opted to try base64-encoding of the fonts for inclusion via a data url, since they are now supported in AIR. &Acirc;&nbsp;I'm running on OS X and have openssl installed, so I opted to run the following command, which I've used in the past for generated base64-encoded files for other Webkit-based projects and didn't have any issues:
<p><code>shell# openssl base64 -in UniversLTStd.otf -out Std</code></p>
This produced a proper base64 file that worked perfectly in Safari, but when the same encoded file was inserted into CSS and launched in the AIR runtime, it resulted in the display of the default font.  After ruminating a bit on the issue, I suspected that the line breaks produced by the openssl encoding were the issue, and not feeling particularly like removing line breaks by hand on 709 lines of code, I busted out the following:
<p><code>shell# tr -d '\r\n' < Std > StdNoBreaks</code></p>
I then used the output in the resulting file as the data url and it worked like a charm in the AIR runtime with the following CSS:
<p>
<code>src: url("data:font/opentype;charset=utf-8;base64,[INSERT_BASE64_ENCODED_DATA_HERE]");</code></p>

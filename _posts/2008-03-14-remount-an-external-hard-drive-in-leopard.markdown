---
layout: post
status: publish
published: true
title: Remount an External Hard Drive in Leopard
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "This may seem like a fairly outlandish edge case for external hard drives,
  but it's one that I've run recently.  Suppose you have an external Firewire drive
  connected to your MacBook Pro and then daisy-chained via Firewire to that, you have
  several more Firewire drives.  Then suppose you've accidentally ejected that first
  drive that everything else is daisy-chained to.  Then suppose that you're currently
  in the middle of a render to one of the other down-stream drives and really need
  some files off of the drive that was unmounted.  That removes the possibility of
  physically disconnecting the first drive to then reconnecting it to remount it,
  since the act of disconnecting would fubar the render.\r\n\r\n"
wordpress_id: 42
wordpress_url: http://phy5ics.com/blog/2008/03/14/remount-an-external-hard-drive-in-leopard/
date: 2008-03-14 17:27:14.000000000 -04:00
categories:
- General Technology
- leopard
tags: []
comments: []
---
This may seem like a fairly outlandish edge case for external hard drives, but it's one that I've run recently.  Suppose you have an external Firewire drive connected to your MacBook Pro and then daisy-chained via Firewire to that, you have several more Firewire drives.  Then suppose you've accidentally ejected that first drive that everything else is daisy-chained to.  Then suppose that you're currently in the middle of a render to one of the other down-stream drives and really need some files off of the drive that was unmounted.  That removes the possibility of physically disconnecting the first drive to then reconnecting it to remount it, since the act of disconnecting would fubar the render.

<a id="more"></a><a id="more-42"></a> I know that you're now agreeing that this is a tedious edge case and probably clicking the close button on your browser, but for those that haven't yet, there's an easy answer.  Open up Disk Utility from /Applications/Utilities and select the drive that you unmounted and click "Mount" from the menu.  Problem solved, render complete (hours later).

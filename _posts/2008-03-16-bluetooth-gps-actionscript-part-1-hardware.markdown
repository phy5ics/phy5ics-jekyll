---
layout: post
status: publish
published: true
title: Bluetooth + GPS + ActionScript - Part 1 - Hardware
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "<strong>Overview</strong>\r\nFor this project, my goal was to get
  GPS data into my Mac for some visualization experiments with ActionScript.  After
  some initial prototypes that worked well using an RS232-to-USB converter, I decided
  that wasn't slick enough and had it too many wires.  I like things nice and clean
  around my desk, so I opted for adding Bluetooth in place of a USB converter.\r\n\r\nAfter
  experimenting with some different methods, some using microprocessors and some not,
  I opted for the simpler route, eliminating the microprocessor.  A microprocessor
  doesn't add anything other than cost for the basic purpose of this project.  Although
  stay tuned for another posting about integrating a similar configuration with the
  Make Controller and Arduino microprocessors.\r\n\r\n"
wordpress_id: 43
wordpress_url: http://phy5ics.com/blog/2008/03/16/bluetooth-gps-actionscript-part-1-hardware/
date: 2008-03-16 09:37:19.000000000 -04:00
categories:
- AS3
- GPS
- Physical Computing
- Bluetooth
tags: []
comments:
- id: 1985
  author: grhabyt
  author_email: gwyan.rhabyt@csueastbay.edu
  author_url: http://www.gwyanrhabyt.net
  date: !binary |-
    MjAwOC0wNS0yMiAxMjoyNTozNiAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNS0yMiAyMDoyNTozNiAtMDQwMA==
  content: This sounds great. I'm eagerly awaiting the software side of it. Did you
    use flosc? Is there something better in AS3 to socket it into? I'm still with
    AS2 and can't find anything there barring going via XML or flosc
- id: 2542
  author: Eric
  author_email: eric@ericheaton.com
  author_url: ''
  date: !binary |-
    MjAwOC0wNy0yMiAwNTo1MzowNSAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMiAxMzo1MzowNSAtMDQwMA==
  content: ! "I wonder how long it will take to come out with an iPhone App to connect
    to this for 2G iPhones without GPS\r\n\r\n:-)"
- id: 2544
  author: Envio de dados GPS para seu PC via Bluetooth e ActionScript | Deu Curto!
  author_email: ''
  author_url: http://deucurto.site88.net/blog/?p=45
  date: !binary |-
    MjAwOC0wNy0yMiAwNjowMDoxMiAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMiAxNDowMDoxMiAtMDQwMA==
  content: ! '[...] [Leia mais] [...]'
- id: 2547
  author: Send GPS data to your computer without a microcontroller &raquo; Developages
    - Development and Technology Blog
  author_email: ''
  author_url: http://www.developages.com/send-gps-data-to-your-computer-without-a-microcontroller/37663
  date: !binary |-
    MjAwOC0wNy0yMiAwNjoxMzowOCAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMiAxNDoxMzowOCAtMDQwMA==
  content: ! '[...]  Bluetooth + GPS + ActionScript  [...]'
- id: 2548
  author: ! "&auml;&sup1;&OElig;&aelig;&permil;&tilde;&eacute;&sbquo;&brvbar;|&aelig;&bdquo;&Yuml;&aring;&Scaron;&uml;&auml;&cedil;&shy;&aring;&rsaquo;&frac12;|Keep
    Simple, Make Fun. / &eacute;&tilde;&hellip;&egrave;&macr;&raquo;&aelig;&mdash;&para;&eacute;&mdash;&acute;
    &iuml;&frac14;\x8D 20080722"
  author_email: ''
  author_url: http://www.sinoutopia.org/wp/?p=1300
  date: !binary |-
    MjAwOC0wNy0yMiAwNjo1MzowMCAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMiAxNDo1MzowMCAtMDQwMA==
  content: ! "[...] &egrave;&iquest;&trade;&auml;&sup1;&circ;&aring;&deg;\x8F&ccedil;&scaron;&bdquo;
    GPS &aelig;&uml;&iexcl;&aring;\x9D&mdash;&aring;&dagger;\x8D&aring;&Scaron;&nbsp;&auml;&cedil;&Scaron;&auml;&cedil;&shy;&aring;&rsaquo;&frac12;&ccedil;&rdquo;&micro;&auml;&iquest;&iexcl;&eacute;&hellip;\x9D&eacute;&hellip;&iquest;&aelig;Ž&uml;Wi-Fi&aelig;&permil;&lsaquo;&aelig;&OElig;\x81&ccedil;&raquo;&circ;&ccedil;&laquo;&macr;&egrave;&iquest;&trade;&aelig;\x9D&iexcl;&aelig;&para;&circ;&aelig;\x81&macr;&atilde;&euro;&sbquo;&ccedil;&oelig;&Yuml;&ccedil;&scaron;&bdquo;&aring;&euro;&frac14;&aring;&frac34;&mdash;&aelig;&oelig;&Yuml;&aring;&frac34;&hellip;&aring;&bull;&Scaron;&iuml;&frac12;ž&iuml;&frac12;ž
    &auml;&cedil;\x8D&egrave;&iquest;&Dagger;&ccedil;Ž&deg;&aring;&oelig;&uml;&ccedil;&rdquo;&micro;&aring;&Scaron;&rsaquo;&aelig;&ndash;&sup1;&eacute;\x9D&cent;&eacute;&mdash;&reg;&eacute;&cent;&tilde;&ccedil;&scaron;&bdquo;&ccedil;&iexcl;&reg;&egrave;&iquest;&tilde;&aelig;&sup2;&iexcl;&aelig;&oelig;&permil;&aring;&reg;&OElig;&aring;&hellip;&uml;&aring;&Dagger;&dagger;&aring;&curren;&Dagger;&aring;&yen;&frac12;&iuml;&frac14;&OElig;&aelig;&permil;&lsaquo;&aelig;&OElig;\x81&egrave;&reg;&frac34;&aring;&curren;&Dagger;&ccedil;&scaron;&bdquo;&ccedil;&mdash;&rsaquo;&aring;&bull;&Scaron;&iuml;&frac12;ž
    [...]"
- id: 2549
  author: Tam
  author_email: asdf@asdf.com
  author_url: ''
  date: !binary |-
    MjAwOC0wNy0yMiAwNzowMDowNiAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMiAxNTowMDowNiAtMDQwMA==
  content: ! "Uh. On that little diagram that you made, is the BlueSMiRF connected
    right?\r\n\r\nIs the VCC+ AND the GND of the BlueSMiRF Supposed to both be connected
    to the VCC+ of the power supply? Cause that makes less than no sense to me. Was
    it supposed to be connected in parallel instead?"
- id: 2550
  author: Siftah
  author_email: John@siftah.com
  author_url: http://www.siftah.com
  date: !binary |-
    MjAwOC0wNy0yMiAwNzowNjozNCAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMiAxNTowNjozNCAtMDQwMA==
  content: ! "I'm a bit confused - have you not just replicated the functionality
    of a $40 Bluetooth GPS module (with a built in battery and charging circuit) by
    using two $60 sparkfun modules that still need external power?\r\n\r\nInterested
    question rather than a criticism! :)"
- id: 2556
  author: David
  author_email: david@fastolfe.net
  author_url: http://fastolfe.net/
  date: !binary |-
    MjAwOC0wNy0yMiAxMzowMToyNSAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMiAyMTowMToyNSAtMDQwMA==
  content: Did you really connect GND and VCC+ together on the BlueSMiRF?
- id: 2563
  author: Arto
  author_email: arto.salminen@luukku.com
  author_url: ''
  date: !binary |-
    MjAwOC0wNy0yMiAyMjozMDo1MyAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMyAwNjozMDo1MyAtMDQwMA==
  content: Nice project. But it would be cheaper to buy a ready-made commercial Bluetooth
    GPS. Usually those things have internal batteries with a charging circuit. And
    they come in very compact housing.
- id: 2564
  author: Snoopy
  author_email: bill34@freemail.hu
  author_url: ''
  date: !binary |-
    MjAwOC0wNy0yMiAyMzoxMzo1NCAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMyAwNzoxMzo1NCAtMDQwMA==
  content: ! "Nice stuff!\r\nPlease, correct the schematic on wiring BT module because
    you have short circuit between gnd and vcc+ :)"
- id: 2568
  author: GB Vehicles Info &raquo; Blog Archive &raquo; Send GPS data to your computer
    without a microcontroller
  author_email: ''
  author_url: http://www.gbvinfo.com/?p=47
  date: !binary |-
    MjAwOC0wNy0yMyAwMjowNTo1NCAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yMyAxMDowNTo1NCAtMDQwMA==
  content: ! '[...]  Bluetooth + GPS + ActionScript , GPS Parser [...]'
- id: 2600
  author: phy5ics &raquo; Blog Archive &raquo; Thanks for all the Fish
  author_email: ''
  author_url: http://phy5ics.com/blog/2008/07/24/thanks-for-all-the-fish/
  date: !binary |-
    MjAwOC0wNy0yNCAxODoxNjo0MiAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yNSAwMjoxNjo0MiAtMDQwMA==
  content: ! '[...] greatly appreciate everyone&#8217;s comments and input on my article
    on Bluetooth and GPS  .&Acirc;&nbsp; It is quite nice to have the exposure from
    Make and also to have one&#8217;s efforts peer [...]'
- id: 2601
  author: Barton
  author_email: jb@phy5ics.com
  author_url: http://phy5ics.com
  date: !binary |-
    MjAwOC0wNy0yNCAxODoxNjo1OCAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yNSAwMjoxNjo1OCAtMDQwMA==
  content: ! 'Thanks for all the comments.  I parlayed them into another article:
    http://phy5ics.com/blog/2008/07/24/thanks-for-all-the-fish/'
- id: 2609
  author: Electronics-Lab.com Blog &raquo; Blog Archive &raquo; Send GPS data to your
    computer without a microcontroller
  author_email: ''
  author_url: http://www.electronics-lab.com/blog/?p=2277
  date: !binary |-
    MjAwOC0wNy0yNSAwOToyODowMiAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0yNSAxNzoyODowMiAtMDQwMA==
  content: ! '[...] Send GPS data to your computer without a microcontroller - [Link]
    [...]'
- id: 2675
  author: The Three Mighty Combo &acirc;&euro;&ldquo; Bluetooth, GPS and Action Script
    - CircuitGeek
  author_email: ''
  author_url: http://www.circuitgeek.com/the-three-mighty-combo-bluetooth-gps-and-action-script/
  date: !binary |-
    MjAwOC0wNy0zMSAxMToyNDo1MSAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wNy0zMSAxOToyNDo1MSAtMDQwMA==
  content: ! '[...] That&#8217;s all, guys and do enjoys yourself! [link] [...]'
- id: 2995
  author: ! '. [ Z o o B a B ] .: Good Designs'
  author_email: ''
  author_url: http://zoobab.wikidot.com/designs
  date: !binary |-
    MjAwOC0wOC0yOCAwMTozMzozMSAtMDQwMA==
  date_gmt: !binary |-
    MjAwOC0wOC0yOCAwOTozMzozMSAtMDQwMA==
  content: ! '[...] http://phy5ics.com/blog/2008/03/16/bluetooth-gps-actionscript-part-1-hardware/#more-43
    [...]'
- id: 3880
  author: Barton
  author_email: jb@phy5ics.com
  author_url: http://phy5ics.com
  date: !binary |-
    MjAwOC0xMS0wNiAxNzoyMjo1NSAtMDUwMA==
  date_gmt: !binary |-
    MjAwOC0xMS0wNyAwMToyMjo1NSAtMDUwMA==
  content: I finally got around to making some updates - namely the schematic with
    the short in it and adding a missing top-down photo.
- id: 3904
  author: Illusion
  author_email: mea06ma@shef.ac.uk
  author_url: http://Website
  date: !binary |-
    MjAwOC0xMS0xNSAwODoxMjowMiAtMDUwMA==
  date_gmt: !binary |-
    MjAwOC0xMS0xNSAxNjoxMjowMiAtMDUwMA==
  content: ! "Hi m8,\r\n\r\nNice stuff.\r\n\r\nI am also using this module in a different
    manner and was therefore wondering, what is the functionality of 1 pulse per second
    pin in EM406-A.\r\n\r\nAlthough, I am already getting my stuff working, but do
    you know exactly what is this pps pin for?\r\n\r\nHope to hear from you soon."
- id: 3912
  author: Barton
  author_email: jb@phy5ics.com
  author_url: http://phy5ics.com
  date: !binary |-
    MjAwOC0xMS0xNyAxNDozMTo0NCAtMDUwMA==
  date_gmt: !binary |-
    MjAwOC0xMS0xNyAyMjozMTo0NCAtMDUwMA==
  content: The 1PPS pin is synchronized with the GPS time that is received.  As for
    a use, by monitoring output on that pin, you can determine whether or not the
    board has a GPS fix (i.e. there will not be one pulse-per-second if there is not
    a GPS fix, as there is no GPS time available).  In other words, this enables you
    to create an application that does not have to monitor and parse serial output
    to determine if there is a fix or not.
- id: 3958
  author: Clay
  author_email: GrahamC@my.hiram.edu
  author_url: http://Website
  date: !binary |-
    MjAwOS0wOC0yNyAxODozNjowMiAtMDQwMA==
  date_gmt: !binary |-
    MjAwOS0wOC0yOCAwMjozNjowMiAtMDQwMA==
  content: ! "Hi John,\r\n\r\nI'm not sure if this site is defunct, but if not would
    you mind posting or sending the schematic to my email. I am trying to do some
    work with birds for tracking their location and I would like to see the layout
    of the design.\r\n\r\nthanks,\r\nClay"
- id: 3999
  author: atrolveEssell
  author_email: bijonce6@go2.pl
  author_url: http://Website
  date: !binary |-
    MjAxMS0wNC0wOSAwMDoxNjozOCAtMDQwMA==
  date_gmt: !binary |-
    MjAxMS0wNC0wOSAwODoxNjozOCAtMDQwMA==
  content: ! "It absolutely agree with the previous phrase    \r\n<a href=\"http://www.fotograffo.pl\"
    rel=\"nofollow\">fotografia &#347;lubna </a>"
---
<strong>Overview</strong>
For this project, my goal was to get GPS data into my Mac for some visualization experiments with ActionScript.  After some initial prototypes that worked well using an RS232-to-USB converter, I decided that wasn't slick enough and had it too many wires.  I like things nice and clean around my desk, so I opted for adding Bluetooth in place of a USB converter.

After experimenting with some different methods, some using microprocessors and some not, I opted for the simpler route, eliminating the microprocessor.  A microprocessor doesn't add anything other than cost for the basic purpose of this project.  Although stay tuned for another posting about integrating a similar configuration with the Make Controller and Arduino microprocessors.

<a id="more"></a><a id="more-43"></a>
<strong>Parts List</strong>
<ul>
	<li> <a href="http://www.sparkfun.com/commerce/product_info.php?products_id=114" target="_blank">5V regulated power supply</a></li>
	<li> <a href="http://www.sparkfun.com/commerce/product_info.php?products_id=158" target="_blank">BlueSMiRF Bluetooth Module</a></li>
	<li> <a href="http://www.sparkfun.com/commerce/product_info.php?products_id=465" target="_blank">EM406A GPS Module</a></li>
	<li> Extra 6-pin interface cable</li>
	<li> 9V battery holder</li>
	<li> Headers</li>
	<li> Breadboard</li>
	<li> Solid 22-gauge wire</li>
	<li> Soldering iron</li>
</ul>
<strong>5v Power Supply</strong>
Select a 5V power supply to use.  In this case, I'm using a switchable 3.3V/5V power supply kit that I picked up from SparkFun.  I made a slight modification to it and soldered a 9V battery adaptor to it to make it a bit more flexible and truly wireless rather than using the standard 9V DC wall adaptor.  This is just my preference for prototyping.  When I get down to a final design, I generally switch it up in favor of a simple voltage regulator to save space and weight.

<strong>BlueSMiRF Embedded Bluetooth Serial RF Link</strong>
The BlueSMiRF module is sweet little device, providing an easy way to link any project using a serial interface to a computer (or another BlueSMiRF module).  Simply connect the TX, RX to another serial device along with vcc (4.5V-5.5V) and ground and it is ready to pair.

<strong>EM406A GPS Board</strong>
This small board uses the SiRF Star III chipset, which is a nice chipset that is relatively stingy on power supply and can fix its position - known as TTFF (Time To First Fix), even in indoor environments, in a matter of 30 seconds or so.  Just keep in mind that the odd peach-colored ceramic part is the antenna and should point towards the sky.   Many other chipsets offer significantly less in terms of performance and most are unable to fix a position unless outside.  I was sold on it since happens to be the same chipset that I have in my Garmin CS60x, a considerably more expensive device.

Besides all that, the EM406A is a perfect candidate for integration with physical computing projects because it's output is serial.  It starts outputting NMEA strings at 4800 baud once its position is fixed.  NMEA 0183 is a standard with which GPS data is transmitted from a device using comma-delimited strings.  For more information on NMEA, consult <a href="http://www.gpsinformation.org/dale/nmea.htm" target="_blank">this resource</a>.

The documentation for the board itself is well done.  In addition to the NMEA strings that are broadcast from the board itself, the EM406A can have commands sent to it via its serial interface to get specific NMEA data back.&Acirc;&nbsp; The only catch is be sure to get an 6-pin extra interface cable along with the board itself.&Acirc;&nbsp; I cut the interface cable in half and then soldered the wires some headers to make prototyping easier.  Otherwise it's going to be impossible to do anything useful with it.

<strong>Schematic</strong>
Now that we have all that down, here's a little schematic of how everything is hooked up together:

<a href="http://phy5ics.com/blog/wp-content/uploads/2008/11/gps_bt_schematic_rev1.jpg"><img class="alignnone size-full wp-image-54" title="gps_bt_schematic_rev1" src="http://phy5ics.com/blog/wp-content/uploads/2008/11/gps_bt_schematic_rev1.jpg" /></a>

<strong>Photograph</strong>

<a href="http://phy5ics.com/blog/wp-content/uploads/2008/11/gps_bt_2.jpg"><img class="alignnone size-full wp-image-56" title="gps_bt_2" src="http://phy5ics.com/blog/wp-content/uploads/2008/11/gps_bt_2.jpg" /></a>
<strong>Next Article</strong>
In the next post, I'll be working through the software aspects of this project.

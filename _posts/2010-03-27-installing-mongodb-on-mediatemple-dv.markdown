---
layout: post
status: publish
published: true
title: Installing MongoDB on MediaTemple (dv)
author: Barton
author_login: admin
author_email: jb@phy5ics.com
author_url: http://phy5ics.com
excerpt: ! "<p>Due to a project that  I've been working on that has some very specific
  software requirements  I consolidated several separate boxes (from Joyent and MediaTemple's
  Grid Service) to a new (dv) from  MediaTemple for more flexibility.&Acirc;&nbsp;
  As part of that migration, I needed to get MongoDB setup on CentOS.&Acirc;&nbsp;
  The only RPM out there is for MongoDB is 1.2.2, (available here: http://chrislea.com/2010/02/07/mongodb-1-2-2-for-centos-5/).&Acirc;&nbsp;
  However, I quickly found out that with MT's (dv), there are all sorts of depsolving
  issues with the Plesk psa packages and boost.&Acirc;&nbsp; So after all sorts of
  hell with yum, I decided to give the pre-compiled binaries a shot, and much to my
  dismay, they worked a treat with no fussing. I ran into further issues with installing
  the MongoDB PHP extension via pecl, but figured out how to work around those as
  well.  In an effort to help out those that might run into this as well, here are
  instructions on how to get it running on an MT (dv).</p>\r\n<p style=\"font-size:
  19.5px; line-height: 28.5px;\">"
wordpress_id: 73
wordpress_url: http://blog.phy5ics.com/?p=73
date: 2010-03-27 16:43:42.000000000 -04:00
categories:
- mongodb
tags:
- mongodb
- mediatemple
- hosting
comments: []
---
<p>Due to a project that  I've been working on that has some very specific software requirements  I consolidated several separate boxes (from Joyent and MediaTemple's Grid Service) to a new (dv) from  MediaTemple for more flexibility.&Acirc;&nbsp; As part of that migration, I needed to get MongoDB setup on CentOS.&Acirc;&nbsp; The only RPM out there is for MongoDB is 1.2.2, (available here: http://chrislea.com/2010/02/07/mongodb-1-2-2-for-centos-5/).&Acirc;&nbsp; However, I quickly found out that with MT's (dv), there are all sorts of depsolving issues with the Plesk psa packages and boost.&Acirc;&nbsp; So after all sorts of hell with yum, I decided to give the pre-compiled binaries a shot, and much to my dismay, they worked a treat with no fussing. I ran into further issues with installing the MongoDB PHP extension via pecl, but figured out how to work around those as well.  In an effort to help out those that might run into this as well, here are instructions on how to get it running on an MT (dv).</p>
<p style="font-size: 19.5px; line-height: 28.5px;"><a id="more"></a><a id="more-73"></a></p>

<strong>Here is the dependency hell that I ran into after adding the repository:</strong>
<pre># yum install --enablerepo=chl mongo-server mongo
Loaded plugins: fastestmirror, protectbase
Loading mirror speeds from cached hostfile
 * addons: mirror.trouble-free.net
 * atomic: www4.atomicorp.com
 * base: mirror.rackspace.com
 * epel: serverbeach1.fedoraproject.org
 * extras: mirrors.unbornmedia.com
 * rpmforge: apt.sw.be
 * updates: updates.interworx.info
0 packages excluded due to repository protections
Setting up Install Process
Resolving Dependencies
--> Running transaction check
---> Package mongo.i386 0:1.2.2-mongodb_2 set to be updated
--> Processing Dependency: boost >= 1.35 for package: mongo
--> Processing Dependency: libboost_program_options-mt.so.4 for package: mongo
--> Processing Dependency: libboost_filesystem-mt.so.4 for package: mongo
--> Processing Dependency: libjs.so.1 for package: mongo
--> Processing Dependency: libboost_thread-mt.so.4 for package: mongo
--> Processing Dependency: libboost_system-mt.so.4 for package: mongo
---> Package mongo-server.i386 0:1.2.2-mongodb_2 set to be updated
--> Running transaction check
--> Processing Dependency: libboost_date_time.so.2 for package: psa
--> Processing Dependency: libboost_filesystem.so.2 for package: psa
---> Package boost.i386 0:1.37.0-6 set to be updated
---> Package js.i386 1:1.7.0-1.el5.rf set to be updated
--> Finished Dependency Resolution
psa-8.6.0-cos5.build86080722.00.i586 from installed has depsolving problems
  --> Missing Dependency: libboost_filesystem.so.2 is needed by package 
psa-8.6.0-cos5.build86080722.00.i586 (installed)
psa-8.6.0-cos5.build86080722.00.i586 from installed has depsolving problems
  --> Missing Dependency: libboost_date_time.so.2 is needed by package 
psa-8.6.0-cos5.build86080722.00.i586 (installed)
Error: Missing Dependency: libboost_date_time.so.2 is needed by package 
psa-8.6.0-cos5.build86080722.00.i586 (installed)
Error: Missing Dependency: libboost_filesystem.so.2 is needed by package 
psa-8.6.0-cos5.build86080722.00.i586 (installed)
 You could try using --skip-broken to work around the problem
 You could try running: package-cleanup --problems
                        package-cleanup --dupes
                        rpm -Va --nofiles --nodigest
The program package-cleanup is found in the yum-utils package.</pre>

<strong>Installing MongoDB from Pre-Compiled Binaries</strong>
<p>Log in to your (dv) and su to root and get to work:</p>
<pre>
[user@hostname]# su root
[root@hostname]# cd /var/lib
[root@hostname]# wget http://downloads.mongodb.org/linux/mongodb-linux-i686-1.4.0.tgz
[root@hostname]# tar -xvf mongodb-linux-i686-1.4.0.tgz
</pre>

<p>From there, you'll want to create the directories for the database:</p>

<pre>
[root@hostname]# mkdir /data
[root@hostname]# mkdir /data/db
</pre>

<p>That's all there is to it.  You can test your install by doing the following:</p>

<pre>
[root@hostname]# ./mongod
./mongod --help for help and startup options
Sat Mar 27 09:59:16 Mongo DB : starting : pid = 24197 port = 27017 dbpath = /data/db/ master = 0 slave = 0  32-bit 

** NOTE: when using MongoDB 32 bit, you are limited to about 2 gigabytes of data
**       see http://blog.mongodb.org/post/137788967/32-bit-limitations for more

Sat Mar 27 09:59:16 db version v1.4.0, pdfile version 4.5
Sat Mar 27 09:59:16 git version: 514f8bbab657c1dc110d45eea6ea33de296dbb26
Sat Mar 27 09:59:16 sys info: Linux domU-12-31-39-01-70-B4 2.6.21.7-2.fc8xen #1 SMP Fri Feb 15 12:39:36 EST 2008 i686 BOOST_LIB_VERSION=1_37
Sat Mar 27 09:59:16 waiting for connections on port 27017
Sat Mar 27 09:59:16 web admin interface listening on port 28017
</pre>

<strong>Installing MongoDB Driver for PHP</strong>
<p>Here is what I ran into at first:</p>
<pre>
[root@hostname]# cd /var/tmp
[root@hostname]# pecl install mongo
downloading mongo-1.0.6.tgz ...
Starting to download mongo-1.0.6.tgz (53,175 bytes)
.............done: 53,175 bytes
16 source files, building
running: phpize
Configuring for:
PHP Api Version:         20041225
Zend Module Api No:      20060613
Zend Extension Api No:   220060519
building in /var/tmp/pear-build-phy5ics/mongo-1.0.6
running: /var/cache/php-pear/mongo-1.0.6/configure
checking for egrep... grep -E
checking for a sed that does not truncate output... //bin/sed
checking for gcc... gcc
checking for C compiler default output file name... a.out
checking whether the C compiler works... configure: error: cannot run C compiled programs.
If you meant to cross compile, use `--host'.
See `config.log' for more details.
ERROR: `/var/cache/php-pear/mongo-1.0.6/configure' failed
</pre>

<p>Looking at this, I realized that /var/tmp wasn't mounted to allow execution.  That was easy enough to fix after figuring out what it was.  The key is to remount /var/tmp to allow execution:</p>
<pre>
mount -o,remount,rw,exec /var/tmp
</pre>

<p>Once you do that, then you can just run the pecl install command and everything works fine:</p>

<pre>[root@hostname]# pecl install mongo</pre>

<p><i>Important:</i> Don't forget to change it back once you've done your business:</p>
<pre>
mount -o,remount,rw,noexec /var/tmp
</pre>


---
layout: post
title: Hack your wrist
tags: asteroidos,zenwatch,zw2
category: blog
permalink: /blog/hack-your-wrist/
author: sachin
comments: true
---

[AsteroidOS](https://asteroidos.org/) is an open-source operating
system for smartwatches. It's based on Qt & QML with OpenEmbedded
GNU/Linux distribution.

<p align="center">
<img src="{{ site.baseurl }}/images/asteroidos/cropped-logo-tourne.png"
	alt="AsteroidOS logo"
	width=""
	height="300">
</p>


Eventually I was able to run AsteroidOS on
my
[ZenWatch2](https://www.asus.com/in/ZenWatch/ASUS_ZenWatch_2_WI501Q/).
It has been an amazing experience to run GNU/Linux distribution on a
watch. The user-interface is smooth and covers most features that are
needed for a smart-watch.

<p align="center">
<img src="{{ site.baseurl }}/images/asteroidos/drawer20.png"
	alt="Drawer"
	width=""
	height="500">
	<br/>
	<b>Quick settings with Brightness, Bluetooth & Sound control</b>
</p>


### Community

Since few days I was planning to install AsteroidOS. My initial
attempts failed with my watch refused to boot up with AsteroidOS. This
is when I figured out that `initramfs` is not able to find
`/sdcard/linux/rootfs.ext2` on Zenwatch-2 HyperCharge model(WI501Q).
This was brought up by `bencord0`
on [#asteroid channel](https://asteroidos.org/irc-channel/)

	psachin	bencord0: All the files are downloaded from official page and are intact
	psachin	bencord0: Do you want to look at the output of above command?
	bencord0	Sure
	psachin	bencord0: < waiting for any device >
	psachin	downloading 'boot.img'...
	psachin	OKAY [  0.336s]
	psachin	booting...
	psachin	OKAY [  0.506s]
	psachin	finished. total time: 0.842s
	psachin	bencord0: Nothing unusual
	bencord0	The initramfs will reboot back to android it it cant find the rootfs
	bencord0	Did you adb push the rootfs to /sdcard/linux/rootfs.ext2 ?
	psachin	bencord0: Yes. adb push -p asteroid-image-sparrow.ext2 /sdcard/linux/rootfs.ext2
	psachin	[100%] /sdcard/linux/rootfs.ext2

I tried to compile few builds to verify this using `bencord0`
suggestions

	bencord0	https://github.com/AsteroidOS/meta-sparrow-hybris/blob/master/recipes-core/initrdscripts/initramfs-boot-android/init.sh is the init script in the initramfs. Stick an infinite loop near the top, run the build and boot that. If it stays blank, then we will have learned something.

which yield similar results and failed to boot AsteroidOS

	psachin	bencord0: even with infinite loop it booted with android-wear

I also tried few AOSP branch which gave same results

	psachin	kido: Didn't get you. What branch? android-msm-sparrow-3.10-marshmallow-mr1-wear-release? with commit: 8ffc85d0e5dba485a52a4405a21d3a516f969420. Do you want me to test the patch manually?
	@kido	this branch is marshmallow, maybe there is a newer branch for lollypop or whatever


I waited for few weeks and
saw
[new commit](https://github.com/AsteroidOS/meta-sparrow-hybris/commit/d1c95c8c508b69f01fa957b427d430b9e892f94f) by
Florent which I decided to try. I pulled and compiled latest changes
which worked.


### User Interface

Asteroid has sufficient features to get started. The UI is smooth and
can be tweaked as per need. Within settings it has Time, Date,
Language, Bluetooth, Brightness, Wallpaper, Watchface, USB, Poweroff,
Reboot & About options.

<p align="center">
<img src="{{ site.baseurl }}/images/asteroidos/settings10.png"
	alt="Settings"
	width=""
	height="392">
	<br/>
	<b>Settings</b>
</p>

I personally find adjusting date/time much more convenient that
Android Wear.

<p align="center">
<img src="{{ site.baseurl }}/images/asteroidos/date20.png"
	alt="Set date"
	width=""
	height="470">
	<br/>
	<b>Settings date</b>
</p>

User has option to set USB mode to adb, Developer, Mass storage or MTP
mode.

<p align="center">
<img src="{{ site.baseurl }}/images/asteroidos/adb20.png"
	alt="ADB mode"
	width=""
	height="470">
	<br/>
	<b>USB mode</b>
</p>


Using app switcher, one can switch between recently opened apps easily.

<p align="center">
<img src="{{ site.baseurl }}/images/asteroidos/apps20.png"
	alt="Opened apps"
	width=""
	height="470">
	<br/>
	<b>App switcher</b>
</p>

AsteroidOS has few Watchface but they match Asteroid theme and I find
them sober.

<p align="center">
<img src="{{ site.baseurl }}/images/asteroidos/watchface20.png"
	alt="Default Watchface"
	width=""
	height="470">
	<br/>
	<b>Default Asteroid Watchface</b>
</p>


Finally it has wallpapers which can be applied over a Watchface.

<p align="center">
<img src="{{ site.baseurl }}/images/asteroidos/wallpaper20.png"
	alt="Wallpaper"
	width=""
	height="470">
	<br/>
	<b>Watchface</b>
</p>


### Install AsteroidOS

AsteroidOS Alpha 1.0 can
be [installed](https://asteroidos.org/install/) on four smartwatches

- LG G Watch(dory)
- LG G Watch Urbane(bass)
- Sony Smartwatch 3(tetra)
- Asus Zenwatch 2(sparrow)

### Build AsteroidOS

One can build AsteroidOS
following
[wiki page](https://asteroidos.org/wiki/building-asteroidos/). On
Fedora-25, one need to install following dependencies

	# dnf install -y git perl-bignum git patch chrpath gawk diffstat texinfo libaccounts-glib libaccounts-glib-devel
	# dnf groupinstall -y "C Development Tools and Libraries"


#### Unofficial build

- Asus
  ZenWatch2:
  [asteriodOS-alpha-1.0](https://mega.nz/#F!DshE3DKY!4cX_nQ2iSo3sMkZ3TXLvQA)(_Compiled
  on: Feb 18, 2017_):



AsteroidOS unlocks new doors for Smartwatch Operating system with
end-users no longer have to only depend on Android Wear. AsteroidOS
community is very active and responsive. I encourage users to try out
AsteroidOS on smartwatch and give feedback to AsteroidOS community.



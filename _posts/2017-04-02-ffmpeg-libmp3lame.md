---
layout: post
title: ffmpeg with libmp3lame encoder support
tags: ffmpeg, libmp3lame
category: blog
permalink: /blog/ffmpeg-libmp3lame/
author: sachin
comments: true
---

Manually installing `ffmpeg` with `libmp3lame` encoder support.

### Install lame encoder

Download and extract lame from [https://sourceforge.net/projects/lame](https://sourceforge.net/projects/lame/?source=typ_redirect)

{% highlight bash linenos %}
cd lame-*
make
sudo make install
{% endhighlight %}

### Clone and install ffmpeg

{% highlight bash linenos %}
git clone https://git.ffmpeg.org/ffmpeg.git
./configure --enable-libmp3lame
make
sudo make install
{% endhighlight %}


---
layout: post
title: Handy commands
tags: gs, ssh, wget, import, mplayer, ffmpeg, convert
category: blog
permalink: /blog/handy-commands/
author: sachin
comments: true
---

List of commands for day-to-day use

(*Updated on Mar 04, 2017*)

## SOCKS proxy using SSH

{% highlight bash linenos %}
ssh -N -D 1080 user@server
{% endhighlight %}

*where*
{% highlight bash %}
# -N: Do not execute remote commands.
# -D: [bind address:]port. Port in above example.
{% endhighlight %}


## `wget` a website

{% highlight bash linenos %}
wget -rkp -l5 -np -nH -cut-dirs=1 https://example.com
{% endhighlight %}

*where*
{% highlight bash %}
# -rkp: recursive, make link suitable for local viewing, download all files needed to properly view the page.
# -l5: recursively download 5 links away form the original page.
# -n: retrieve files below parent directory.
# -H: Span across hosts when doing recursive retrieving.
{% endhighlight %}


## Capture screenshot

{% highlight bash linenos %}
import -window root screenshot.png
{% endhighlight %}


## Reduce PDF size
{% highlight bash linenos %}
gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -sOutputFile=new_file.pdf original_file.pdf
{% endhighlight %}


## Unlock PDF file
{% highlight bash linenos %}
gs -q -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile=unencrypted.pdf -c .setpdfwrite -f encrypted.pdf
{% endhighlight %}


## Rotate video
{% highlight bash linenos %}
# Using mplayer(watch rotated video)
mplayer -vf-add rotate=1 sample.mp4

# Using ffmpeg
ffmpeg -i infile.mp4 -strict -2 -vf "transpose=1" outfile.mp4
{% endhighlight %}


## Convert 3GP to MP4
{% highlight bash linenos %}
ffmpeg -i VID_0050.3gp -strict -2 -q:a 0 -ab 64k -ar 44100 VID_0050.mp4
{% endhighlight %}


## FLV to MP4

{% highlight bash linenos %}
ffmpeg -i input.flv -qscale 1 -ar 22050 output.mp4
{% endhighlight %}


## Extract audio(MP3) from MP4 video

{% highlight bash linenos %}
ffmpeg -i video.mp4 -f mp3 -ab 192000 -vn music.mp3

# or specify codec to use `libmp3lame` in this case.
ffmpeg -i video.mp4 -f mp3 -codec:a libmp3lame -ab 320000 -vn music.mp3
{% endhighlight %}

*where*
{% highlight bash %}
# -i: input file
# -f mp3: file format should be MP3
# -ab 192000: audio should be encoded at 192Kbps. 320000 for 320Kbps
# -vn: don't want video
{% endhighlight %}


## Cut video by time interval

  *Cut video starting from 19 min 49 seconds up to 04 mins 18 seconds.*

{% highlight bash linenos %}
ffmpeg -y -i Video.mp4 -qscale 1 -ss 00:19:49.0 -t 00:04:18.0 -acodec copy -vcodec copy output.mp4
{% endhighlight %}

  _Note_: `-sameq` was removed in recent version of `ffmpeg`


## Use `mplayer` to extract audio(MP3)

{% highlight bash linenos %}
mplayer -dumpaudio movie.flv -dumpfile movie_audio_track.mp3
{% endhighlight %}


## Reduce resolution

{% highlight bash linenos %}
ffmpeg -i Birdman.mp4 -strict -2  -s 720x480 birdman.mp4
{% endhighlight %}


## recordmydesktop

{% highlight bash linenos %}
recordmydesktop -x 100 -y 100 --width 1280 --height 720 --freq 48000 --fps 30 -o ~/Videos/recordings/test-video.ogv
{% endhighlight %}


## Include subtitles(Use `subtitleeditor` to create subtitle)

{% highlight bash linenos %}
ffmpeg -i video.avi -vf subtitles=subtitle.srt out.avi
{% endhighlight %}


## Resize image 50% of its original size

{% highlight bash linenos %}
convert dragon.gif -resize 50% half_dragon.gif
{% endhighlight %}


## Control compression level of an image

{% highlight bash linenos %}
convert input.png -quality 75 output.jpg
{% endhighlight %}

## Clean up `~/.ccache/` directory

{% highlight bash linenos %}
# View statistics using
ccache -s

# Clear cache using
ccache -C
{% endhighlight %}

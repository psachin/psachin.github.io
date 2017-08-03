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

#### Generic

* SOCKS proxy using SSH

  ```
  ssh -N -D 1080 user@server
  ```

  `-N`: *Do not execute remote commands.*

  `-D`: *[bind address:]port. Port in above example.*


* `wget` a website

  ```
  wget -rkp -l5 -np -nH -cut-dirs=1 https://example.com
  ```

  `-rkp`: *recursive, make link suitable for local viewing, download
all files needed to properly view the page.*

  `-l5`: *recursively download 5 links away form the original page.*

  `-n`: *retrieve files below parent directory.*

  `-H`: *Span across hosts when doing recursive retrieving.*

* Capture screenshot

  ```
  import -window root screenshot.png
  ```

#### PDF

* Reduce PDF size

  ```
  gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -sOutputFile=new_file.pdf original_file.pdf
  ```

* Unlock PDF file

  ```
  gs -q -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile=unencrypted.pdf -c .setpdfwrite -f encrypted.pdf
  ```

#### Audio/Video

* Rotate video

  ```
  # Using mplayer(watch rotated video)
  mplayer -vf-add rotate=1 sample.mp4

  # Using ffmpeg
  ffmpeg -i infile.mp4 -strict -2 -vf "transpose=1" outfile.mp4
  ```

* Convert 3GP to MP4

  ```
  ffmpeg -i VID_0050.3gp -strict -2 -q:a 0 -ab 64k -ar 44100 VID_0050.mp4
  ```

* FLV to MP4

  ```
  ffmpeg -i input.flv -qscale 1 -ar 22050 output.mp4
  ```

* Extract audio(MP3) from MP4 video

  ```
  ffmpeg -i video.mp4 -f mp3 -ab 192000 -vn music.mp3
  ```

  or specify codec to use `libmp3lame` in this case.

  ```
  ffmpeg -i video.mp4 -f mp3 -codec:a libmp3lame -ab 320000 -vn music.mp3
  ```

  `-i`: *input file*

  `-f mp3`: *file format should be MP3*

  `-ab 192000`: *audio should be encoded at 192Kbps. 320000 for 320Kbps*

  `-vn`: *don't want video*


* Cut video by time interval

  *Cut video starting from 19 min 49 seconds up to 04 mins 18 seconds.*

  ```
  ffmpeg -y -i Video.mp4 -qscale 1 -ss 00:19:49.0 -t 00:04:18.0 -acodec copy -vcodec copy output.mp4
  ```

  _Note_: `-sameq` was removed in recent version of `ffmpeg`

* Use `mplayer` to extract audio(MP3)

  ```
  mplayer -dumpaudio movie.flv -dumpfile movie_audio_track.mp3
  ```

* Reduce resolution

  ```
  ffmpeg -i Birdman.mp4 -strict -2  -s 720x480 birdman.mp4
  ```

* recordmydesktop

  ```
  recordmydesktop -x 100 -y 100 --width 1280 --height 720 --freq 48000 --fps 30 -o ~/Videos/recordings/test-video.ogv
  ```

* Include subtitles(Use `subtitleeditor` to create subtitle)

  ```
  ffmpeg -i video.avi -vf subtitles=subtitle.srt out.avi
  ```

#### Image manipulation

* Resize image 50% of its original size

  ```
  convert dragon.gif -resize 50% half_dragon.gif
  ```

* Control compression level of an image

  ```
  convert input.png -quality 75 output.jpg
  ```

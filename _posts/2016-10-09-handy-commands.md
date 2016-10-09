---
layout: post
title: Handy commands
tags: gs, mplayer, ssh, convert, wget, import, ffmpeg
category: blog
permalink: /blog/handy-commands/
author: sachin
comments: true
---

List of commands for day-to-day use

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

  `-rkp`: *recursive, make link suitable to local viewing, download
all files needed to properly view the page.*

  `-l5`: *recursively download 5 links away form the original page.*

  `-n`: *retrieve files below parent directory.*

  `-H`: *Span across hosts when doing recursive retrieving.*


* Reduce PDF size

  ```
  gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -sOutputFile=new_file.pdf original_file.pdf
  ```

* Unlock PDF file

  ```
  gs -q -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -sOutputFile=unencrypted.pdf -c .setpdfwrite -f encrypted.pdf
  ```

* Capture screenshot

  ```
  import -window root screenshot.png
  ```

* Rotate video

  ```
  # Using mplayer(watch rotated video)
  mplayer -vf-add rotate=1 sample.mp4

  # Using ffmpeg
  ffmpeg -i infile.mp4 -strict -2 -vf "transpose=1" outfile.mp4
  ```

* Convert 3gp to mp4

  ```
  ffmpeg -i VID_0050.3gp -strict -2 -q:a 0 -ab 64k -ar 44100 VID_0050.mp4
  ```

* Resize image 50% of its original size

  ```
  convert dragon.gif -resize 50% half_dragon.gif
  ```

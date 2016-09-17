---
layout: post
title: Very happy with Emacs pretest
tags: emacs, pretest
category: blog
permalink: /blog/happy-emacs/
author: sachin
comments: true
---

I decided to use pretest version of Emacs instead of a stable release
and so far it turned out to be a pleasant experience.

![img]({{ site.baseurl }}/images/happy-emacs/emacs-pretest.png
"Emacs pretest"){: center-image}

For those who don't have any idea, you can visit
[http://alpha.gnu.org/gnu/emacs/pretest/](http://alpha.gnu.org/gnu/emacs/pretest/)
and download the latest version. Compiling and using should not be a
problem. But still for newcomers, following are the steps:

- Download and extract the latest pretest version.

        wget -Nc --show-progress http://alpha.gnu.org/gnu/emacs/pretest/emacs-25.0.92.tar.xz
		tar xvJf emacs-25.0.92.tar.xz

- Configure and compile.

        cd emacs-25-0.92

	Make sure you have `/opt/emacs-pretest` directory present.

	    sudo mkdir -p /opt/emacs-pretest

	Configure the build environment

		./configure --prefix=/opt/emacs-pretest --host=x86_64-fedora23-linux-gnu

	Build from source

        make

   `make` will take time depending on your system specs

	If you are not aware of the flags:

	- `--prefix` makes sure that the final binary(with directory
	  structure) will be copied inside `/opt/emacs-pretest/` when you
	  run `make install`

    - `--host` ensures that when you do `M-x version`, it should return
      'x86_64-fedora23-linux-gnu' instead of 'x86_64-unknown-linux-gnu'.
      Feel free to experiment but make sure the string ends with 'linux'
      or 'gnu'.

	If the `make` is successful, you can go head and try the build.

        src/emacs

	Now try querying the version within Emacs.

	    M-x version

- Install

	Try out Emacs with your custom configuration. When you are happy,
    you can proceed toward installation.

		sudo make install

	Emacs binary will be inside `/opt/emacs-pretest/bin/emacs`. This
    is symbolic link to the file
    `/opt/emacs-pretest/bin/emacs-25.0.92`

If everything goes well, you can add this binary to your launch
application or just create a desktop shortcut.

You should keep the stable version of Emacs as a backup. Till now, I
never faced any problem and will continue using Emacs-pretest as my
default.

If you encounter any issues during `make`, make sure you have all
dependencies installed. If you think, there is an issue in the pretest
release and needs to be fixed, make sure that it is reproducible
before notifying `emacs-devel@gnu.org`. You can also ask for help on
IRC at freenode, channel `#emacs`.

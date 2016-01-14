---
layout: post
title: Python virtualenv
tags: python, setv, virtualenv
category: blog
permalink: /blog/setv/
author: sachin
comments: true
---

`setv` an alternative to `virtualenvwrapper`

I like to have a separate
[virtualenv](http://www.virtualenv.org/en/latest/) for each python
project. This ends up having virtual-environments for each project
that I often find difficult to manage. All my virtual-environments
resides in `~/virtualenvs` directory but to activate/deactivate a
virtual environment every time is a tedious job.

An easy solution to this is to install
[virtualenvwrapper](http://virtualenvwrapper.readthedocs.org/en/latest/index.html),
but then I have run commands like `workon` & `mkvirtualenv`. I don't
want to do that. Can I manage virtual environment using single
command?. Luckily I have Bash function I find very handy. It lists all
available virtual environments and can switch the environment as
needed.

## Usage:

- List all virtual environment

        setv [TAB] [TAB]

      or

        setv -l

- Switch virtual environment

        setv <VIRTUAL-ENVIRONMENT-NAME>

      for example:

        setv rango

- Create new virtual environment

        setv -n <NEW-VIRTUAL-ENVIRONMENT-NAME>

      for example:

        setv -n foobar

- Delete existing virtual environment

        setv -d <EXISTING-VIRTUAL-ENVIRONMENT-NAME>

      for example:

        setv -d foobar

- Deactivate virtual environment

        deactivate

## Download

The script is available
[here](https://raw.github.com/psachin/bash_scripts/master/virtual.sh)
and can be downloaded via `wget`

    wget https://raw.github.com/psachin/bash_scripts/master/virtual.sh

## Install

- Set `VIRTUAL_DIR_PATH` value to your virtual environments
  directory-path in `virtual.sh` file. By default it is set to
  `~/virtualenvs/`

- Create a directory to hold all virtual environments

        mkdir ~/virtualenvs

- Added this line to your `.bashrc` or any local rc script.

        source /path/to/virtual.sh

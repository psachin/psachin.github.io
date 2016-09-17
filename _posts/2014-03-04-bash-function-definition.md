---
layout: post
title: Find bash function
tags: bash, function
category: blog
permalink: /blog/bash-function/
author: sachin
comments: true
---

In this post I'll walk you through few commands which will help to
find the location & definition of Bash functions.

I have lot of custom Bash functions for every seldom and frequent
tasks. Usually I like to store these functions in `~/.bashrc` file but
when they grow in size and importance, I like to keep it in a separate
Bash script and `source` this script from `~/.bashrc`. As these Bash
scripts goes on increasing and so does the functions, it becomes
tedious to locate these functions.

Unlike `which` command, which is used to find a program file location,
we can't use it to find Bash function location. But there is a way we can
read the function definition and also find its location.

## Read function definition

`type` can be used to read function definition.

    type -a <FUNCTION-NAME>

For example, I have a function called `mcd` to create new directory
and `cd` in to it. The following command will print the function
definition

    type -a mcd

Output:

    mcd is a function
    mcd ()
    {
      if [ "$#" -eq 1 ]; then
          mkdir --parents "$1";
          cd "$1";
      else
          echo "Usage: mcd <DIR_NAME>" > /dev/stderr;
      fi
    }


### Update <2016-04-06 Wed>

I you enable shell debug ON USING `set -e`, you can still read a
function definition.

	set -e
	which mcd

## Find function location in a file

In the similar way `declare` can be used to locate the function.

To locate the function, turn on shell debugging using

    shopt -s extdebug

and then

    declare -F <FUNCTION-NAME>

For example, to find `mcd`'s location, type

    declare -F mcd

Output:

    mcd 51 /home/sachin/.bashrc


**51** is the line number in file `~/.bashrc` where `mcd` is defined.

Finally turn off shell debugging.

    shopt -u extdebug

## Custom function

Its better to write a custom function(`whichf` in this case) using
above commands.

    function whichf () {
      if [ ${1} ];
      then
          shopt -s extdebug
          declare -F ${1}
          shopt -u extdebug
          type -a ${1}
      else
          echo "Error: Expected Function name as an argument!"
      fi
    }

Copy above function in `~/.bashrc` file and source the file using

    source ~/.bashrc

Now call this function by typing

    whichf <FUNCTION-NAME>

For example

    whichf mcd

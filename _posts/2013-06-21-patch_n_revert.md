---
layout: post
title: patch and revert source code
tags: patch, linux, kernel, revert
category: blog
permalink: /blog/patch-n-revert/
author: sachin
comments: true
---

Using `patch` efficiently.

We often have the situation while testing to applying a patch or to
remove changes made by a patch. It may happen that a patch is not
correctly applied and result into a dirty source code. This simple bit
of information will help you to carefully apply the patch to your
source code and also revert the changes back to original state if
something goes wrong. I'm using linux kernel version **3.0.42+** as
and example and Elan Touch Screen patch
file(`patch-linux-3.0.42+_elan_ts.patch`).

Unpack and change directory to your linux kernel version you want to
apply the patch for. I this case my kernel version is 3.0.42+

    cd linux-3.0.42+

I have a patch file in the `~/Downloads` directory. Patch files
generally ends with `.patch`. This helps in differentiating them as
patches.

It is always recommended to do a dry run before actually applying a
patch.

    patch -p1 --dry-run < ~/Downloads/patch-linux-3.0.42+_elan_ts.patch


1. `-p1` stands for verbosity. For more information, please refer
    comment by *Yogesh* [here](http://www.cyberciti.biz/faq/appy-patch-file-using-patch-command/).

2. `--dry-run` will not actually apply a patch, but gives you an
output as if the patch is really applied.

If `--dry-run` applies a patch without any error message, you can go
ahead an apply a real patch.

    patch -p1 < ~/Downloads/patch-linux-3.0.42+_elan_ts.patch

Now if you want to remove a patch just add the flag `-R`. For example,

    patch -R -p1 < ~/Downloads/patch-linux-3.0.42+_elan_ts.patch

Remember you have to give full path to your patch file when you apply
or revert a patch. If you plan to apply or revert a patch it is
recommended to apply/revert one patch at a time. In this way you can
carefully manage you patches.

Hope this was helpful.

Linux kernel has an excellent documentation on this topic
[applying-patch](https://www.kernel.org/doc/Documentation/applying-patches.txt).

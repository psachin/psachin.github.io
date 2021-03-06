---
layout: post
title: Python 3.x on RHEL7
tags: python, rhel
category: blog
permalink: /blog/python3-on-rhel7/
author: sachin
comments: true
---

Manually install Python-3.5 in Red Hat Enterprise Linux

### Install required dependencies

{% highlight bash linenos %}
yum install zlib-devel openssl-devel readline \
readline-devel sqlite-devel tkinter ncurses-static \
ncurses-base ncurses-term -y
{% endhighlight %}


### Download, Configure, & Install Python

Download and extract the tarball

{% highlight bash linenos %}
wget --progress=bar https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tar.xz

# Extract tarball
tar xvJf Python-3.5.2.tar.xz
{% endhighlight %}

Configure and install

{% highlight bash linenos %}
cd Python-3.5.2
./configure --prefix=/usr/local

# make [-jX], where X is number of jobs.
# This can be less-than or equal to number
# of cpu-cores
make -j4
make install
{% endhighlight %}


*Sample tailed output*

	Collecting setuptools
	Collecting pip
	Installing collected packages: setuptools, pip
	Found existing installation: setuptools 18.2
    Uninstalling setuptools-18.2:
      Successfully uninstalled setuptools-18.2
    Found existing installation: pip 7.1.2
    Uninstalling pip-7.1.2:
      Successfully uninstalled pip-7.1.2
    Successfully installed pip-8.1.1 setuptools-20.10.1


You should have successfully installed Python-3.5.2 by now.

{% highlight bash linenos %}
which python3.5
#  Output
/usr/local/bin/python3.5
{% endhighlight %}


### [Optional] Create virtual environment

You can go head and try creating Python virtual environment
using [pyenv](https://docs.python.org/3/library/venv.html).

{% highlight bash linenos %}
pyvenv py3
source py3/bin/activate
{% endhighlight %}

Once inside the virtual environment, verify Python version

{% highlight bash linenos %}
(py3) [jedi@pywar ~]$ python --version
Python 3.5.2
{% endhighlight %}

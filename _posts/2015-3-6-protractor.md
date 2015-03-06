---
layout: post
title: Install Protractor
tags: nodejs, protractor
category: blog
---

Protractor is an unittest framework for
[AngularJS](http://angularjs.org/) applications. It is based on
[Node.js](http://nodejs.org/). To install Protractor, you need to
install Node.js

## To install Node.js
1. Download source code of Node.js from
   [nodejs.org](http://nodejs.org/download/). Debian/Ubuntu user may
   use `apt-get` to install Node.js.
2. Untar using tar -xvzf node-vXXX.tar.gz
3. Configure, compile, and install using
```shell
cd node
./configure
make
sudo make install
```


`npm` is a package-manager for Node.js. It should installed with
Node.js



## Now install Protractor using
1. `sudo npm install -g protractor`
...`-g` will install protractor globally
2. This will also install `webdriver-manager`. Update
...webdriver-manager using:


...`webdriver-manager update`











![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.

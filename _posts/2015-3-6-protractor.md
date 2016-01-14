---
layout: post
title: Install Protractor
tags: nodejs, protractor
category: blog
permalink: /blog/protractor/
author: sachin
comments: true
---

Protractor is an unittest framework for
[AngularJS](http://angularjs.org/) applications. It is based on
[Node.js](http://nodejs.org/). To install Protractor, you need to
install Node.js

#### To install Node.js
1. Download source code of Node.js from
   [nodejs.org](http://nodejs.org/download/). Debian/Ubuntu user may
   use `apt-get` to install Node.js.
2. Untar using `tar -xvzf node-xxx.tar.gz`
3. Configure, compile, and install using


```sh
cd node
./configure
make
sudo make install
```


4. `npm` is a package-manager for Node.js. It should installed with
   Node.js


#### Now install Protractor using
1. `sudo npm install -g protractor`. `-g` will install protractor
   globally
2. This will also install `webdriver-manager`. Update
   webdriver-manager using: `webdriver-manager update`

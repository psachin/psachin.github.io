---
layout: post
title: Install Protractor
tags: nodejs, protractor
category: blog
permalink: /blog/protractor/
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

% if page.comments %
<div id="disqus_thread"></div>
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES * * */
    var disqus_shortname = 'darkstar';

    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
% endif %

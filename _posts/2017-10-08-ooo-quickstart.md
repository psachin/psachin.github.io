---
layout: post
title: TripleO quickstart
tags: tripleo, quickstart
category: blog
permalink: /blog/ooo-quickstart/
author: sachin
comments: true
---


Setup
[tripleo-quickstart](https://docs.oepenstack.org/tripleo-quickstart/latest/readme.html)
environment.

### Create non-root user

``` bash
adduser <NON-ROOT-USER> -G wheel
passwd <NON-ROOT-USER>
```


Login as NON-ROOT-USER and download required scripts

``` bash
ssh-keygen
export VIRTHOST=127.0.0.2
ssh-copy-id root@$VIRTHOST

# Test the settings
ssh root@$VIRTHOST uname -a

# Download required scripts
git clone https://github.com/openstack/tripleo-quickstart.git
# Last time I checked, commit hash 0a5dc8de8df3ddbf1886b8416b55464b0910c7ba
# worked for me pretty well.

# Download Heat templates(Optional)
git clone https://github.com/openstack/tripleo-heat-templates.git

cd tripleo-quickstart
./quickstart.sh --install-deps
```

### Deploy OpenStack


* 1-ctrl, 1-compute, pacemaker (Ocata release)

``` bash
./quickstart.sh --config config/general_config/pacemaker.yml  \
-N config/nodes/1ctlr_1comp.yml \
--teardown all \
--tags all \
--clean \
--release ocata $VIRTHOST
```

* 3-ctrl, 1-compute, pacemaker (Ocata release)

``` bash
./quickstart.sh --config config/general_config/pacemaker.yml \
-N config/nodes/3ctlr_1comp.yml \
--teardown all \
--tags all \
--clean \
--release ocata $VIRTHOST
```

* 1-ctrl, 1-compute, pacemaker (Master branch with latest commit)

``` bash
./quickstart.sh --config config/general_config/pacemaker.yml \
-N config/nodes/1ctlr_1comp.yml \
--teardown all \
--tags all \
--clean \
--release master-tripleo-ci $VIRTHOST
```

* 1-ctrl, 1-compute, pacemaker (Ocata with telemetry)

  Note the selecting any release other that newton will disable
  telemetry. To enable telemetry remove following lines from
  `pacemaker.yml`. I usually save file as `pacemaker-enable-telemetry.yml`

``` bash
./quickstart.sh --config config/general_config/pacemaker-enable-telemetry.yml \
-N config/nodes/1ctlr_1comp.yml \
--teardown all \
--tags all \
--clean \
--release ocata $VIRTHOST
```

Once setup is complete login to undercloud node using,

``` bash
ssh -F /home/NON-ROOT-USER/.quickstart/ssh.config.ansible undercloud
```

and source `overcloudrc` for API version 2 or `overcloudrc.v3` for API
version 3


### Reference

* [psachin/gist](https://gist.github.com/psachin/6ba906217984f7dec97efce7b753ad11)

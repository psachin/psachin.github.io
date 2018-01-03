---
layout: post
title: Test tripleo-quickstart environment
tags: tripleo, quickstart
category: blog
permalink: /blog/test-ooo-quickstart/
author: sachin
comments: true
---


[Last post](http://psachin.github.io/blog/ooo-quickstart/) explains
how to setup tripleo-quickstart environment. In this post we will see
how to test the environment by using [heat
template](https://docs.openstack.org/heat/latest/template_guide/hot_guide.html).

Below is the sample template that can be used to deploy a stack which
will deploy an instance using cirros image.


{% gist 85b89e125007bca0b4fc2d5bd2d19fa6 %}


Download the template using,

	wget https://gist.githubusercontent.com/psachin/85b89e125007bca0b4fc2d5bd2d19fa6/raw/test-stack.yml

Download and create glance image,

	curl http://download.cirros-cloud.net/0.3.5/cirros-0.3.5-x86_64-disk.img -o cirros-0.3.5-x86_64-disk.img
	openstack image create --public --container-format bare --file cirros-0.3.5-x86_64-disk.img cirros

Finally create a stack using,

	openstack stack create --template test-stack.yml test-stack

Once stack creation is completed, get IP address of an instance using
comment `openstack server list`(should be in range 192.168.24.0/24)
and you are good to go.

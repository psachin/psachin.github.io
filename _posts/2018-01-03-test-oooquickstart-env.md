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

{% highlight bash linenos %}
wget https://gist.githubusercontent.com/psachin/85b89e125007bca0b4fc2d5bd2d19fa6/raw/test-stack.yml
{% endhighlight %}

Download and create glance image,

{% highlight bash linenos %}
curl http://download.cirros-cloud.net/0.3.5/cirros-0.3.5-x86_64-disk.img -o cirros-0.3.5-x86_64-disk.img
openstack image create --public --container-format bare --file cirros-0.3.5-x86_64-disk.img cirros
{% endhighlight %}

Finally create a stack using,

{% highlight bash linenos %}
openstack stack create --template test-stack.yml test-stack
{% endhighlight %}

Once stack creation is completed, get IP address of an instance using
comment `openstack server list`(should be in range 192.168.24.0/24)
as show in example below,

{% highlight bash linenos %}
[stack@undercloud ]$ openstack server list
+--------------------------------------+-----------------------------------------------+--------+------------------------------------+------------+
| ID                                   | Name                                          | Status | Networks                           | Image Name |
+--------------------------------------+-----------------------------------------------+--------+------------------------------------+------------+
| c14904d2-bc35-48a3-bc75-7b778eb02acd | test-stack-test_instance-1-adgli2qymnzm       | ACTIVE | int-green=30.0.0.8, 192.168.24.110 | cirros     |
+--------------------------------------+-----------------------------------------------+--------+------------------------------------+------------+
{% endhighlight %}

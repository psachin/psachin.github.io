---
layout: post
title: ManageIQ - Attach disk to RHV VM using button
tags: manageiq, rhv, rhevm, button, disk
category: blog
permalink: /blog/miq-rhv-vm-add-disk/
author: sachin
comments: true
---

Post describes a way to attach additional disk to RHV VM using button.

<p align="center">
<img src="{{ site.baseurl }}/images/miq-add-disk/manageiq-logo-standard-vertical.png"
	alt="ManageIQ logo"
	width=""
	height="200">
</p>

Just to get my hands dirty
on
[ManageIQ's Automate model](http://manageiq.org/docs/reference/latest/doc-Methods_Available_for_Automation/miq/),
I started working on a way to attach additional disk to VM
on
[Red Hat Virtualization](https://access.redhat.com/products/red-hat-virtualization).
Although it can be easily done by "Reconfigure this VM", I wanted a way
to do this via Automate. I did found two ways to do this, one
described
in
[Mastering Automation in CloudForms & ManageIQ](https://pemcg.gitbooks.io/mastering-automation-in-cloudforms-4-2-and-manage/content/customising_vm_provisioning/chapter.html) and
other
[here](http://www.jung-christian.de/2016/08/add-an-additional-disk-on-rhev-virtual-machines/).
Both uses ReST APIs to achieve the task but then I came across
this [Pull Request](https://github.com/ManageIQ/manageiq/pull/13318)
which made the job quite easy.

### Datastore

I have created a domain
-- [AutomateMIQ](https://github.com/psachin/AutomateMIQ.git) which has
a custom method -- `add_disk`. It is called by instance
`hot_add_disk`. `add_disk` has everything you need to attach new disk
to VM including notifications and email.

<p align="center">
<img src="{{ site.baseurl }}/images/miq-add-disk/datastore.png"
	alt="Automate datastore"
	width=""
	height="550">
	<br/>
	<b>Automate datastore</b>
</p>

Now datastores can be managed by [`git`](https://git-scm.com) has seen
below.

<p align="center">
<img src="{{ site.baseurl }}/images/miq-add-disk/automate-git.png"
	alt="Use Automate git to manage datastore"
	width=""
	height="350">
	<br/>
	<b>Use Automate git to manage datastore</b>
</p>

### Service dialog

One also needs to create a service dialog which prompts for **disk
size** and **disk provisioning type**. These fields are then imported
by `add_disk`. The disk is then attached based on user defined
parameters. I have
imported
[service dialog](https://gist.github.com/psachin/d601fc54c9ba060c132fbf052af8c7c7) in
form on yaml for reference.

<p align="center">
<img src="{{ site.baseurl }}/images/miq-add-disk/dialog_add_disk.png"
	alt="Service dialog prompts for disk size and provisioning type"
	width=""
	height="300">
	<br/>
	<b>Service dialog prompts for disk size and provisioning type</b>
</p>


### Button

Finally we need a button to call instance `hot_add_disk`. A button
calls request type `AddDisk` from `/System/Process/` as seen below.
Please find button in form of
yaml
[here](https://gist.github.com/psachin/7079e1328810bb61dda485845009f921).

<p align="center">
<img src="{{ site.baseurl }}/images/miq-add-disk/button_add_disk.png"
	alt="Create button to add disk"
	width=""
	height="550">
	<br/>
	<b>Create button to add disk</b>
</p>

Button will appear on VM's summary page as below.

<p align="center">
<img src="{{ site.baseurl }}/images/miq-add-disk/button_action_add_disk.png"
	alt="Add disk button on VM's summary page"
	width=""
	height="200">
	<br/>
	<b>Add disk button on VM's summary page</b>
</p>

### Notifications

Once the disk is attached, user will be notified.

<p align="center">
<img src="{{ site.baseurl }}/images/miq-add-disk/notification.png"
	alt="Notification"
	width=""
	height="200">
	<br/>
	<b>Notification</b>
</p>

Finally, an additional disk will be attached to VM.

<p align="center">
<img src="{{ site.baseurl }}/images/miq-add-disk/number_of_disks.png"
	alt="Newly attached disk"
	width=""
	height="150">
	<br/>
	<b>Newly attached disk</b>
</p>

_Note that the feature work on **euwe** release of ManageIQ. If not
already done, please upgrade ManageIQ version following below steps._

	# SSH to ManageIQ
	vmdb
	git fetch --all
	git checkout euwe-2
	bundle install
	bundle exec rake evm:compile_assets
	bundle exec rake evm:restart

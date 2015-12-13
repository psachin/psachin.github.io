---
layout: post
title: Enable Kernel virtualization on Intel/AMD arch
tags: kvm, virtualization, linux
category: blog
permalink: /blog/kvm/
comments: true
---

Enable *Kernel-based Virtual Machine* on your system.


To check if the hardware supports Virtualizaton Technology(VT), open a
terminal and type

    egrep '(vmx|svm)' /proc/cpuinfo

if you can see a output, means your hardware supports VT.

Next step is to enable load kernel modules(Irrespective of your
processor type)

    sudo modprobe kvm_intel
    sudo modprobe kvm

## Note
In above command

- `vmx`(Virtual Machine eXtension) - is for Intel processor
- `svm`(Secure Virtual Machine) - is for AMD processor

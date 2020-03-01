---
title: "PREEMPT_RT"
layout: single
author_profile: true
excerpt: "Absolute mad lad"
header:
  overlay_color: "#333"
---

Check which preempts are set on your distribution:

```bash
 cat /boot/config-4.15.0-50-generic | grep PREEMPT
```
* CONFIG_PREEMPT
* CONFIG_PREEMPTIRQ_EVENTS
* CONFIG_HZ

These options should be set (according to [Real time ethernet](https://www.osadl.org/Real-time-Ethernet-UDP-worst-case-roun.qa-farm-rt-ethernet-udp-monitor.0.html))
* CONFIG_RCU_BOOST=y   
* CONFIG_RCU_BOOST_PRIO=99

[How To determine Linux Kernel Timer Interrupt Frequency](https://www.advenage.com/topics/linux-timer-interrupt-frequency)

[Interupt handling](https://www.oreilly.com/library/view/linux-device-drivers/0596005903/ch10.html)
[Red hat performance tuning](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/performance_tuning_guide/index)

### Compile linux kernel with preempt_rt for ubuntu 18.04


1. Check your kernel version

```bash
uname -r
```
[Ubuntu and linux kernel versions](https://people.canonical.com/~kernel/info/kernel-version-map.html)

[Notes on compiling preempt_rt](http://kernel-notes.gbittencourt.net/compiling-preempt-rt/)

### Setting RT priority on non-rt kernel

[Audio jack rt Linux configuration](https://jackaudio.org/faq/linux_rt_config.html)

### References

[Intel Optimizing Computer applications for latency](https://software.intel.com/en-us/articles/optimizing-computer-applications-for-latency-part-1-configuring-the-hardware)


### Video

[Maintaining a Real Time Stable Kernel - Steven Rostedt, VMware
](https://www.youtube.com/watch?v=pIJ3Zv_uxn0&list=WL&index=8&t=1163s)

[Kernel Recipes 2016 - Understanding a Real-Time System (more than just a kernel)](https://www.youtube.com/watch?v=w3yT8zJe0Uw&list=PL4bIb95zE1Mqv1VbHeBCzH7K0ZscOgAz_)

[Linux Performance Optimization - Red Hat EX442 - Complete Video Course](https://www.youtube.com/watch?v=2kNih0fqnzQ)

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
*
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

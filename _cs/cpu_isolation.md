---
title: "CPU isolation"
layout: single
author_profile: true
excerpt: "Getting real time performance without PREEMPT_RT or Xenomai"
header:
  overlay_color: "#333"
---

"If we would like to get real-time performance on single-CPU systems it is necessary to adapt the entire system, e.g. using the PREEMPT_RT patch or an RTOS. This is not always necessary in a multicore system."

# Architecture layout

Before:

lstopo

After:

```bash
sudo gedit /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash isolcpus=1,5"
```

reboot and chneck that the parameter was passed to the kernel

```bash
cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-4.15.0-43-generic root=UUID=47226ffd-864a-4f7d-9f15-779cdee4bdf3 ro quiet splash isolcpus=1,5 vt.handoff=1
```

Processor per CPU before CPU isolation

```bash
cpu: 0  pid: 37.0
cpu: 1  pid: 49.0
cpu: 2  pid: 48.0
cpu: 3  pid: 45.0
cpu: 4  pid: 41.0
cpu: 5  pid: 46.0
cpu: 6  pid: 45.0
cpu: 7  pid: 32.0
```

Processes per CPU after CPU isolation

```bash
cpu: 0  pid: 51.0
cpu: 1  pid: 8.0
cpu: 2  pid: 49.0
cpu: 3  pid: 42.0
cpu: 4  pid: 42.0
cpu: 5  pid: 8.0
cpu: 6  pid: 63.0
cpu: 7  pid: 57.0
```

The remaining 8 process for both cpus are:

* cpuhp PRI: RT NI 0
* watchdog PRI: RT NI 0
* migration PRI: RT NI 0
* ksoftirqd PRI: 20 NI 0
* kworker/1:0 PRI 20 NI 0
* kworker/1:0H PRI 0 NI -20

[linux kernel software interrupts](https://lwn.net/Articles/520076/)
[Real-time Linux communications: an evaluation of the Linux
communication stack for real-time robotic applications](https://arxiv.org/pdf/1808.10821.pdf)


```bash
  stress -d 4 --hdd-bytes 20M -c 4 -i 4 -m 4 --vm-bytes 15M -t 40s
```

## Ethernet Optimization

* [Network Stack](https://www.cubrid.org/blog/understanding-tcp-ip-network-stack)

* [net_prio](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/resource_management_guide/net_prio)

* [How to achieve low latency](https://blog.cloudflare.com/how-to-achieve-low-latency/)

* [IMPROVE NETWORK PERFORMANCE BY SETTING PER-QUEUE INTERRUPT MODERATION IN LINUX](https://01.org/linux-interrupt-moderation)

* [Traffic Control](https://wiki.debian.org/TrafficControl)

* [Low latency tcp settings on ubuntu](https://serverfault.com/questions/623780/low-latency-tcp-settings-on-ubuntu)

* [Low latency tuning on red hat](https://access.redhat.com/sites/default/files/attachments/201501-perf-brief-low-latency-tuning-rhel7-v1.pdf)

### network questions

* Is there one transmite queue per interface ?
* Can I increase the rate at which TCP execution occures.
* What does increasing the interrupt rate of the NIC driver do ?

### rx-tx optimization


/sys/class/net holds all the network interfaces
/sys/class/net/eno1/queues holds queues for receiving and sending data over the network interface
card. In my case I have:

* rx-0  
* tx-0

I have one queue for receiving data (rx-0) and one for sending data (tx-0)



## low latency ubuntu kernel

```bash
sudo apt-get install linux-lowlatency
```


### Low latency vs generic ubuntu Kernel

```bash
diff config-4.15.0-50-generic config-4.15.0-50-lowlatency
```

The low latency has the following additions:


* CONFIG_IRQ_FORCED_THREADING_DEFAULT=y
* CONFIG_TREE_RCU (removed)
* CONFIG_PREEMPT_RCU=y
* CONFIG_UNINLINE_SPIN_UNLOCK=y

* CONFIG_PREEMPT_VOLUNTARY=y (removed)
* CONFIG_PREEMPT=y
* CONFIG_PREEMPT_COUNT=y

* CONFIG_HZ_1000=y
* CONFIG_HZ=1000

* CONFIG_CEC_PIN=y (removed)
* CONFIG_CEC_GPIO=m

* CONFIG_LATENCYTOP=y
* CONFIG_PREEMPT_TRACER (removed)


### Bios settings

* [BIOS settings](https://homerl.github.io/2018/05/27/bios/)

* C-State
The C-State represents the processor power
state of the core. The C-State is often more commonly known as the
processor “idle” state of the core. C-State values range from C0 to Cn, where
n is dependent on the specific processor. When the core is active and
executing instructions it is in the C0 state. Higher C-States indicate how deep
the CPU idle state is.

* P-State
The voltage frequency pair is known as the Device and Processor
Performance State (P-State). A P-State of P0 is the highest voltage/frequency
pairing. A high P-State will have lower voltage and frequency levels. It takes
the processor longer to complete a task in a high P-State, but less energy is
consumed.


## Links

* [Ethernet optimization](https://greenhost.net/blog/2013/04/10/multi-queue-network-interfaces-with-smp-on-linux/)
* [Networking bonding](https://wiki.linuxfoundation.org/networking/bonding)
* [C++11 thread affinity](https://eli.thegreenplace.net/2016/c11-threads-affinity-and-hyperthreading/)
* [Improving real time properties](http://linuxrealtime.org/index.php/Improving_the_Real-Time_Properties#Benchmarks_for_CPU_Isolation)
* [How To Optimize Performance](https://wiki.fd.io/view/VPP/How_To_Optimize_Performance_(System_Tuning))
* [Linux kernel IRQ affinity](https://www.kernel.org/doc/Documentation/IRQ-affinity.txt) is a good resouce on the subject.
* [SMP-affinity](https://cs.uwaterloo.ca/~brecht/servers/apic/SMP-affinity.txt)

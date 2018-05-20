---
title: "Batteries"
layout: single
author_profile: true
excerpt: ""
header:
  overlay_color: "#333"
---
{% include base_path %}

<!-- KaTeX -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## jargon

* LiPo - Lithium-ion Polymer
* NiMH - Nickel-Metal Hydrid
* Discharge Rating

### Capacity

Capacity is denonted in milliampers hours (mAh) on the battery. It is the amount of charge stored
in the battery.
If you have a battery with a capaciy 1 mAh and a motor is drawing 1 mAh then your motor will run for 1 h. In general the \textit{approximate} duration of a battery can be computed
by:

$$\mathrm{duration} (h) = \frac{\mathrm{capaciy(mAh)}}{\mathrm{load (mA)} }$$

If you have a 4700 mAh battery and it is powering a moter with a 100 mA load, it will
keep runing for approximatly 47 hours. [reference](https://electronics.stackexchange.com/questions/79279/does-mah-measure-how-long-a-battery-would-last)


### Discharge


### Battery bank

Combination of multiple batteries [reference](https://www.batterystuff.com/kb/articles/battery-articles/battery-bank-tutorial.html)

* joined in series: voltage increases, capacity remains the same.
* joined in parallel: voltage remains the same, capacity increases.
* series and parallel: both voltage and capacity increase.


[A guide to understanding battery specifications](http://web.mit.edu/evt/summary_battery_specifications.pdf)

[RC battery guide](http://www.ebay.co.uk/gds/RC-Lipo-Batteries-Buying-Usage-and-Storage-Basic-Guide-/10000000205584236/g.html)

## Pixhawk 2.1 battery stuff

[Power brick mini](https://drones.altigator.com/power-brick-mini-for-pixhawk-21-p-42548.html)
* Max continuous current sensing: 30A
* Max burst current: 100A
* Connectors: XT-60

## Electricity

* Ampere: A - base unit. Attractive/repulsive force of $$2 \times 10^{-7}$$ Newtons between
two wires 1m appart is the definition of  $$1\,\mathrm{A}$$.
$$1\,\mathrm{A} = 1\,\mathrm{C} / 1\,\mathrm{s}$$

* Coulomb: C -  charge transported by a constant current of 1 A in on second.
$$1\,\mathrm{C} = 1\,\mathrm{A} \cdot 1\,\mathrm{s}$$

* [Electrical work](http://hyperphysics.phy-astr.gsu.edu/hbase/electric/elewor.html) is the work done on a charged particle by an electric field. 

* Watt : W - power.  $$1\,\mathrm{W} = \frac{1\,\mathrm{N} \cdot \mathrm{m}}{\mathrm{s}}$$

* Volt: V - pressure

* Ohm: $$\Omega$$ - electrical resistance

### voltage

$$ V = \frac{\mathrm{potential energy}}{\mathrm{charge}} = \frac{N\cdot m}{C} $$

### Ohm



* Ah - ampere hour
* mAh - milli ampere hour

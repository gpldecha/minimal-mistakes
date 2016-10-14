---
title: KUKA LWR ROS
permalink: /projects/kuka_lwr_ros/
excerpt: A C++ software package which allows to simulate and control the KUKA LWR robot.

header:
  teaser:  /projects/kuka_lwr_ros/kuka-lwr-th.png
sidebar:
  nav: "docs"
---

{% include image.html
           img="/projects/kuka_lwr_ros/concept.png"
           bbox="false"
%}
<br>
A ROS package to control the KUKA LWR 4,  both in simulation and for the physical robot.
[Rviz](http://wiki.ros.org/rviz) is used to visualize the sensor data coming from
either the [Gazebo](http://gazebosim.org/) simulator or the FRI API interfacing the
KUKA control box.

* github package [kuka-lwr-ros](https://github.com/epfl-lasa/kuka-lwr-ros)
* examples using this package: [kuka-lwr-ros-examples](https://github.com/epfl-lasa/kuka-lwr-ros-examples)

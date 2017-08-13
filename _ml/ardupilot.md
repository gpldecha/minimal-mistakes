---
title: "ArduPilot ecosystem"
layout: single
author_profile: true
excerpt: ""
header:
  overlay_color: "#333"
---
# [DroneKit](https://github.com/dronekit/dronekit-python)

DroneKit-Python allows developers to create apps that run on an onboard companion computer and communicate with the ArduPilot flight controller using a low-latency link.

The API communicates with vehicles over MAVLink. It provides programmatic access to a connected vehicle’s telemetry, state and parameter information, and enables both mission management and direct control over vehicle movement and operations.

Drone-kit is a python API corresponding to the functionality of mavproxy. This means you can arm, change flight modes and send waypoints.
The constraint being that all of this happens at a low frequency.

If you want to implement an an autonomous vehicle with your very
own AI you would choose the [GUIDED](http://python.dronekit.io/guide/copter/guided_mode.html#guided-mode-copter-control-movement) mode. There are [two ways to
control the vehicle](http://python.dronekit.io/guide/copter/guided_mode.html#guided-mode-copter-velocity-control)

1. Position. In this mode positions in relative/global frame are
sent to vehicle (over mavlink) in the form of goto commands.

2. Velocity
The function send_ned_velocity() below generates a SET_POSITION_TARGET_LOCAL_NED MAVLink message which is used to directly specify the speed components of the vehicle in the MAV_FRAME_LOCAL_NED frame (relative to home location). The message is re-sent every second for the specified duration.

# [PX4 pro](https://github.com/PX4/Firmware)

[PX4 Pro](http://px4.io/)

Build an Agent on your offboard compute which communicate with the PX4 autopilot client. The client and agent both run as daemon process.

[PX4-user-guide](https://www.gitbook.com/book/px4/px4-user-guide/details)
[PX4-dev-guide](https://dev.px4.io/en/)


1. [PX4-Firmware](https://github.com/PX4/Firmware/tree/master/src)
This repository holds the PX4 Pro flight control solution for drones, with the main applications located in the src/modules directory. It also contains the PX4 Drone Middleware Platform, which provides drivers and middleware to run drones.

2. [PX4-flight stack](https://dev.px4.io/en/concept/flight_stack.html)

3. [PX4-middleware](https://dev.px4.io/en/concept/middleware.html)




# [ArduPilot](https://github.com/ArduPilot/ardupilot)

 [Learning the ArduPilot Codebase](http://ardupilot.org/dev/docs/learning-the-ardupilot-codebase.html)

# [Mavros](https://dev.px4.io/en/ros/mavros_installation.html)



# What is the difference between ArduPilot and PX4

ArduPilot uses

# Resources

[px4-gazebo](https://404warehouse.net/2016/07/11/px4-software-in-the-loopsitl-simulation-on-gazebo/)

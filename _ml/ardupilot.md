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

# Notes

Drone-kit is a python API corresponding to the functionality of mavproxy. This means you can arm, change flight modes and send waypoints.
The constraint being that all of this happens at a low frequency.

If you want to implement an an autonomous vehicle with your very
own AI you would choose the [GUIDED](http://python.dronekit.io/guide/copter/guided_mode.html#guided-mode-copter-control-movement) mode. There are [two ways to
control the vehicle](http://python.dronekit.io/guide/copter/guided_mode.html#guided-mode-copter-velocity-control)

1. Position. In this mode positions in relative/global frame are
sent to vehicle (over mavlink) in the form of goto commands.

2. Velocity
The function send_ned_velocity() below generates a SET_POSITION_TARGET_LOCAL_NED MAVLink message which is used to directly specify the speed components of the vehicle in the MAV_FRAME_LOCAL_NED frame (relative to home location). The message is re-sent every second for the specified duration.

# How to do it

[PX4](https://dev.px4.io/en/middleware/micrortps.html)

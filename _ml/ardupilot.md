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

# RC overid

[teleoperation_erle_rover](http://docs.erlerobotics.com/erle_robots/erle_rover/examples/teleoperation_erle_rover)

# [PX4 pro](https://github.com/PX4/Firmware)

[PX4 Pro](http://px4.io/)

Build an Agent on your offboard compute which communicate with the PX4 autopilot client. The client and agent both run as daemon process.

[PX4-user-guide](https://www.gitbook.com/book/px4/px4-user-guide/details)
[PX4-dev-guide](https://dev.px4.io/en/)


1. [PX4-Firmware](https://github.com/PX4/Firmware/tree/master/src)
This repository holds the PX4 Pro flight control solution for drones, with the main applications located in the src/modules directory. It also contains the PX4 Drone Middleware Platform, which provides drivers and middleware to run drones.

2. [PX4-flight stack](https://dev.px4.io/en/concept/flight_stack.html)

3. [PX4-middleware](https://dev.px4.io/en/concept/middleware.html)


* multiple applications known as Apps are runnig on the Pixhawk2:

```bash
~/src/Firmware/Tools$ ./mavlink_shell.py /dev/ttyACM0
Connecting to MAVLINK...

NuttShell (NSH)
nsh> help
...
Builtin Apps:
  adc
  tone_alarm
  fmu
  px4io
  rgbled
  mpu6000
  mpu9250
  lsm303d
  l3gd20
  hmc5883
  ms5611
  sf0x
  ll40ls
  trone
  gps
  pwm_out_sim
  ets_airspeed
  ms4525_airspeed
  ms5525_airspeed
  sdp3x_airspeed
  frsky_telemetry
  sensors
  px4flow
  vmount
  pwm_input
  camera_trigger
  bst
  lis3mdl
  ulanding_radar
  bl_update
  config
  hardfault_log
  mixer
  mtd
  nshterm
  param
  perf
  pwm
  reboot
  top
  ver
  commander
  send_event
  load_mon
  navigator
  mavlink
  gpio_led
  land_detector
  camera_feedback
  ekf2
  fw_att_control
  fw_pos_control_l1
  gnd_att_control
  gnd_pos_control
  mc_att_control
  mc_pos_control
  vtol_att_control
  logger
  uorb
  dataman
  px4_simple_app
  serdis
  sercon

```

Individual message channels between Applications (Apps) are called topics in PX4.

[modules](https://dev.px4.io/en/middleware/modules_main.html)

# [ArduPilot](https://github.com/ArduPilot/ardupilot)

 [Learning the ArduPilot Codebase](http://ardupilot.org/dev/docs/learning-the-ardupilot-codebase.html)

# [Mavros](https://dev.px4.io/en/ros/mavros_installation.html)



# What is the difference between ArduPilot and PX4

ArduPilot uses

# Resources

[px4-gazebo](https://404warehouse.net/2016/07/11/px4-software-in-the-loopsitl-simulation-on-gazebo/)

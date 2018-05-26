---
title: "PX4 rover tutorial"
layout: single
author_profile: true
excerpt: "Example tutorial of px4 rover running Pixhawk2"
header:
  overlay_color: "#333"
---

# Building the Firmware

1. Uncomment in the file src/Firmware/cmake/configs/nuttx_px4fmu-v2_default.cmake the line examples/px4_simple_app. This will register the application src/examples/px4_simple_app.

2. Rebuild the Firmware:

```bash
  ~/src/Firmware$ make px4fmu-v3_rover
```

3. Upload it to the board.
This step will erase what is currently installed on the board and
processed to install the new compiled px4 Firmware.

```bash
  ~/src/Firmware$ make px4fmu-v3_rover upload

chip: 20016419
family: STM32F42x
revision: 3
flash 2080768

Erase  : [====================] 100.0%
Program: [====================] 100.0%
Verify : [====================] 100.0%
Rebooting.

```

4. Check if all is good by connecting to the console onboard
the pixhawk via mavlink.

```bash
~/src/Firmware/Tools$ ./mavlink_shell.py /dev/ttyACM0
Connecting to MAVLINK...

NuttShell (NSH)
nsh>
nsh> help
...
dataman
px4_simple_app
serdis
...
```
Note that px4_simple_app is now part of the available commands. Start it by typing px4_simple_app and ENTER:

# Modules

## General system control

* modules/commander
* modules/events
* modules/gpio_led
* modules/load_mon
* modules/mavlink

## Estimation modules

## Vehicle control

modules/navigator
modules/uavcan
modules/camera_feedback


# Communcation between Raspberrypi and Pixhawk2

The pixhawk2 outputs information on the TELEM2 connection which
is done via the /dev/ttyAMA0 device. The device transmits on a
Broadcom UART.

### Arming example

### Companion computer/ground station

Mavproxy can be used to send commands to the pixhawk flight stack.
Consier the arming of the vehicle from the terminal:

```bash
> arm throttle
```
The following code in the MAVProxy will be called (see [mavproxy_arm.py](https://github.com/ArduPilot/MAVProxy/blob/master/MAVProxy/modules/mavproxy_arm.py)):

```python
if args[0] == "throttle":
    self.master.arducopter_arm()
    return

def arducopter_arm(self):
  '''arm motors (arducopter only)'''
  if self.mavlink10():
    self.mav.command_long_send(
                self.target_system,  # target_system
                self.target_component,
                mavlink.MAV_CMD_COMPONENT_ARM_DISARM, # command
                0, # confirmation
                1, # param1 (1 to indicate arm)
                0, # param2 (all other params meaningless)
                0, # param3
                0, # param4
                0, # param5
                0, # param6
                0) # param7
```
You can see that MAVProxy is wrapper of [pymavlink](https://github.com/ArduPilot/pymavlink) which does the actual sending of the mavlink message over the ttyAMA0 device.
Below is the functin definition from pymavlink.

```python
def command_long_send(self, target_system, target_component, command, confirmation, param1, param2, param3, param4, param5, param6, param7, force_mavlink1=False):
  '''
    Send a command with up to seven parameters to the MAV

        target_system             : System which should execute the command (uint8_t)
        target_component          : Component which should execute the command, 0 for all components (uint8_t)
        command                   : Command ID, as defined by MAV_CMD enum. (uint16_t)
        confirmation              : 0: First transmission of this command. 1-255: Confirmation transmissions (e.g. for kill command) (uint8_t)
        param1                    : Parameter 1, as defined by MAV_CMD enum. (float)
        param2                    : Parameter 2, as defined by MAV_CMD enum. (float)
        param3                    : Parameter 3, as defined by MAV_CMD enum. (float)
        param4                    : Parameter 4, as defined by MAV_CMD enum. (float)
        param5                    : Parameter 5, as defined by MAV_CMD enum. (float)
        param6                    : Parameter 6, as defined by MAV_CMD enum. (float)
        param7                    : Parameter 7, as defined by MAV_CMD enum. (float)
'''
```


Next we see how the Pixhawk receives and processes the message.

### Pixhawk

In the file **src/modules/mavlink/mavlink_receiver.cpp** incoming mavlink messages
are received and published via the micro object request broker (uORB) protocol.

```cpp
void MavlinkReceiver::handle_message_command_long(mavlink_message_t *msg){
	/* command */
	mavlink_command_long_t cmd_mavlink;
	mavlink_msg_command_long_decode(msg, &cmd_mavlink);

	bool target_ok = evaluate_target_ok(cmd_mavlink.command, cmd_mavlink.target_system, cmd_mavlink.target_component);

  (code hidden for brevity)

  struct vehicle_command_s vcmd = {
  .timestamp = hrt_absolute_time(),
  .param5 = cmd_mavlink.param5,
  .param6 = cmd_mavlink.param6,
  /* Copy the content of mavlink_command_long_t cmd_mavlink into command_t cmd */
  .param1 = cmd_mavlink.param1,
  .param2 = cmd_mavlink.param2,
  .param3 = cmd_mavlink.param3,
  .param4 = cmd_mavlink.param4,
  .param7 = cmd_mavlink.param7,
  // XXX do proper translation
  .command = cmd_mavlink.command,
  .target_system = cmd_mavlink.target_system,
  .target_component = cmd_mavlink.target_component,
  .source_system = msg->sysid,
  .source_component = msg->compid,
  .confirmation = cmd_mavlink.confirmation,
  .from_external = 1
};

if (_cmd_pub == nullptr) {
  _cmd_pub = orb_advertise_queue(ORB_ID(vehicle_command), &vcmd, vehicle_command_s::ORB_QUEUE_LENGTH);

} else {
  orb_publish(ORB_ID(vehicle_command), _cmd_pub, &vcmd);
}
```
The commander, see file **src/modules/commander/commander.cpp**, subscribs to the vehicle_command uORB topic and is able
to further process arm command.

```cpp
/* Subscribe to command topic */
int cmd_sub = orb_subscribe(ORB_ID(vehicle_command));
```

### Position control example

In **/mavros/src/plugins/setpoint_position.cpp** a position can be sent to the
pixhawk with the mavlink message (set-position-target-local-ned)[http://ardupilot.org/dev/docs/copter-commands-in-guided-mode.html#copter-commands-in-guided-mode-set-position-target-local-ned].

```cpp
set_position_target_local_ned(stamp.toNSec() / 1000000,
          utils::enum_value(MAV_FRAME::LOCAL_NED),
					ignore_all_except_xyz_y,
					p,
					Eigen::Vector3d::Zero(),
					Eigen::Vector3d::Zero(),
					ftf::quaternion_get_yaw(q), 0.0);
```
This message is received by the px4 mavlink process. You can see this in
**src/modules/mavlink/mavlink_receiver.cpp**

```cpp
case MAVLINK_MSG_ID_SET_POSITION_TARGET_LOCAL_NED:
  handle_message_set_position_target_local_ned(msg);
  break;
```

The mavlink message is processed in the **handle_message_set_position_target_local_ned** which publishes
the result on a uORB topic.

```cpp
if (_pos_sp_triplet_pub == nullptr) {
  _pos_sp_triplet_pub = orb_advertise(ORB_ID(position_setpoint_triplet), &pos_sp_triplet);
} else {
  orb_publish(ORB_ID(position_setpoint_triplet), _pos_sp_triplet_pub, &pos_sp_triplet);
}
```

The position_setpoint_triplet is further processed by anyone who subscribes to the ORB publisher.
It looks like the navigator module takes care of further processing this commanded.

**src/modules/navigator/navigator_main.cpp**
```cpp
void Navigator::publish_vehicle_cmd(const struct vehicle_command_s &vcmd)
{
	if (_vehicle_cmd_pub != nullptr) {
		orb_publish(ORB_ID(vehicle_command), _vehicle_cmd_pub, &vcmd);

	} else {
		_vehicle_cmd_pub = orb_advertise_queue(ORB_ID(vehicle_command), &vcmd, vehicle_command_s::ORB_QUEUE_LENGTH);
	}
}
```

# Mixers

* Folder **Firmware/ROMFS/px4fmu_common/init.d**
* file: 50002_traxxas_stampede_2wd (for throttle and steering)
* Folder **Firmware/ROMFS/px4fmu_common/mixers/**


# devices

* /dev/ttyACM0 is a USB communication device (CDC) of sub-type "abstract control model" (ACM).
* /dev/ttyAMA0 is the Broadcom UART (appears as under Linux).


# Resources

* [building-px4-for-linux-with-make](http://ardupilot.org/dev/docs/building-px4-for-linux-with-make.html)
* [px4 gazebo simulation](https://dev.px4.io/en/simulation/gazebo.html)
* [Mavros and gazebo simulation](https://dev.px4.io/en/simulation/ros_interface.html)

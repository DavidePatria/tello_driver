# tello_driver


ROS driver wrapper for DJI/Ryze Tello drone

Node: [src/tello_driver_node.py](src/tello_driver_node.py)

Topics:
* `~cmd_vel`: [geometry_msgs/Twist](http://docs.ros.org/api/geometry_msgs/html/msg/Twist.html)
* `~fast_mode`: [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* `~image_raw`: [sensor_msgs/Image](http://docs.ros.org/api/sensor_msgs/html/msg/Image.html)
* `~takeoff`: [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* `~throw_takeoff`: [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* `~land`: [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* `~palm_land`: [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* `~flattrim`: [std_msgs/Empty](http://docs.ros.org/api/std_msgs/html/msg/Empty.html)
* `~flip`: [std_msgs/Uint8](http://docs.ros.org/api/std_msgs/html/msg/UInt8.html)

Parameters:
* `~tello_ip`
* `~tello_cmd_port`
* `~client_port`
* `~connect_timeout_sec`

## Installation
* `$ cd <CATKIN_WS/SRC>`
* `$ git clone https://github.com/anqixu/TelloPy.git`
* `$ cd TelloPy`

using a virtual environment for python this is the sane thing to do, previously it was `sudo -H pip...`, big no no.
* `$ pip install -e .`
* `$ cd ..`
* `$ git clone https://github.com/anqixu/h264_image_transport.git`
* `$ git clone https://github.com/anqixu/tello_driver.git`
* `$ cd ..`
* `$ rosdep install h264_image_transport`
* `$ catkin build tello_driver`

Optionally, install the [following udev rules](https://github.com/anqixu/sixad_rumble/blob/master/misc/10-gamepads.rules) for PS3 gamepads; see instructions in comments on top of file.

## Running the driver

* turn on drone and wait for its front lights to blink amber
* connect WiFi to drone's access point (e.g. `TELLO_######`)
* `$ roslaunch tello_driver launch/tello_node.launch`

To see the camera:
* `$ rosrun rqt_image_view rqt_image_view /tello/image_raw/compressed`

This doesn't work apparently, but the camera is still accessible using *rviz* and subscribing to the topic.

## Tested use-case

Launching `roslaunch tello_driver tello_node.launch` will start a node and connect to the drone. Then the usual topics will be available to receive publications.
No controller was availble when testing the modified package.

## Known bugs
* Sometimes, perhaps when taking off without moving gamepad analog sticks / sending commands to `/tello/cmd_vel`, further cmd_vel will not work; fix by restarting node, moving gamepad analog sticks / send a message to `/tello/cmd_vel` FIRST, then takeoff

## Disclaimer:
This was modified for personal needs and shared since a desperate attempt worked and the basic functions of the drone were fine. I'm not deep into the development of this package and cannot do much about other problems.
Refer to the original repository for more details.

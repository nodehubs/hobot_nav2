English| [简体中文](./README_cn.md)

# Feature Introduction

Taking the sweeping robot as an example, how to thoroughly clean every place in the house? How to avoid known obstacles such as walls, wardrobes, etc. on the map? It's easy to deal with static obstacles, but what if there are naughty kids or pets, as well as various debris that occasionally appear on the floor, how should the robot avoid them one by one? These issues require a set of intelligent autonomous navigation algorithms to solve.

Autonomous navigation function runs through most of the movement process of mobile robots, and it is also a crucial basic skill in intelligent mobile robots. Robots can plan walking paths effectively based on map information, and they also need to recognize surrounding obstacles in real-time through lidar or cameras. Once unexpected obstacles appear, immediate avoidance actions need to be taken.

# Bill of Materials

The following robots are all compatible with RDK X3

| Robot Name             | Manufacturer | Reference Link                                               |
| :--------------------- | ----------- | ------------------------------------------------------------ |
| OriginBot Smart Robot   | Guyueju     | [Click Here](https://www.originbot.org/)                      |
| X3 Sweeping Robot      | Lunqu Tech  | [Click Here](https://item.taobao.com/item.htm?spm=a230r.1.14.17.55e556912LPGGx&id=676436236906&ns=1&abbucket=12#detail) |
| Tracked Smart Vehicle   | Weixue Electronics | [Click Here](https://detail.tmall.com/item.htm?abbucket=9&id=696078152772&rn=4d81bea40d392509d4a5153fb2c65a35&spm=a1z10.5-b-s.w4011-22714387486.159.12d33742lJtqRk) |
| RDK X3 Robot           | Various Manufacturers | [Click Here](https://developer.horizon.ai/sunrise) |

# Instructions for Use

## Preparation

1. The robot has a mobile chassis, camera, and RDK kit. The hardware is already connected and tested.
2. ROS low-level drivers are installed, and the robot can receive "/cmd_vel" commands to move correctly according to the command.
3. Lidar driver is installed and able to publish /scan topics normally.
4. PC computer has completed the installation of Ubuntu, ROS Foxy/Humble.

## Install the hobot-nav2 package

After starting the robot, connect to the robot via terminal or VNC, click the "One-click Deployment" button on [NodeHub hobot-nav2](http://it-dev.horizon.ai/nodehubDetail/170117036053371397) website, and copy the following command to run on the RDK system to install the hobot-nav2 package.

```bash
sudo apt update
sudo apt install -y tros-hobot-nav2
```

## Run nav2

Taking OriginBot as an example here, the commands to execute in the first three steps may vary for robots of different categories.

**1. Start the robot's chassis**

Start the robot and connect to it via terminal or VNC. The startup command for OriginBot is as follows:

```bash
# Set the environment variables for tros
source /opt/tros/setup.bash

# Set the environment variables for ROS
source /opt/ros/foxy/setup.bash
```# Launch OriginBot
ros2 launch originbot_base robot.launch.py
```

**2. Start the LiDAR**

Connect to the robot via terminal or VNC, and the command to start the LiDAR is as follows:

```bash
# Set the environment variables for tros
source /opt/tros/setup.bash

# Set the environment variables for ROS
source /opt/ros/foxy/setup.bash

# Launch the LiDAR
ros2 launch ydlidar_ros2_driver ydlidar_launch.py
```

**3. Launch nav2**

After starting the robot, connect to the robot via terminal or VNC, click the "One-click Deployment" button at the top right of this page, copy and run the following command on the RDK system to install Nodes:

```bash
# Set the environment variables for tros
source /opt/tros/setup.bash

# Set the environment variables for ROS
source /opt/ros/foxy/setup.bash

# Launch nav2
ros2 launch hobot_nav2 hobot_nav2_bringup.launch.py
```

**4. Visualize Navigation Process**

To monitor the robot's navigation process conveniently, start the Rviz visualization software on a PC in the same network:

```bash
# Modify the path here according to the ROS version being used
source /opt/ros/foxy/setup.bash

ros2 launch nav2_bringup rviz_launch.py
```

Once the navigation is launched, the robot initially doesn't know where it is. By default, Nav2 will wait for the user to provide an approximate starting location for the robot. Check the robot's position in Gazebo, find that location on the map, click the "2D Pose Estimate" button in Rviz2, then set the initial position of the robot by clicking at the estimated location on the map. Drag the location clicked forward to set the initial moving direction for the robot.

> **Note:**
>After starting the navigation, continuous output information will be seen in the terminal because the initial pose of the robot has not been set. Once the initial position is set, the log refreshing will stop.

Click the "2D Goal Pose" button to select the target location, then you can start autonomous navigation on the map.

![e69be30fab](image/e69be30fab.gif)


# Interface Description

For information on interfaces and parameter adjustments, please refer to the official NAV2 documentation [NAV2 Parameter Adjustment Guide](https://navigation.ros.org/setup_guides/index.html)


# References

- NAV2 Official Documentation: [Click here to jump](https://navigation.ros.org/index.html)


# Frequently Asked Questions

None at the moment
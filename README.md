# Turtlebro navigation stack

This package provides a wrapper for the standard ROS navigation stack, and stores parameters specifically tailored for Voltbro robots.   
The package provides the ability to construct a terrain map from lidar data using the standard ROS gmapping package.  
The package also provides the possibility of autonomous movement according to lidar data using the ROS movebase package.
It is preinstalled and is already on the Linux image supplied with the robot.   

For more information see:  
- ROS navigation: http://wiki.ros.org/navigation   
- Gmapping: http://wiki.ros.org/gmapping  
- Voltbro course about navigation: http://learn.voltbro.ru/  
 
## Setup

```
export ROVER_MODEL=turtlebro
-or-
export ROVER_MODEL=brover
```
It\`s tune at turtlebro RaspberryPi firmware.


## Launch

##### Note:
You have to clear all previous odometry data from robot to use map building and navigation:
```
rosservice call /reset
```

#### Launch navigation and mapping
Run in autonomous navigation mode and map building:  
```
roslaunch turtlebro_navigation turtlebro_slam_navigation.launch open_rviz:=0
```
It will launch move_base and slam_gmapping nodes both. in that mode you can set goals to robot through rviz on your PC.  
Just set correct ROS_MASTER_URI and ROS_HOSTNAME in console on your pc and run rviz. Then Add->By Topic->/map and you will be able to see robot`s map. You can add new goal to robot using 2D Nav Goal button on the top of rviz window.  


#### Navigation on existing map 
If you want to run navigation on pre-builded map:  
```
roslaunch turtlebro_navigation turtlebro_map_navigation.launch
```

#### Build map only
If you want to build map, but you want to move turtlebot without move_base package, for example with joystick:  
```
roslaunch turtlebro_navigation turtlebro_gmapping.launch
```

#### Save map file
if you want to save map after some time of navigation:    
```
rosrun map_server map_saver -f mymap
```

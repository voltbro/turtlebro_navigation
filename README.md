# Turtlebro navigation stack

## Setup

```
export ROVER_MODEL=turtlebro
-or-
export ROVER_MODEL=brover
```



## Build

```
catkin_make --pkg turtlebro_navigation
```

## Launch

#### Slam and move_base 
```
roslaunch turtlebro_navigation turtlebro_slam_navigation.launch
```

#### Navigation on exist map 
```
roslaunch turtlebro_navigation turtlebro_map_navigation.launch
```

build map
```
roslaunch turtlebro_navigation turtlebro_gmapping.launch
```

Save map file
```
rosrun map_server map_server -f mymap
```

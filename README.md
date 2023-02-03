# Пакет навигации turtlebro_navigation для роботов компании "Братья Вольт"

Этот пакет предоставляет оболочку для стандартного навигационного стека ROS и хранит параметры, специально разработанные для роботов компании "Братья Вольт".   
Пакет предоставляет возможность построения карты местности на основе данных лидара с использованием стандартного пакета ROS gmapping.  
Пакет также предоставляет возможность автономного перемещения по данным лидара с использованием пакета ROS move_base.
Он предустановлен и уже находится в образе операционной системы, поставляемом вместе с роботами.

Для получения дополнительной информации смотрите:
- Стек навигации ROS: http://wiki.ros.org/navigation   
- Стек картографирования Gmapping: http://wiki.ros.org/gmapping  
- Курс по навигации от "Братья Вольт": http://learn.voltbro.ru/data/ros-navigation/ 
 
## Установка пакета

По умолчанию пакет навигации уже настроен на работу с используемым типо робота TurtleBro/BRover V.4. В случае, если вам необходимо изменить тип используемого робота, воспользуйтесь следующими командами:

```
export ROVER_MODEL=turtlebro

-или-

export ROVER_MODEL=brover
```

## Запуск навигации


##### Важная заметка:

Перед запуском рекомендуется сбрасывать показания одометрии для использования навигации и построения карты:
```
rosservice call /reset
```

__Запуск навигации в режиме SLAM__

SLAM (англ. simultaneous localization and mapping — одновременная локализация и построение карты) — метод, используемый в мобильных автономных средствах для построения карты в неизвестном пространстве или для обновления карты в заранее известном пространстве с одновременным контролем текущего местоположения и пройденного пути.

Для запуска навигации в режиме SLAM необходимо выполнить на роботе следующую команду:  

```
roslaunch turtlebro_navigation turtlebro_slam_navigation.launch open_rviz:=0
```

Лаунч-файл запустит обе ноды move_base и slam_gmapping. В этом режиме вы можете устанавливать цели для робота через RViz на компьютере.

__Установка __

Just set correct ROS_MASTER_URI and ROS_HOSTNAME in console on your pc and run rviz. 
```
export ROS_MASTER_URI=http://<IP-address_robot>:11311/
export ROS_HOSTNAME=IP-address_PC

rviz
```

Then Add->By Topic->/map and you will be able to see robot`s map. You can add new goal to robot using 2D Nav Goal button on the top of rviz window.  


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

Plymouth's Pepper ROS nodes
===========================

Bringing it up
--------------

- ``export NAO_IP=<pepper IP>``
- ``ssh nao@<pepper IP>``, then:
```
$ nao stop
$ naoqi-bin --disable-life
```
- ``ssh nao@<pepper IP>``, then:
```
qicli call ALMotion.wakeUp
```

Finally:
```
roslaunch pepper_bringup pepper_full.launch
```

Teleop
------

Required packages:
- ``ros-<version>-joy``
- ``nao_teleop``: http://wiki.ros.org/nao_teleop

Then:
```
$ roslaunch nao_teleop teleop_joy.launch
```

Note: to enable the joystick control, press button **10** on the joystick, not
9.

Mapping
-------

Using `gmapping`
```
$ rosrun gmapping slam_gmapping scan:=/pepper_robot/laser _odom_frame:=/odom _angularUpdate:="0.1" _linearUpdate:="0.1" _map_update_interval:="2" _maxRange:="1.5" _maxUrange:="1.3" _temporalUpdate:="0.5" _xmax:="10" _xmin:="-10" _ymax:="10" _ymin:="-10" _particles:="300" _delta:="0.02"
```

Localisation
------------

First, the map server:

```
$ rosrun map_server map_server <path to map>/map.yaml
```

Then, AMCL:
```
$ rosrun amcl amcl scan:=/pepper_robot/laser
```

Navigation
----------

```
roslaunch pepper_plymouth_ros nav.launch
```

3D Perception
-------------

![doc/rgbd_pepper.png](Registered depth cloud)

Until it is officially released, you might need to manually install ``pepper_bringup`` with the perception
launch file: [https://github.com/ros-naoqi/pepper_robot/pull/27](get it here).

Then it works 'out of the box'.

Building a 3D voxel octomap
---------------------------

![doc/octomap_pepper.png](Octomap building with Pepper + ROS)

You need the 3D perception pipeline up and running. See above.

- First:
``` 
$ sudo apt install ros-kinetic-octo*
```

- then install by hand [https://github.com/OctoMap/octomap_mapping](octomap_mapping)
- then:
```
$ roslaunch pepper_plymouth_ros octomap_mapping.launch
```


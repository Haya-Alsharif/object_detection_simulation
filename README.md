# object_detection_simulation
A simple simulation enviroment of one person and iris drone with downward looking camera. 

## Required packages:
To use it make sure you have the following pakages:
1) **PX4 avoidane:** I only use this to plan a path to the person model in gazebo world
2) **PX4 Firmware:** to get the iris drone model and to use the avoidance package
3) **darknet_ros:** to run yolo NN for object detection
4) **Tarek's object localization**: contact Tarek to get the package.


## Required modifications:
1) update camera intrensic paramters in Tarek's package to the values you obtain by: 
```
rostopic echo /down_camera/rgb/camera_info -n1 | grep K:
```

2) Instead of going into Tarek's package and changing the camera frame_id to the one used in the simulator, I added the following transformation in `object_detection_simulation.launch`. Make sure that the topic frame_id used in Tarek's package is `zed_left_camera_optical_frame`.
```
<node pkg="tf" type="static_transform_publisher"    name="zed_to_simulation_frame"    args="0 0 0 0 0 0 $(arg down_frame_id) zed_left_camera_optical_frame 40"/>
```

## Build and launch:
```
cd catkin_ws/src/
git clone https://github.com/Haya-Alsharif/object_detection_simulation.git
cd ..
catkin build object_detection_simulation
source devel/setup.bash
roslaunch object_detection_simulation object_detection_simulation.launch 
```

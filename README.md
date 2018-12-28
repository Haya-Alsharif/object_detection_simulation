# object_detection_simulation

A simple simulation enviroment of one person and iris drone with downward looking camera. To use it make sure you have the following:
1) **PX4 avoidane:** I only use this to plan a path to the person model in gazebo world
2) **PX4 Firmware:** to get the iris drone model and to use the avoidance package
3) **darknet_ros:** to run yolo NN for object detection
4) **Tarek's object localization pakage**.

Also make sure that
1) update camera intrensic paramters in Tarek's package to the values you obtain by: 
```
rostopic echo /down_camera/rgb/camera_info -n1 | grep K:
```

2) Instead of going into Tarek's package and changing the camera frame_id to the one used in the simulator, I added the following transformation: 
```
<node pkg="tf" type="static_transform_publisher"    name="zed_to_simulation_frame"    args="0 0 0 0 0 0 $(arg down_frame_id) zed_left_camera_optical_frame 40"/>
```
Make sure that the topic frame_id used in Tarek's package is `zed_left_camera_optical_frame`.

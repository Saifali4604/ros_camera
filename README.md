# ros_camera
you can install the camera package either by catkin_make in to your works space or directly downloading
# Directly Download
## step 1:  Normal camera drivers
Install usb_cam ROS node with needed dependencies:
```sudo apt install ros-noetic-usb-cam```

Check if camera was recognized by system:

```lsusb``` 

```ls /dev | grep video*```
```
cd /
cd /opt/ros/noetic/share/usb_cam/launch/
sudoedit usb_cam-test.launch
```
**4th line:** change video ID in the.

**5th line:** change image width as per the camera

**6th line:** change image hieght s per the camera

**add**  ```<node pkg="tf" type="static_transform_publisher" name="camera_frames_pub" args="0.05 0.0 0.1 0 0 0 /base_link /camera 35"/>``` before ```</launch>```


**ctrl + x** then **press y** to save and **press enter**.

```
cd
git clone https://github.com/Saifali4604/ros_camera && cp -r ros_camera/camera_info .ros && rm -rf ros_camera
```

**Run the package**
```roslaunch usb_cam usb_cam-test.launch```

## step 2: ROS opencv camera drivers
Install usb_cam ROS node with needed dependencies:
```
sudo apt update 
sudo apt install ros-noetic-cv-camera
```

Check if camera was recognized by system:
```lsusb``` 
```ls /dev | grep video*```
```
cd /
cd /opt/ros/noetic/share/cv_camera/
sudo touch launch
cd launch
sudo nano cv-test.launch
```

add 
```
<launch>
  <node pkg="cv_camera" type="cv_camera_node" name="cv_camera" output="screen"/>
  <node pkg="tf" type="static_transform_publisher" name="camera_frames_pub" args="0.05 0.0 0.1 0 0 0 /base_link /camera 35"/>
</launch>
```

**ctrl + x** then **press y** to save and **press enter**.

```
cd
git clone https://github.com/Saifali4604/ros_camera && cp -r ros_camera/camera_info .ros && rm -rf ros_camera
```


**Run the package**
```roslaunch cv_camera cv-test.launch```


**Viewing in RVIZ**
```rviz``` go to ```by topic``` and click on ```image``` 
change the frmae to ```base_link```

# Calibration
## Option 1
(ROS WIKI)[https://wiki.ros.org/camera_calibration/Tutorials/MonocularCalibration]

(Youtube Video)[https://www.youtube.com/watch?v=UGArg1kQwFc&t=434s]
```
rosdep install camera_calibration
roslaunch usb_cam usb_cam-test.launch
rosrun camera_calibration cameracalibrator.py --size 8x6 --square 0.108 image:=/usb_cam/image_raw camera:=/usb_cam
```




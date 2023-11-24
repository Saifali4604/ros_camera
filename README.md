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
4th line: change video ID in the
5th line: change image width by 1280
6th line: change image hieght by 720
add 
```<node pkg="tf" type="static_transform_publisher" name="camera_frames_pub" args="0.05 0.0 0.1 0 0 0 /base_link /camera 35"/>``` before ```</launch>```
ctrl + x then press y to save and press enter.

**Run the package**
```roslaunch usb_cam usb_cam-test.launch```

**Viewing in RVIZ**
```rviz``` go to ```by topic``` and click on ```image``` 
change the frmae to ```base_link```

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
ctrl + x then press y to save and press enter.

**Run the package**
```roslaunch cv_camer cv-test.launch```

**Viewing in RVIZ**
```rviz``` go to ```by topic``` and click on ```image``` 
change the frmae to ```base_link```
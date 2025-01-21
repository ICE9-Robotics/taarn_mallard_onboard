# taarn_mallard_onboard

# Dependencies

Make sure all dependencies are configured according to the following guide before build the package. Some of these packages need extra procedures or specific versions to work. See below for installation instructions

### 1. MallARD
ice9-dev branch (may later be merged into master)
```
git clone -b ice9-dev git@github.com:EEEManchester/MallARD.git
```

### 2. visual_virtual_tether
```
git clone git@github.com:EEEManchester/visual_virtual_tether.git
```

### 3. microstrain_inertial
```
git clone --recursive -b ba60f4a46f107a19ea7c321c44507198660fdcff https://github.com/LORD-MicroStrain/microstrain_inertial.git
```
We need to checkout to specific commits that work for us (newest may not build properly)
```
cd microstrain_inertial
git checkout ba60f4a46f107a19ea7c321c44507198660fdcff
cd microstrain_inertial_driver/microstrain_inertial_driver_common/include/microstrain_inertial_driver_common
git checkout 80378f949792743bdc15de1c549e7ff28d00004e
```

### 4. hector_slam
This is not the official hector_slam but modified for MallARD with added ros services for fixing map.
```
git clone -b mallard https://github.com/EEEManchester/hector_slam.git
```
#### Note
If `catkin build` complains about QT version:
```
Found unsuitable Qt version "" from NOTFOUND, this code requires Qt 4.x
```
You may need to remove the hector_slam/hector_geotiff and hector_slam/hector_geotiff_plugins packages - we don't need them anyways - and the build folder then rebuild
```
cd hector_slam
rm -r hector_geotiff hector_geotiff_plugins
```

### 5. mavros & mavlink
```
git clone -b 1.15.0 https://github.com/mavlink/mavros.git
git clone -b 1.0.9 https://github.com/mavlink/mavlink.git
```

### 6. Others
Install standard ROS packages: usb_cam, apriltag_ros, sick_tim
```
sudo apt install ros-melodic-usb-cam=0.3.7-1bionic.20230322.235948
sudo apt install ros-melodic-apriltag-ros=3.2.1-1bionic.20221025.223206
sudo apt install ros-melodic-sick-tim=0.0.17-1bionic.20230524.174840
```

# Build
```
rosdep install --from-paths src -i -r
catkin build
```

# Udev rule
Copy and apply udev rules for the downward facing camera. If a new camera is used, make sure udev rule is updated with the correct idVendor and idProduct.
```
sudo cp install/99.camera.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules; sudo udevadm trigger
```

# Run
```
roslaunch taarn_mallard_onboard mallard_onboard.launch
```

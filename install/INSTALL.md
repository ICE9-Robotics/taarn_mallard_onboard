# Install

1. Make catkin workspace and cd into
```
mkdir -p ~/mallard_ws/src
cd ~/mallard_ws/src
```

2. Clone all repositories
```
git clone git@github.com:EEEManchester/taarn_mallard_onboard.git
git clone -b ice9-dev git@github.com:EEEManchester/MallARD.git
git clone git@github.com:EEEManchester/visual_virtual_tether.git
git clone --recursive -b ba60f4a46f107a19ea7c321c44507198660fdcff https://github.com/LORD-MicroStrain/microstrain_inertial.git
git clone -b mallard https://github.com/EEEManchester/hector_slam.git
git clone -b 1.15.0 https://github.com/mavlink/mavros.git
git clone -b 1.0.9 https://github.com/mavlink/mavlink.git
git clone https://github.com/EEEManchester/apriltag_ros.git
```

3. Remove some files from hector slam that we don't need but requires additional dependencies
```
cd hector_slam
rm -r hector_geotiff hector_geotiff_plugins
```

4. Install standard ros packages
```
sudo apt install ros-melodic-usb-cam=0.3.7-1bionic.20230322.235948
sudo apt install ros-melodic-sick-tim=0.0.17-1bionic.20230524.174840
```

5. cd workspace root dir and build
```
cd ..
rosdep install --from-paths src -i -y
catkin_make
```

Note if microstrain_inertial fails to build, try switching to an older commit and rebuild:
```
cd src/microstrain_inertial
git checkout ba60f4a46f107a19ea7c321c44507198660fdcff
cd microstrain_inertial_driver/microstrain_inertial_driver_common/include/microstrain_inertial_driver_common
git checkout 80378f949792743bdc15de1c549e7ff28d00004e
cd ..
catkin_make
```

6. Source and config bashrc
```
source devel/setup.bash
echo "source ~/devel/setup.bash" >> ~/.bashrc
```

7. Copy udev rules
Copy and apply udev rules for the downward facing camera. If a new camera is used, make sure udev rule is updated with the correct idVendor and idProduct.
```
sudo cp src/taarn_mallard_onboard/install/99.camera.rules /etc/udev/rules.d/
sudo udevadm control --reload-rules; sudo udevadm trigger
```

# Instructions

1. Make catkin workspace and cd into
```
mkdir -p ~/mallard_ws/src
cd ~/mallard_ws/src
```

2. Clone all repositories
```
git clone git@github.com:EEEManchester/taarn_mallard_onboard.git
git clone -b ice9-dev git@github.com:ICE9-Robotics/MallARD.git
git clone git@github.com:EEEManchester/visual_virtual_tether.git
git clone git@github.com:EEEManchester/taarn_mallard_onboard.git
git clone --recursive -b ba60f4a46f107a19ea7c321c44507198660fdcff https://github.com/LORD-MicroStrain/microstrain_inertial.git
git clone -b mallard https://github.com/EEEManchester/hector_slam.git
git clone -b 1.15.0 https://github.com/mavlink/mavros.git
git clone -b 1.0.9 https://github.com/mavlink/mavlink.git
```

3. Remove some files from hector slam that we don't need but requires additional dependencies
```
cd hector_slam
rm -r hector_geotiff hector_geotiff_plugins
```

4. Install standard ros packages
```
sudo apt install ros-melodic-usb-cam=0.3.7-1bionic.20230322.235948
sudo apt install ros-melodic-apriltag-ros=3.2.1-1bionic.20221025.223206
sudo apt install ros-melodic-sick-tim=0.0.17-1bionic.20230524.174840
```

5. cd workspace root dir and build
```
cd ..
rosdep install --from-paths src -i -y
catkin_make
source devel/setup.bash
echo "source ~/devel/setup.bash" >> ~/.bashrc
```

6. Copy udev rules
```
sudo cp src/taarn_mallard_onboard/install/99.camera.rules /etc/udev/rules.d/
```

7. launch bluerov
```
roslaunch taarn_mallard_onboard mallard_onboard.launch
```

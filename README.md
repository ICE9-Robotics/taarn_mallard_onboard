# taarn_mallard_onboard

# Dependencies

Make sure all dependencies are configured according to the following guide before build the package.All of these packages need extra procedures or specific versions to work, apart from the `usb_cam`.
- MallARD
- microstrain_inertial
- hector_slam
- mavros & mavlink
- usb_cam (through `apt install` route)

## MallARD
Xueliang modified MallARD on `Xueliang` branch
```
git clone -b Xueliang git@github.com:EEEManchester/MallARD.git
```
## microstrain_inertial
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
## hector_slam
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

## mavros
```
git clone -b 1.15.0 https://github.com/mavlink/mavros.git
git clone -b 1.0.9 https://github.com/mavlink/mavlink.git
```
## usb_cam
```
sudo apt install ros-$ROS_DISTRO-usb-cam
```

# Build
```
rosdep install --from-paths src -i -r
catkin build
```

# Run

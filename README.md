# taarn_mallard_onboard

# Instructions
See [install/Instruction.md](install/Instruction.md)

# Dependencies
- MallARD
- visual_vertual_tether
- microstrain_inertial
- hector_slam
- sick_tim
- mavros & mavlink
- usb_cam
- apriltag_ros (UOM modified)

See Instructions for details.

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

# Install

1. Make catkin workspace and cd into
```
mkdir -p ~/mallard_ws/src
cd ~/mallard_ws/src
```

2. Clone all repositories
```
git clone git@github.com:ICE9-Robotics/taarn_mallard_onboard.git
git clone -b ice9-dev git@github.com:ICE9-Robotics/MallARD.git
git clone git@github.com:ICE9-Robotics/visual_virtual_tether.git
git clone -b 1.15.0 https://github.com/mavlink/mavros.git
git clone -b 1.0.9 https://github.com/mavlink/mavlink.git
git clone https://github.com/EEEManchester/apriltag_ros.git
```

3. cd workspace root dir and build
```
cd ..
rosdep install --from-paths src -i -y
catkin_make
```

4. Source and config bashrc
```
source devel/setup.bash
echo "source ~/mallard_ws/devel/setup.bash" >> ~/.bashrc
```

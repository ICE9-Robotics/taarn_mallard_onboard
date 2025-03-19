# taarn_mallard_onboard

# Dependencies
- MallARD
- visual_vertual_tether
- mavros & mavlink
- apriltag_ros (UOM modified)

# Install
See [install/INSTALL.md](install/INSTALL.md)

# SITL setup
MallARD is set to udp 127.0.0.2:1455x
```xml
<arg name="fcu_url" default="udp://127.0.0.2:14550@udp://127.0.0.2:14555" />
```

Start SITL with:
```shell
sim_vehicle.py --console -v ArduSub -f mallard --out=127.0.0.2:14550 -I1
```

Type `output` in the terminal, you should see:
```
MANUAL> 2 outputs
0: xxx.xxx.xxx.xxx:xxxxx
1: 127.0.0.2:14550
```

# Run
```
roslaunch taarn_mallard_onboard mallard_onboard.launch
```

## SITL test
You should be able to ARM Bluerov now:
```
rosservice call /mallard/mavros/cmd/arming "value: true"
```
The output should be:
```
success: True
result: 0
```
You can also see heartbeat messages at 1 Hz from ros topic
```
rostopic echo /mallard/mavros/state
```

rosservice call /mavros/cmd/arming "value: true"
rosservice call /mavros/cmd/takeoff "{min_pitch: 0.0, yaw: 0.0, latitude: 47.3977508, longitude: 8.5456074, altitude: 2.5}"
rostopic pub -r 10 /mavros/setpoint_position/local geometry_msgs/PoseStamped "header:
  auto
pose:
  position:
    x: 0.0
    y: 0.0
    z: 0.0
  orientation:
    x: 0.0
    y: 0.0
    z: 0.0
    w: 0.0"

rosservice call /mavros/set_mode "base_mode: 0 custom_mode: 'OFFBOARD'"


## ROS 노드 실행 및 관리
### ROS Core 노드 실행
```
$ roscore
```
### MAVROS 노드 실행
```
$ roslaunch mavros px4.launch
#roslaunch mavros px4.launch fcu_url:="udp://:14540@192.168.88.53:14557" gcs_url:="udp://@192.168.88.53"
# roslaunch mavros px4.launch fcu_url:="/dev/ttyTHS1:921600" gcs_url:="udp://@192.168.88.53"
```
### 토픽 목록
```
$ rostopic list
```

## ROS 노드 토픽 명령
### state
```
$ rostopic echo /mavros/state
```

### LOCAL_POSITION 확인
```
$ rostopic echo /mavros/local_position/pos
```

### Mode 설정
```
# https://github.com/mavlink/mavros/blob/master/mavros_msgs/srv/SetMode.srv
# http://wiki.ros.org/mavros/CustomModes
# Manual Mode

rosservice call /mavros/set_mode "base_mode: 64
custom_mode: ''"

rosservice call /mavros/set_mode "base_mode: 0
custom_mode: 'MANUAL'"

rosservice call /mavros/set_mode "base_mode: 0
custom_mode: 'POSCTL'"

rosservice call /mavros/set_mode "base_mode: 0
custom_mode: 'OFFBOARD'"

rosservice call /mavros/set_mode "base_mode: 0
custom_mode: 'AUTO.LAND'"
```

1. ARM 모드 설정
- rosservice call /mavros/cmd/arming "value: true"

2. Take off
rosservice call /mavros/cmd/takeoff "{min_pitch: 0.0, yaw: 0.0, latitude: 47.3977508, longitude: 8.5456074, altitude: 2.5}"

3. mavros/setpoint_position 을 이용 - 위치 지정 (이동)  
- OFF Board 모드에서 동작
```
rostopic pub -r 10 /mavros/setpoint_position/local geometry_msgs/PoseStamped "header:
  auto
pose:
  position:
    x: 0.0
    y: 0.0
    z: 10.0
  orientation:
    x: 0.0
    y: 0.0
    z: 0.0
    w: 0.0"
```

4. SETPOINT_VELOCITY
- OFFBOARD 모드에서 동작

```
$ rostopic pub -r 10 /mavros/setpoint_velocity/cmd_vel geometry_msgs/TwistStamped "{header: auto, twist: {linear: {x: 10.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 0.0}}}"
```

5. OFFBOARD 모드 변환
- rosservice call /mavros/set_mode "base_mode: 0 custom_mode: 'OFFBOARD'"

# ROS 노드 만들기
## 새로운 노드 만들기
### 패키지 생성
```
$ source ~/catkin_ws/devel/setup.bash
$ cd ~/catkin_ws/src
$ catkin_create_pkg drone_control mavros sensor_msgs roscpp
```

### 노드 코드 작성
- example

- ~~/catkin_ws/src/drone_control/src/drone_state.cpp~
```{.cpp}
#include "ros/ros.h"
#include "sensor_msgs/Imu.h"

void imuDataCallback(const sensor_msgs::Imu::ConstPtr& msg){
  ROS_INFO("\nlinear acceleration\
      \nx: [%f]\ny:[%f]\nz:[%f]", msg->linear_acceleration.x,
      msg->linear_acceleration.y, msg->linear_acceleration.z);
}

int main(int argc, char **argv){
  ros::init(argc, argv, "drone_state");
  ros::NodeHandle nh;
  ros::Subscriber sub = nh.subscribe("/mavros/imu/data", 1000, imuDataCallback);
  ros::spin();
  return 0;
}
```

- 빌드 스크립트 추가
- ~~/catkin_ws/src/drone_control/CMakeLists.txt~ 파일 끝에 다음 3줄 추가
```
include_directories(include ${catkin_INCLUDE_DIRS})
add_executable(drone_state src/drone_state.cpp)
target_link_libraries(drone_state ${catkin_LIBRARIES})
```
- 환경 변수 다시 로드!
```
$ source ~/catkin_ws/devel/setup.bash
```
### 패키지 빌드
```
$ cd ~/catkin_ws
$ catkin build
```

### 패키지 노드 실행
- drone_control 패키지의 drone_state 노드 실행
```
$ rosrun drone_control drone_state
```


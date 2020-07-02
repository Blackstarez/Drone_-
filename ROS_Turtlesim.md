## 1. 환경 변수 설정

```{.no-highlight}
$ source /opt/ros/melodic/setup.bash
```

## 2. roscore 실행
 - roscore: Master + rosout + parameter server
  - Master: 네임 서비스
  - rosout: stdout/stderr 로깅
  - parameter server: 파라미터 저장 서버

```
$ roscore
```

## 3. turtlesim 패키지의 turtlesim_node 실행
```
$ rosrun turtlesim turtlesim_node
```

## 4. turtlesim 패키지의 turtle_teleop_key 실행
```
rosrun turtlesim turtle_teleop_key
```

### Turtlesim 노드 목록

```
rosnode list
```

/rosout : ROS 메시지 로깅.

### Turtlesim 토픽 목록
```
rostopic list
```

### Turtlesim 토픽 정보

```
rostopic info /turtle1/cmd_vel
```

### Turtlesim 메시지 정보

```
$ rosmsg info geometry_msgs/Twist
geometry_msgs/Vector3 linear
  float64 x
  float64 y
  float64 z
geometry_msgs/Vector3 angular
  float64 x
  float64 y
  float64 z
```

or

```
rosed geometry_msgs Twist.msg
```
1. 환경 변수 설정

#+begin_src sh
$ source /opt/ros/melodic/setup.bash
#+end_src

2. roscore 실행
 - roscore: Master + rosout + parameter server
  - Master: 네임 서비스
  - rosout: stdout/stderr 로깅
  - parameter server: 파라미터 저장 서버

#+begin_src sh
$ roscore
#+end_src

3. turtlesim 패키지의 turtlesim_node 실행
#+begin_src sh
$ rosrun turtlesim turtlesim_node
#+end_src

4. turtlesim 패키지의 turtle_teleop_key 실행
#+begin_src sh
rosrun turtlesim turtle_teleop_key
#+end_src

*** Turtlesim 노드 목록

#+begin_src sh
rosnode list
#+end_src

/rosout : ROS 메시지 로깅.

*** Turtlesim 토픽 목록
#+begin_src sh
rostopic list
#+end_src

*** Turtlesim 토픽 정보

#+begin_src sh
rostopic info /turtle1/cmd_vel

#+end_src

*** Turtlesim 메시지 정보

#+begin_src sh
$ rosmsg info geometry_msgs/Twist
geometry_msgs/Vector3 linear
  float64 x
  float64 y
  float64 z
geometry_msgs/Vector3 angular
  float64 x
  float64 y
  float64 z
#+end_src

or

#+begin_src sh
rosed geometry_msgs Twist.msg
#+end_src
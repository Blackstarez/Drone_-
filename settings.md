# How to Setting

## 1. Linux - ubuntu 18.04 Install
- Link : http://cdimage.ubuntu.com/netboot/18.04/?_ga=2.19477246.711640376.1593573994-1652297923.1593573994
- 링크로 가서 기기에 해당하는 ubuntu를 다운받아 듀얼부팅 또는 리눅스 단일 부팅으로 설치한다.
** 30GB이상 할당 요망.

## 2. ubuntu ros_melodic 설치
- Link : https://dev.px4.io/master/en/setup/dev_env_linux_ubuntu.html
- ubuntu_sim_ros_melodic.sh 를 다운받아 실행한다.

## 3. PX4 펌웨어 다운로드
1. cd ~
2. git clone https://github.com/PX4/Firmware.git --recursive
3. cd ~/Firmware
4. bash ./Tools/setup/ubuntu.sh
5. git checkout v1.10.1
6. git submodule update --init --recursive

## 4. gazebo 실행
1. cd ~/Firmware
2. make px4_sitl gazebo

## 5. QGroundControl 다운로드 및 실행
1. sudo usermod - a -G dialout $USER
2. sudo apt-get remove modemmanger -y
3. sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-libav gstreamer1.0-gl -y
4. cd ~/Downloads  또는 cd ~/다운로드
5. chmod +x ./QGroundControl.AppImage
6. ./QGroundControl.AppImage
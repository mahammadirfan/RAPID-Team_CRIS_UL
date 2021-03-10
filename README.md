# RAPID-Team_CRIS_UL
This repository is a work for the RAPID project at CRIS LAB.

# Installing and running (Ubuntu 16.04)

## Install ROS Kinetic & DJI ROS SDK
[http://wiki.ros.org/kinetic/Installation/Ubuntu]

'sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

'sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654'

`sudo apt install ros-kinetic-desktop-full`

`echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc`

`source ~/.bashrc`

`sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential python-catkin-tools`

`sudo rosdep init`

`rosdep update`


## Install dependencies

`sudo apt install ros-kinetic-nav-msgs`

`sudo apt install ros-kinetic-image-transport`

`sudo apt install ros-kinetic-urg-node`

`sudo apt install ros-kinetic-nmea-msgs`

`sudo apt install ros-kinetic-message-to-tf`

`sudo apt install ros-kinetic-rosserial`

`sudo apt install ros-kinetic-rosserial-arduino`

`sudo apt install ros-kinetic-robot-localization`

`sudo apt install v4l-utils`

## Install OpenCV

Tested and run with opencv 4.2.0 (should work with opencv > 3.3)



## Instal DJI SDK

Clone repository branch 3.9

`git clone https://github.com/dji-sdk/Onboard-SDK.git`

Compile and install 

`cd Onboard-SDK`

`mkdir build && cd build`

`cmake ..`

`make`

`sudo make install`

`sudo ldconfig`

`sudo usermod -a -G dialout $USER`

Log in and out and DJI SDK is ready to go

## Setting up the ROS ws

`mkdir -p ~/ROS/DJI_OSDK_ws/src`

`catkin_init_workspace`

`cd ..`

`catkin init`

`catkin build`

`echo "source ~/ROS/DJI_OSDK_ws/devel/setup.bash" >> ~/.bashrc`

`source ~/.bashrc`

## Fixing usb cam

`cd ~/ROS/DJI_OSDK_ws/src`

`git clone https://github.com/ros-drivers/usb_cam.git`

Open `usb_cam/src/usb_cam.cpp` and add:
`av_log_set_level(AV_LOG_ERROR);`
to line 376

This fixes the following warning beeing spammed to the console:
`[swscaler @ 0x564625b66b60] deprecated pixel format used, make sure you did set range correctly`

## Teensy UDEV rules
Add the file: `49-teensy.rules` to the udev folder : `/etc/udev/rules.d/` and add the following content to it:

[https://www.pjrc.com/teensy/49-teensy.rules]


## Python

`pip install pandas`

`pip install scikit-image`

## Edit the launch file and enter your App ID, Key, Baudrate and Port name in the designated places.
(note:there are two launch file.
dji_sdk_node.launch is for dji_sdk_node.(3.8.1's interface)
dji_vehicle_node is for dji_vehicle_node(4.1.0's interface))

$rosed dji_osdk_ros dji_sdk_node.launch
$rosed dji_osdk_ros dji_vehicle_node.launch

Remember to add UserConfig.txt to correct path.(in the current work directory)

If you want to run dji_sdk_node.launch, you need to put UserConfig.txt into /home/{user}/.ros. dji_vehicle_node.launch does not need UserConfig.txt.

## Running the Samples
1.Start up the dji_osdk_ros ROS node.
if you want to use OSDK ROS 4.1.0's services and topics:

$roslaunch dji_osdk_ros dji_vehicle_node.launch

if you want to adapt to OSDK ROS 3.8.1's services and topics:

$roslaunch dji_osdk_ros dji_sdk_node.launch

2.Open up another terminal and cd to your catkin_ws location, and start up a sample (e.g. flight control sample).

$source devel/setup.bash
$rosrun dji_osdk_ros flight_control_node

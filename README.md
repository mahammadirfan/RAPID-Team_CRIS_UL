# RAPID-Team_CRIS_UL
This repository is a work for the RAPID project at CRIS LAB.

# Installing and running (Ubuntu 16.04)

## Install ROS Kinetic
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

`git clone -b 3.9 https://github.com/dji-sdk/Onboard-SDK.git`

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

## Install Guidance

`cd ~/ROS/DJI_OSDK_ws/src`

`git clone https://github.com/AnandaNN/Guidance-SDK-ROS.git`

`sudo sh -c 'echo "SUBSYSTEM==\"usb\", ATTR{idVendor}==\"fff0\", ATTR{idProduct}==\"d009\", MODE=\"0666\"" > /etc/udev/rules.d/51-guidance.rules'`

`catkin build` Needs to be run a couple of times before it compiles (Something with the message generation)


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


## 


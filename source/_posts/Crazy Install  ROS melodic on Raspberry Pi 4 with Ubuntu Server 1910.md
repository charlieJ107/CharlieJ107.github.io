---
title: Crazy Install  ROS melodic on Raspberry Pi 4 with Ubuntu Server 1910 # 标题
date: 2019/11/1 # 时间
categories: # 分类
- Experience
tags: # 标签
- ROS
- Ubuntu
- Raspberry Pi
---
Install 1910 on Raspberri Pi 4
<!--more--->

However, the mouse and keyboard , actually the whole USB port are useless.

Install ROS melodic from source as the tutorial on the wiki.ros.org/melodic/installation/ubuntu. 

When resolving Dependencies:

Some dependencies not found in the repository for eoan. 

That's ok to set the official repository ros-latest.list to bionic. 

Install the dependences manually one by one.

Build the catkin workspace. 

"console bridge" problem:

```bash
git clone git://github.com/ros/console_bridge.git
cd console_bridge
cmake .
make
sudo make install
```

"boots lib" problem:

```bash
sudo apt-get install cmake libblkid-dev e2fslibs-dev libboost-all-dev libaudit-dev
```

"gtenst"problems:

```bash

udo apt-get install libgtest-dev
sudo apt-get install cmake # install cmake
cd /usr/src/gtest
sudo cmake CMakeLists.txt
sudo make

```





eigen3 probrems

```bash
sudo apt install libeigen3-dev
```



no module named sigconfig 

```bash
wget https://www.riverbankcomputing.com/static/Downloads/sip/4.19/sip-4.19.tar.gz
tar -xvfz sip-4.19.tar.gz
cd sip-4.19.tar.gz
python configure.py
sudo make
sudo make install
```

empy:

```bash
sudo apt install python-empy
```

tinyxml2

```bash
git clone https://github.com/leethomason/tinyxml2.git
cd tityxml.git
mkdir build
cd build
cmake ..
make
sudo make install
```



not found sudo LOG4CXX

```bash
sudo apt-get install liblog4cxx-dev
```

tinyxml1

````bash
sudo apt install tinyxml-dev
````



tested: 

```bash

sudo apt-get install libfontconfig1-dev libdbus-1-dev libfreetype6-dev libudev-dev libicu-dev libsqlite3-dev libxslt1-dev libssl-dev libasound2-dev libavcodec-dev libavformat-dev libswscale-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev gstreamer-tools gstreamer0.10-plugins-good gstreamer0.10-plugins-bad libraspberrypi-dev libpulse-dev libx11-dev libglib2.0-dev libcups2-dev freetds-dev libsqlite0-dev libpq-dev libiodbc2-dev libmysqlclient-dev firebird-dev libpng12-dev libjpeg9-dev libgst-dev libxext-dev libxcb1 libxcb1-dev
libx11-xcb1 libx11-xcb-dev libxcb-keysyms1 libxcb-keysyms1-dev libxcb-image0 libxcb-image0-dev libxcb-shm0 libxcb-shm0-dev libxcb-icccm4 libxcb-icccm4-dev libxcb-sync1 libxcb-sync-dev libxcb-render-util0 libxcb-render-util0-dev libxcb-xfixes0-dev libxrender-dev libxcb-shape0-dev libxcb-randr0-dev libxcb-glx0-dev libxi-dev libdrm-dev libssl-dev libxcb-xinerama0 libxcb-xinerama0-dev
```





qt5-widgets

```bash
sudo apt install qt5-default
```



pyqt5

```bash
sudo apt install python-pyqt5
```





'SIP_NULLPTR'

```
wget https://www.riverbankcomputing.com/static/Downloads/sip/4.19/sip-4.49.tar.gz
tar -xvfz sip-4.49.tar.gz
cd sip-4.49.tar.gz
python configure.py
sudo make
sudo make install
```



lz4

```bash
sudo apt install python-lz4 python3-lz4
```

it not use

try everything you can search in apt about lz4

seems lz4 and ros about would be work?



urdfdom_header:

```bash
sudo apt insatll liburdfdom-dev
```



bzip2

try everything you can fine in `apt search ` about bzip2



opencv

install everything about opencv, actually you will use it later them all. 



"OGRE"

```bash
sudo apt install libogre-1.9.0-dev libogre-1.9.0v5
```

"yaml-cpp"

```bash'
sudo apt install libyaml-cpp-dev libyaml-cpp0.6
```

asssmp:

```bash
sudo apt install libassimp-dev assimp-utils libassimp4 python-pyassimp python3-pyassimp
```





After installation:

roscore:

netiface

````bash
pip install netifaces
#or
sudo apt install python-netifaces python3-netifaces
````



The main idea of debug the dependences is apt search the package name. 
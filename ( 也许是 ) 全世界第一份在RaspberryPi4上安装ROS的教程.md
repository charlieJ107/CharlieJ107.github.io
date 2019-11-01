# ( 也许是 ) 全世界第一份在RaspberryPi4上安装ROS-melodic的教程

##### How to install ROS - Melodic On Raspberry Pi 4 with Ubuntu Server 19.10

### 失踪人口回归

长期以来被学校和各种各样其他的事物压榨得奄奄一息, 一度把自己弄到抑郁. 但经过这一番奋斗, 虽然依然压力很大, 但还是希望能够留下点东西, 不然学完了就学完了, 姑且不说久不用了会不会忘, 重要的是, 总需要一点东西逼迫自己写点东西. 于是, 还是希望每周能抽出一点时间来写点东西. 

### 源起

​	想做一个情绪机器人, 灵感来源于超能陆战队里的大白. 但是大白的这个形象从硬件上涉及很多问题, 根据曾灿辉的说法, 几乎不可能做到. 心血来潮想要参加微软的IC, 所以就想着, 要不做个球吧. 叫做Ba Ba'll. 名字起得很随便, 总之, 这玩意儿是一个机器人. 

​	基本的思想就是树莓派作为大脑, 控制高级功能, 再用一个Arduino来作为小脑, 控制运动. RaspberryPi4刚刚出来, 4GB的RAM真的很爽. 不过官方的Raspberrybian还是一个32位的操作系统, 而且作为一个教育为导向的操作系统, 总觉得太Low了. ROS也并没有为了这个版本的debian设计过. 虽然一样没有为1910的Ubuntu设计, 但好歹也是Ubuntu. 

​	不过Ubuntu还是有问题. 首先, 18.04 的LTS是不支持RP4的, 这玩意儿出来的时候RP4还没出来. 如果强行刷进去的话会直接没办法进系统. 第二, 即使是19.10 (eoan) 的Ubuntu server, 还是有个惊天bug导致了整个USB不能用. 因为这个USB的芯片需要一些有特殊要求的内存空间, 但是这个内存空间没有被好好划给芯片, 被系统其他部分占用了. 这个东西已经被一个内核补丁给搞定了, 但是在我的板子上解决这个问题还要重新编译内核, 这个可能可以留给以后去解决这个问题. 

​	于是就有了我们这个并不完美的环境: 一块RP4, 一根网线 ( 用来连接SSH访问命令行) , 以及电源. 外带一个预安装版本的Ubuntu server 19.10 的arm64版本. 

### 正片开始

​	在RP4上安装ROS有以下几个基本问题:

1.  ROS是为Ubuntu设计的, 其他的发行版只是顺便支持一下. 所以Raspberrybian是别想了, 乖乖按照Ubuntu官网上的指南安装Ubuntu. 在此之前, 很多人都是在RP上装Ubuntu mate. 这个mate虽然也是基于Ubuntu, 但是难保你这个定制的桌面环境会给你整出什么幺蛾子. 当然作为一个愿意折腾的人虽然我们不怕幺蛾子, 但是第一这玩意儿很浪费时间, 第二, 你想想一旦出了幺蛾子, 你觉不觉得Ubuntu server 的相关资料要比一个小众的mate要多得多? 
2.  ROS的预编译版本是为x86的设备编译的, 虽然也有arm64的版本, 但无论是哪个预编译版本, 都只支持bionic(18.04). 这就意味着仅有19.10能支持的树莓派也别想用预编译版本了, 只能从源码编译. 
3.  正如之前所说, ROS的依赖关系检查和安装是由一个专门的工具 (`rorsdep`) 来完成的. 这玩意儿是python写的, 而Cpython的解释器是c写的. 虽然自己从源码编译理论上能够保证任何有GCC的平台就能用上ROS, 然鹅这个愚蠢的`rosdep`根本不认识刚发布不久的19.10. 你在使用`rosdep`检查和处理依赖的时候会报一堆说不认识你这个OS版本. 这就意味着你只能自己找依赖. 



​	首先先记得换一下镜像源. 镜像源的问题已经老生常谈了. 网上有很多资料, 总的来说, 就是换掉`/etc/apt/source.list`里面的域名. 我原本以为这个应该是一个很简单那的东西, 但是我发现好多人根本不看版本, 直接上CSDN上面照抄, 结果一个1604的版本换了个1804的镜像源, 报了一堆错. 

​	哦, 也有一堆人根本不知道镜像源是什么, 我原本以为机器人队质量会高一点, 没想到一堆人还不知道linux是啥...

​	嗯, 中国的高考制度让中国优秀的大学里充斥着90%的精通考试的学生, 但这群学生一旦遇到考试之外的东西, 完全不知道怎么下手. 而中国的大学为了保证这群学生不至于太惨, 只好调整自己的考试和考核模式, 即让考试考得好的人评价好, 而实际的工程能力和学习能力, who cares? 我非常理解这种举动, 因为大家都是这样上来的, 所有人都是既得利益者. 所以只能牺牲那极少数的, 工程OK但考试不强的, 来希图那三分之一考试比较好的人里面, 能够萌生出更极少数的, 工程能力强的人. 

### 官网上的能用的部分

1.  安装`bootstrap`依赖. 

    ```bash
    sudo apt-get install python-rosdep python-rosinstall-generator python-wstool python-rosinstall build-essential
    ```

2.  初始化 `rosdep`

    ```bash
    sudo rosdep init
    rosdep update
    ```

3.  创建`catkin`工作区

    ```bash
    mkdir ~/ros_catkin_ws
    cd ~/ros_catkin_ws
    ```

4.  然后用`wstool`把源码下载下来

    ```bash
    rosinstall_generator desktop --rosdistro melodic --deps --tar > melodic-desktop.rosinstall
    wstool init -j8 src melodic-desktop.rosinstall
    ```

    这里安装的是带桌面组件的ROS melodic. 可以根据需要选择其他版本, 也可以选择命令行, 不带桌面组件. 因为目前还处在开发阶段, 等到实际跑起来的时候就不需要桌面了, 直接上命令行的 Bare Bones 版本. 



​	好, 官网上能用的部分就到这儿了. 接下来按照官网上的东西会出现各种各样的问题, 我们解决问题的漫漫长路也是从这里开始的.. 

### 解决依赖

​	到目前为止, 按照官网上的东西都能够正常跑通. 接下来就是要解决依赖的问题了. 官网上的命令是这样的:

```
rosdep install --from-paths src --ignore-src --rosdistro melodic -y
```



到这里会报一堆错, 大概的意思就是劳资不认识你这个系统版本. 因为咱们这个系统是19.10, 它不认识是正常的. 

​	这个时候我们可以先行找到一些 (有可能) 需要安装并且可以被安装的依赖, 简单来说, 看看上面告诉你什么包没找到, 就在`apt`里面安装这个包. 

```bash
sudo apt install python-xxx -y
```

当然, 你就算安装了这些包, 再次跑一边检查依赖的命令还是会报同样的错误, 也许缺的包少一些了, 但问题还没有被解决. 

​	我在走这一步的时候, 先后尝试了很多种花式安装, 先是用`apt`安装了一遍, 又用`pip`安装了一遍, 但是还是没有解决这个问题, 索性就不去管他, 直接开始编译. 

### 踩完了坑之后的做法

​	如果你根本不关心我在这个过程当中遇到的艰难险阻和朴实无华却行之有效的调试方法, 你可以直接跑一遍接下来的命令, 然后直接开始编译. 

​	首先是可以用`apt`或者`pip`直接安装的: 

```bash
sudo apt-get install cmake libblkid-dev e2fslibs-dev libboost-all-dev libaudit-dev libeigen3-dev python-empy liblog4cxx-dev tinyxml-dev qt5-default python-pyqt5 python-lz4 python3-lz4 liburdfdom-dev libzip2 libogre-1.9.0-dev libogre-1.9.0v5  libyaml-cpp-dev libyaml-cpp0.6  libassimp-dev assimp-utils libassimp4 python-pyassimp python3-pyassimp  python-netifaces python3-netifaces
```

然后就是有一个很尴尬的事情, 有些依赖我也不知道是哪个包出了问题, 所以索性就把所有有可能的包装上了. 我猜有一堆人不知道`apt`还有`apt search`这个命令的, 你可以试试用`apt search`一些缺的, 然后把看起来有用的都装上, 最后解决了这两个东西的依赖问题. 鉴于我也不知最后到底是哪个包起作用, 读者可以自己试着做一下. 

```bash
apt search lz4
apt search bzip2
apt search opencv
```

这里说一下, lz4我主要挑了一些介绍或者名字里面有ros和lz4的. 另外, bzip2应该就是libzip之类的库需要装, 所以可以不用把所有搜索出来的都装上, 有选择性地装上就可以了. 

有一些东西需要自己下载源码下来编译. 在此之前, 请确保自己装了git 并且配置了全局用户名. 有些系统镜像(比如docker里面的那个)过于精简, 甚至连wget都没有. 不过考虑到这是树莓派而且这是Ubuntu Server, 所以应该这些都是有的. 

​	首先是可以从GitHub上面clone 源码的

console_bridge

```bash
git clone git://github.com/ros/console_bridge.git
cd console_bridge
cmake .
make
sudo make install
```



gtenst

```bash
sudo apt-get install libgtest-dev
sudo apt-get install cmake # install cmake
cd /usr/src/gtest
sudo cmake CMakeLists.txt
sudo make
```

tinyxml2

这个说一下, 早些年这玩意儿就是tinyxml, 后来更新了以后就是tinyxml2, tinyxml的库就没了. 但是不知道为啥这个ROS里面还有一些包用的还是旧版本的tinyxml, 值得庆幸的是旧版的tinyxml可以用`apt`安装, 所以也顺利解决了这个问题

```bash
git clone https://github.com/leethomason/tinyxml2.git
cd tityxml.git
mkdir build
cd build
cmake ..
make
sudo make install
```

然后就是sip

这个涉及到一个很严肃的问题: python2 今年上半年停止支持了以后, pypi干脆连Python2的sip都不支持了. 所以这个本来可以用`pip`安装的东西, 到头来却要从源码编译

```bash
wget https://www.riverbankcomputing.com/static/Downloads/sip/4.19.19/sip-4.19.19tar.gz
tar -xvfz sip-4.19.19.tar.gz
cd sip-4.19.19.tar.gz
python configure.py
sudo make
sudo make install
```

差不多就是这些了. 

这个时候就可以放心大胆地继续跑官网的那个教程里面的make环节了

```bash
 ./src/catkin/bin/catkin_make_isolated --install -DCMAKE_BUILD_TYPE=Release --install-space /opt/ros/melodic 
```

这个命令注意一下, 官网上的是没有最后那个`--instal-space`这个参数的. 这个参数主要是用来指定安装的地方, 我个人建议最好还是指定一下, 尽可能缩小不同平台之间的差距, 提高代码的可移植性. 

然后就是, 为了能够获得与预编译版本相似的体验, 我个人建议不要依赖官网上的编译教程, 在最后设置环境的时候, 还是按照预编译安装的那个教程, 走这个命令: 

```bash
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```



​	到此为止, 整个ROS就安装好了. 
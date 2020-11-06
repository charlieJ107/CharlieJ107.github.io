---
title: '在多台机器上运行ROS-理论篇'
date: 2020-02-28 23:58:22
category: Tutorial
tags: 
- ROS
- Network
---

​	由于仿真需要, 准备在同一个局域网内开多个容器进行多机协同演练. 这需要在一个局域网内把多个机器的节点链接起来. 查阅官网的教程, 记录如下, 之后可能会补一个实操篇, 记录自己的操作流程.
<!--more-->
### 概述

ROS设计的灵魂就在于其分布式计算。一个优秀的节点不需要考虑在哪台机器上运行，它允许实时分配计算量以最大化的利用系统资源。(有一个特例——驱动节点必须运行在跟硬件设备有物理连接的机器上）。在多个机器人上使用ROS是一件很简单的事，你只需要记住一下几点：  

- 你只需要一个master，只要在一个机器上运行它就可以了。 
- 所有节点都必须通过配置 `ROS_MASTER_URI`连接到同一个master。 
- 任意两台机器间任意两端口都必须要有完整的、双向连接的网络。(参考[ROS/NetworkSetup](http://wiki.ros.org/ROS/NetworkSetup)). 
- 每台机器都必须向其他机器广播其能够解析的名字。(参考 [ROS/NetworkSetup](http://wiki.ros.org/ROS/NetworkSetup)). 

###　跨机器运行的 Talker / listener

假如说我们希望在两台机器上分别运行talker / listener， 主机名分别为 **marvin** 和 **hal**.登陆主机名为｀`marvin`的机器,你只要: 

```sh
ssh marvin@192.168.0.1
```

同样的方法可以登陆`hal`. 

你还需配置ROS_IP为当前的局域网ip地址。(利用ifconfig指令可以查看你当前的ip地址）。其次，很有可能你的主机名不能够被其他机器解析，所以保险的方法是利用 ssh hostname@local_ip的方式进行登陆(如*ssh [turtlebot@192.168.1.100](mailto:turtlebot@192.168.1.100)*)。再者，ROS_MASTER_URI最好也用运行master的那台机器的ip地址来替换主机名（如：*export ROS_MASTER_URI=http://192.168.1.100:11311*) 

### 启动 Listener

在`hal`机器上启用Listener, 并且配置ROS_MASTER_URL来使用`hal`机器上的Master. 你也可以在其他机器上运行master。

```sh
ssh marvin@192.168.0.1
export ROS_MASTER_URL=http://hal:11311
rosrun rospy_tutorial talker.py
```

小惊喜: 现在你可以看到机器**hal**上的listener正在接收来自**marvin**机器上talker发布的消息。 

请注意，talker / listener启动的顺序是没有要求的， 唯一的要求就是master必须先于节点启动。 

### 反向测试

现在我们来尝试一下反向测试。终止talker和listener的运行，但仍然保留master在机器 **hal**上，然后让talker和listerner交换机器运行。 

首先，在机器**marvin**启动listerner: 

```sh
ssh marvin@192.168.0.1
export ROS_MASTER_URI=http://hal:11311
rosrun rospy_tutorials listener.py
```

然后在机器**hal**上启动talker: 

```sh
ssh hal@192.168.0.2
export ROS_MASTER_URI=http://hal:11311
rosrun rospy_tutorials talker.py
```

### 运行出错

如果没有取得如上预期的效果，那么很有可能是你的网络配置出错了。参考[ROS/NetworkSetup](http://wiki.ros.org/ROS/NetworkSetup)重新配置你的网络。 


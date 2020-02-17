# ICRA机器人队招募

* 我们是谁: 厦门大学TUF机器人队

* 我们干啥的: 专攻机器人+AI方向的挑战赛, 目前主攻Robomaster ICRA AI挑战赛

> 等等, Robomaster我知道, ICRA AI挑战赛是干啥的: 
>

* Robomaster是人遥控着机器人打CS (反恐精英, 一款老人们小时候常玩的FPS游戏) , 我们是让机器人自己决策自己去打CS

* 我们要干啥：**招人**，招大牛，最好是能把我们这群菜鸡学长学姐按在地上摩擦，然后带着我们一起飞的那种大牛. 

* 有什么条件吗: 牛逼就行, 甭管你是哪个专业, 电子的, 机械的, 计算机类的, 软工类的, 树莓的, 逼乎四大劝退的...我们都要!

> 我啥也不会能去参加吗?

你不会干活，你还不会学吗？赶紧加群:point_down:: 939307675

<img src="https://xmu-tuf.vankyle.cn/group.jpg" alt="group" style="zoom:40%;" />

​    综上所述：我们设计了一系列任务，我们知道这些任务当中一些名词你可能听都没听说过,  没关系, 我们大一的时候也没听说过, 不过经过不到一个月的磨练, 基本都摸了个差不多了. 所以我相信你们都能搞得定. 

​    需要说明的是, 经过反复验证, 我们确信一个有一定C语言程序设计及其周边知识的学生在一个月内足以完成本试题所要求的全部内容. 因此, 请放心大胆地寻求各种各样的帮助, 包括但不限于网络搜索, 阅读相关书籍. 对于多人共同完成的任务的, 请想办法让我们高效地知道你们各自都做了什么. 

​	我们的题目主要考察以下几个方面: 

* 表达与交流的能力, 团队合作的意识
* 自主学习, 遇到困难时寻求方法解决问题的能力
* 利用已知知识举一反三的能力: 注意, 这不是考试让你做一题就会做整个题型, 而是让你了解了这个方面的知识之后利用知识去解决实际问题
* 理论指导实践的意识, 定位/溯源问题的意识
* Last but not least: 刨根问底的好奇心, 和满足这种好奇心的能力和热情

**另外, 请及时关注我们的要求更新情况, 将会在这个页面更新.**



##  Status Update

* 受疫情影响, 最终推送的Deadline已经由2月18日修改为**3月1日**. 如有其他安排另行通知



### 题目如下

请在2020年3月1日23:59:59之前**使用SSH**向我们的git仓库(git@e.coding.net:xmu-tuf/tuf-wanted.git)Push以下内容: 

1. 用`Markdown`编写的你的简历, 这个内容形式不限, 要求只有一个, 用最高效的方式让我知道你是谁, 顺便说服我让你加入我们. (预计完成时间, 3天内)

2. 一个Bash shell scripts, 能够让一台刚刚使用官方镜像安装好Ubuntu 18.04-desktop/server-amd64的电脑安装上`thefuck`, `git`, `vim`, `vscode`, `docker`, `ROS`, `typora`, 同时更换好国内的apt和pip安装源( 阿里云/腾讯云/清华/中科大源四选一), 加入适当注释让我知道你明白你写的东西在干什么才写的(而不是无脑复制粘贴的)(预计完成时间: 一周)

   (如果可以, 最好试图了解一下以上让你安装的这些东西大概有什么用, 最好能会用其中的一两个, 尤其是thefuck, 这个名字看起来很暴躁的东西真的很好用...)

3. 一个catkin workspace, 包含一个使用C++编写的ROS package, 包含Publisher和Subcriber, 使运行时Subscriber能够打印出你的姓名ID, 并在代码中留下适当注释让我知道你知道你的代码在干什么(而不是无脑复制粘贴的), 要求使用Melodic版本的ROS, 除 (预计完成时间: 一周)

4. **(选做) **请提供一个任意形式的作品, 显示你的技能树

5. **(选做)**在合法合理的情况下, 其他任何能够让我知道你很牛逼的东西, 或者说说你为了完成上面这些题目干了哪些事情, 有什么感受啥的. 

即, 最终你的推送应当至少包含

一个`.md`文件, 一个`.sh`文件, 一个`catkin workspace`(文件夹)

### 注意

1. **使用SSH推送前, 可以将公钥发送至charlie_j107@outlook.com ,  完成授权后, 你将收到邮件回复, 届时你就可以使用你的公钥进行Push了. **
2. 代码可读性将是重要的考量指标, 请特别留意代码的可读性和鲁棒性
3. 如果DDL前没能完成所有题目也不要紧, 提交上来我也会给你机会. 
4. **Deadline: 2020/3/1 23:59:59**

### 提示

1. 如果你需要上网搜索相关知识, 关键词已经在题目中

2. 官方网站和官方文档比CSDN好用, 英语真的不难, 都是四级词汇

3. 以下网址可能有用

   别用百度: https://www.bing.com

   Git 是什么: https://github.com/charlieJ107/gitlearn

   我不想装双系统怎么用Linux? : https://www.vmware.com/cn/products/workstation-player/workstation-player-evaluation.html

   Linux 是什么, 怎么用: http://linux.vbird.org/linux_basic/

   什么是Markdown: https://sspai.com/post/25137

   拿什么写Markdown: https://www.typora.io

   不会C++: https://docs.microsoft.com/zh-cn/cpp/cpp/cpp-language-reference

   [不会C++但是会一点C](https://liuminghui233.cn/2019/08/24/华丽转变%EF%BC%81从C快速入门C/)

   ROS是什么: https://wiki.ros.org

   我需要一个好用免费的东西写代码: https://code.visualstudio.com

   微软爸爸的各种牛逼技术文档: https://docs.microsoft.com

   由于众所周知的原因一些国外的网站下载很慢: https://mirrors.cloud.tencent.com

   这玩意儿报错了, 怎么办? : https://stackoverflow.com/

5. 如果触及了你自己的知识盲区, 请尝试任何可能的方式寻求帮助. 鼓励多人合作完成任务

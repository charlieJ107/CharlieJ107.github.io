# ROS安装时的raw.gihubusercontent.com连不上咋办

1. 连不上是因为一些众所周知的原因...

2. 解决思路:

   1. 科学上网
   2. 换一个能连上的

3. 我自己搭建了一个镜像, 简单来说, 你可以直接吧域名`raw.githubusercontent.com`改成`mirrors.vankyle.cn`, 其他的可以照原样. 

4. 修改的地方: 有以下几个

   1. rosdistro下的`__init__.py`里定义了一个常量叫`DEFAULT_INDEX_URL`
   2. rosdistro下`github.py`下有两个函数, 一个`package_xml_in_parents`里面的`url`这个变量
   3. 还是这个文件下有个`_get_url_contents(url)`里面也是有个叫`url`的变量
   4. rosdep下有三个
      1. gbpdistro_support.py的`FURTER_GBPDISTRO_URL`
      2. rep3.py的REP3_TARGETS_URL
      3. sources_list.py的`DEFAULT_SOURCES_LIST_URL`

   以上这几个地方的`raw.githubusercontent.com`全部改成mirrors.vankyle.cn就可以了



报这个错是因为https://raw.githubusercontent.com/ros/rosdistro/这个的库里的raw文件没办法直接下载下来, 那我们就直接把这个库clone到一个我们可以下载的地方就好了. 
所以我自己搭了一个镜像, 用起来有点麻烦, 但是可以解决问题. 简单来说, 就是把那个域名raw.githubusercontent.com改成我的镜像网址mirrors.vankyle.cn
具体的修改方法如下:
找到/usr/lib/python2.7/dist-packages/这个目录, 这个目录下有两个地方需要改:, 一个rosdep2, 一个rosdistro. 
这两个地方下面有几个.py文件里定义了Url, 把那个Url里面的域名修改一下就可以了. 这几个URL的位置如下: 
\1. rosdistro下的`__init__.py`里定义了一个常量叫`DEFAULT_INDEX_URL`
\2. rosdistro下`github.py`下有两个函数, 一个`package_xml_in_parents`里面的`url`这个变量
\3. 还是这个文件下有个`_get_url_contents(url)`里面也是有个叫`url`的变量
\4. rosdep下有三个
  \1. gbpdistro_support.py的`FURTER_GBPDISTRO_URL`
  \2. rep3.py的REP3_TARGETS_URL
  \3. sources_list.py的`DEFAULT_SOURCES_LIST_URL`

如果你找到这几个文件, 就可以看见这几个url都是https://raw.githubusercontent.com/xxxxxx的, 把里面的raw.guthubusercontent.com改成我的镜像mirrors.vankyle.cn就可以了

提示: vim里面可以用:%s/被替换的内容/替换成的内容/g (g表示见到就替换, 全文都这样)来实现替换

毕竟是个人的土办法, 当然, 也可以科学x网, 或者换一个其他的靠谱的源. mirrors.vankyle.cn这个源是我自己搭建的, 可能不是很快, 但能用了. 

仅供参考, 如果有帮助, 不胜荣幸. 如果有更好的办法, 欢迎讨论


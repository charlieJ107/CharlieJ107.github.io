---
title: 我能不能不用Anaconda
date: 2020/7/7 # 时间
categories: # 分类
- Thinking
tags: # 标签
- Python
- Anaconda
- Config
- pip
---
## 永远不要只依赖于一件事物，否则你拥有不了自由


<!--more-->
### 事由

学校的实训课要学python了. 

虽然这是我大一的时候就已经摸了一遍的东西, 但是既然是学校老师教(也只是为了实训项目服务, 并不是系统地教), 那也可以听一听看看, 毕竟身边的绝大多数同学都在各种奇奇怪怪的 "新生研讨课", "人工智能体验营"之类的东西熏陶下实现了 "精通深度学习算法, 却不知道什么是栈" 的状态, 但总还是要服气, 毕竟人家考试比我好, 上来`int i, j, k;`后面就不会了挺了半天不知道怎么写栈的人, 数据结构考试还是能考满绩...

嗨, 吐槽了一堆, 回到正题. 面对一群没有对Python停留在只听说过名字的学生, 老师在群里说叫大家安装好Anaconda. 

我问老师能不能用pip手动配置, 顶多再加个virtualenv, 但老师觉得Andaconda开箱即用, 还是建议用Anaconda. 

我不是对Conda有什么偏见, 但我不认为Anaconda应该成为Python环境的首选项. 

### 啥是Anaconda

> Python是编程语言，官方的Python包含了核心的模块和库，为了完成其他任务，需要安装其他的模块和库。
>
> Anaconda将Python和许多与科学计算相关的库捆绑在一起，形成了一个方便的科学计算环境，你安装了Ananconda就相当于安装了Python外加这些模块和库。当然Anaconda主要的功能还在于你可以方便进行环境管理。
>
> 除了Anaconda，还有WinPython、Python（X，Y）等，你可以类比Linux系统有Ubuntu、CentOS等发行版，把Anaconda、WinPython理解成不同的Python发行版。
>
> --Euclid zhihu.com

简单来说, anaconda = python + （NumPy、SciPy 等常用第三方库 ）+  IDE (Jupyter notebook 和Spyder)

### 为什么大家都推荐用Anaconda

说白了就一件事儿, 开箱即用. 

Anaconda把大多数的东西都给你准备好了, 你打开就能用, 也不用自己折腾python的环境变量, 也不用自己折腾IDE, 也可以少安装很多包(因为它都给你装好了). 

就好像生娃, 人家给你生好了娃, 你来当父母带娃就行. 

### 为什么我不用Anaconda

#### "政治上"的考量

正如我最开始说, 永远不要依赖于一件事物, 否则你拥有不了自由. 

在这一点上, 我跟[@匿蟒的观点](https://www.zhihu.com/question/404402864/answer/1312881774)基本上是一致的。

中国人最近一年多来在这件事上的教训还不够深刻吗?

Anaconda是商业公司, 它能停掉你国内的分发镜像, 不能停掉你国内的使用权?

多少人现在离了Anaconda连环境都不会配, 就好像一堆人离开MATLAB连图都不会画了. 

今年美国对台积电的长臂管辖，意味着把商业基础交给美国的商业公司，是一件可能会炸的事。在一些公司内部做技术选型时，把美国商业技术列入低优先级名单、甚至黑名单，已经是大势所趋。相比之下，非盈利性的基金会[PSF](https://link.zhihu.com/?target=https%3A//www.python.org/psf-landing/)更可以信赖。

这还只是所谓的政治上的考量. 

#### 如果单纯从技术上说

Anaconda仅仅解决了一些我很容易就能解决的问题, 但是却带来了一堆我不想碰到的问题. 

Anaconda对于包的版本管理落后pip一截, 网络问题国内现在也只有清华这样的学术机构的镜像能用, 原先能用的腾讯阿里的源都挂了. 即使是有了清华的镜像, 从零配置原生的Python环境完毕，这个522MB的安装包（以Anaconda3-2020.02-Linux-x86_64.sh为例）都还没下载完。（这个安装包在解压、安装后，总大小3.4GB。）



#### 工程发布上的考虑

从一家商业公司的角度来考虑，既不能自建镜像，又不能接受团队的低效，难道舔着脸蹭tuna？从合规方向考虑，公司应该出钱购买Team Edition或Enterprise Edition。价格嘛，$10,000起，还有其它单次付费的情况。

原生Python根本不要钱，只需要内部培训一下。而且国内PyPI镜像满天飞，合法合规。

如果考虑到发布, 更要看看Anaconda有多臃肿. 

在大多数Python应用所有环境总共只有100MB以内（包括系统包、Python运行环境与应用本身）的情况下，一个光Python运行环境就有3.4G的东西，真的大到不能忍。从两个角度来解释吧：

1. 作为一家大公司，以Docker镜像方式发布产品。每次产品上线、扩容时，需要额外复制这么大的无用文件，空耗空间与时间，影响发布效率。我怎么和上头吹，我的秒级发布、秒级回退、秒级扩容？而且还要为这么多组件的安全、维护、开源协议操心。
2. 作为一个小开发者，买个1核1G的服务器，自带40G系统硬盘。由于没什么点击量，因此一台服务器本来预备serve几十个服务，基础镜像也往往挑选小而冷的Alpine。这个Anaconda一上来就是3.4G，小家小业折腾不起啊！

### 我不用Anaconda, 并不是因为它不好

> [Miniconda](https://link.zhihu.com/?target=https%3A//docs.conda.io/en/latest/miniconda.html)是[Anaconda](https://link.zhihu.com/?target=https%3A//www.anaconda.com/)的子集，仅包含基本的Python运行环境与conda。
>
> conda是一个了不起的创新！它结合了包管理pip与虚拟环境virtualenv等技术，不仅在客户端简化了操作，还在服务端再造了PyPI的体系。
>
> Python的软件包，大概包含纯Python（.py）、Python混合C/C++（py+so）与纯二进制（so）三大类，都支持import后直接使用。因此，PyPI支持的egg、wheel包，在设计时就考虑了对so的发布支持，即使它很复杂，必须区分架构和系统。
>
> 比如，[numpy](https://link.zhihu.com/?target=https%3A//pypi.org/project/numpy/%23files)的一个版本就通常包含近20个wheel包。这里列几个有代表性的发布件，大家可以通过文件名感受一下。
>
> - numpy-1.19.0-cp36-cp36m-manylinux2010_x86_64.whl
> - numpy-1.19.0-cp37-cp37m-manylinux2014_aarch64.whl
> - numpy-1.19.0-cp38-cp38-win_amd64.whl
> - numpy-1.19.0-pp36-pypy36_pp73-manylinux2010_x86_64.whl
>
> 有一类包，本身是三大类中的某一类（总类别已经变成了2×3=6种了），但发布时只有源码包，**安装时**需要临时编译其中的C/C++部分代码。这类包的问题是，在pip install时可能出现各式各样的crash。有时候，你安装的包本身是正常包，但依赖中有这类包，也会在安装时导致crash。
>
> 还有一类，本身是三大类中的某一类，发布时可能只有源码包，或像numpy一样做好了大多数情况下的wheel包（总类别已经变成了2×2×3=12种），但**运行时**需要依赖某些额外的系统组件（so）。因此，光有pip不够，还需动用系统包管理器，比如apt、yum等，才能完整准备某些运行环境。否则，在运行到某些功能时，就会crash，比如uwsgi、graphviz等。
>
> 所以，在上面12种分类中，只有3种是pip能完美支持的，其它9种都需要系统给与某种程度的配合，比如安装gcc、python3-dev等。conda做了比较完善的编译包，甚至包括某些运行时依赖的组件，比如[ffmpeg](https://link.zhihu.com/?target=https%3A//anaconda.org/conda-forge/ffmpeg)。用户执行conda install就够了，不需要再考虑系统状态。这一点比pip更进一步，非常优秀。
>
> 尽管如此，对我来说也并非不可替代。pip在设计时就选择了与apt这些系统包管理器共生，是因为系统包管理器更完善。一家[Anaconda](https://link.zhihu.com/?target=https%3A//www.anaconda.com/)，在完备性上是不足以与任何一个Linux发行版竞争的。它只能保证数据科学相关的包，出了这个圈依然要动用系统包管理器。
>
> 前面说了，我是一个Python开发者。仅仅有数据科学这部分，对我来说是不够的。在数据分析师、AI工程师那里，conda确实完胜了pip，他们只需要用conda；但在我这里，conda还不够完备。在conda+pip+apt和pip +apt面前，我选择了pip+apt，反而减小了环境准备的复杂度。
>
> -- @匿蟒 zhihu.com

### 最后

还是那句, 我不用Anaconda, 并不是因为它不好, 而是它不适合我. pip也好, Anaconda也罢, 都只是工具. 工具 (在大多数值得比较的场合) 没有好坏之分, 只有适合还是不适合. 我用pip, 可以让环境掌握在我手里, 可以不用被Anaconda流氓般地占用我宝贵的磁盘空间和内存空间. 并且, 在不会因为不用Anaconda给我带来困扰的情况下, 避免了用Anaconda带来的问题, 这才是我不用Anaconda的原因. 

如果你跟我一样, 有工程和发布上的需求, 享受这种自己能够把控的感觉, 或者, 仅仅是因为你已经熟悉了pip, 而Anaconda还需要另外再折腾一套你陌生的东西, 你大可不必因为一些他人的推荐而逼迫自己使用Anaconda, 毕竟永远不要依赖于一件事物, 否则你拥有不了自由. 
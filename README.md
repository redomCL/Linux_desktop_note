# 这是一个笔记本，用来记录Linux桌面版日常家用笔记

![](https://github.com/redomCL/Linux-desktop-note/blob/main/Ubuntu.png)
![](https://github.com/redomCL/Linux-desktop-note/blob/main/duckstation.png)
![](https://github.com/redomCL/Linux-desktop-note/blob/main/gnome-software.png)
![](https://github.com/redomCL/Linux-desktop-note/blob/main/synaptic.png)

# 前言：
* 目前Linux桌面发行版的发展相比Windows真的不适合日常家用娱乐，易用性要差的相当多；当然了，Linux桌面发行版目前的软件生态也真的满纯粹，绝大多数软件都可以默认安装，没有广告没有额外的骚扰，不需要像Windows一样每接触新的软件都要特别小心怕被捆绑等其他骚扰，目前Linux桌面发行版的软件生态问题主要还是1.软件不够，大多数厂商因为利益关系都没有动力在Linux桌面发行版上发布较新的家用软件；2.虽然有开源软件，但是这种非利益驱动下的软件表现参差不齐，有功能和界面都很差的，也有功能强大界面极其粗糙的，对普通家用用户来说非常不友好；3.Linux桌面发行版非常碎片，各种包管理器和图形化软件商店以及各种桌面眼花缭乱，另外个人虽然觉得各种桌面很华丽，但是手感上觉得是不如Windows的，无论是GNOME还是KDE，都有一种边界判定不清晰，“粘手”的感觉；4.依赖问题相当头大，相应的解决办法就是依靠包管理器，但是就像3中所说的，包管理器本身都相当碎片。以上，但为了不完全依赖商业形式运转的Windows操作系统这种独（毒？）苗，我还是尽可能的去了解一下Linux桌面发行版，本合集是Linux桌面发行版为了日常家用娱乐为主的笔记。 具体主要用途：
* 1、家庭影音：主要以跨平台的优秀播放器mpv为主，也可以用基于mpv的gnome mpv、smplayer
* 2、网络通讯：微信、QQ、跨平台的优秀浏览器firefox
* 3、游戏：steam和wine，Linux原生模拟器
* ...

## 一、包管理相关：软件安装

* Linux发行版不同于Windows的软件安装习惯，Linux发行版一般有自己的在线软件库（各国都有镜像源解决不能访问的问题），并通过搭配内置的包管理器进行管理，以下是一些用过的包管理器列举。

* 实际上GNOME除了作为Ubuntu的桌面，同时也为大部分包管理器（软件商店）提供了一个图形界面，apt、snap、flatpak和dnf都可以用gnome-software作为图形包管理器（图形软件商店），同理的还有KDE桌面的Discover软件管理中心。

* Debian/Ubuntu deb：前端包管理器apt，图形前端包管理器synaptic/gnome-software，安装软件的基础。

* Ubuntu snap：前端包管理器snap，有图形前端snap-store/gnome-software，用于对apt的扩充。

* Fodera/RedHat RPM：前端包管理器dnf，图形前端包管理器gnome-software。

* openSUSE YaST2：前端包管理器YaST2，Discover软件管理中心图形前端包管理器。

* *fuse：用户空间文件系统，用于对apt的扩充，ubuntu下通过apt安装libfuse2，实现对appimage独立包的直接运行。

* *Flatpak：多种Linux桌面发行版；前端包管理器flatpak，图形前端包管理器gnome-software，用于对apt的扩充。包含大量游戏模拟器软件。

## 二、Linux显卡驱动篇：由于AMD显卡方面在Linux上开源，所以在Linux上显卡我更偏向于使用AMD而不是英伟达

### AMD显卡篇

* 目前仍在探索阶段，暂且总结一下自己认知下的情形：

* 1、首先是AMD官方自己为Linux制作的fglrx系列：这是闭源的，也正因为如此，所以并不能随着Linux各发行版的更新直接安装，会逐渐出现不兼容。当AMD官方停止更新后，那么这块显卡在更新的Linux发行版上也就随之丧失了这款驱动。

* 2、mesa3D驱动：非AMD官方开源驱动，这是一款在Linux上不仅限于支持AMD显卡的显卡驱动，可以支持OGL、VLK等API，更新很及时，如果显卡在后期不再受官方的支持，我想可能这是最好的选择了。

* 3、AMDVLK开源驱动：AMD的开源驱动项目，貌似可以更持久的维护显卡，但是只支持RX400及以上的显卡，更老的显卡没有办法使用。

### 英伟达显卡篇

* 1、英伟达官方闭源驱动：拓展名为.run的官方驱动，安装该驱动要屏蔽掉Nouveua开源驱动，否则冲突，经过测试英伟达官方驱动在安装时一般会自动进行屏蔽（加入黑名单处理），如果未处理请手动添加，关键词：blacklist。官方驱动更新频率不错，经过测试对游戏和模拟器效率要更好，但是因为某些我不懂的原因，Linus祖师爷表示F**K NVIDIA!

* 2、Nouveua：英伟达非官方开源驱动，英伟达似乎并不认可，经过测试对游戏和模拟器效率不如官方驱动，不过日常功能都算尚可，安装Ubuntu时作为N卡的默认驱动。

* 3、Linux下英伟达有个控制面板叫做NVIDIA X Server Settings，需要注意的是双显卡笔记本（核显+独立N卡）这种要安装prime-select然后prime-select nvidia让N卡独立工作才可以解决各种奇奇怪怪的问题，比如全屏撕裂问题。

### 英特尔显卡篇

* 关于英特尔的显卡，不管是独立显卡还是核显，英特尔似乎都将相关数据分发到各Linux发行版供应商手里，由这些Linux发行版供应商自行开发并支持，目前未找到英特尔官方发行的任何Linux驱动安装包。

### 其他硬件驱动篇

* 虚拟机暂且不提，我一共测试了三套不同年代的平套，他们分别是笔记本AMD A8-4500M，笔记本英特尔 酷睿I5-7300HQ + 1050Ti，台式AMD 锐龙5900X + 1060 + B450F，通过实际的真机ubuntu安装测试，其他硬件驱动似乎都已经被Ubuntu内置集成好的驱动良好的驱动起来了，部分硬件比如无线网卡安装Ubuntu后默认是没有驱动成功的，通过有线网卡或其他可以直接驱动起来的无线网卡，联网更新也可以驱动起来，大多数硬件没有问题，少数Ubuntu没有为其集成驱动的依然是有问题的，这部分硬件的解决办法要么是找硬件厂商网站查看是否有相应驱动，要么去其他网站寻找代码自行编译，还是有一定门槛的。所以我的建议还是尽可能选择Ubuntu默认或者通过后续联网就能支持的硬件。硬件的驱动是否被Ubuntu集成，很大程度的因素应该是他本身的驱动是否开源了，退一步至少他应该发布过闭源驱动，再退一步恐怕就只能是至少被人逆向出来过。

## 三、家用娱乐：调试、影音、网络

* 一款叫做corectrl的工具可以充当AMD显卡和AMD、英特尔CPU的图形控制面板，风格类似于AMD的深红/肾上腺素UI，另一款叫做corepower的带有图形界面的工具，基于BIOS调用CPU的策略，精准指定CPU频率范围。

* 浏览器和播放器用优秀的跨平台软件Firefox和mpv，注意火狐在登陆账号上是可以去反复切换国际账号和国内账号的，火狐不存在网络问题，因此推荐国际账号，mpv方面因为图形api和Windows有很大不同，所以设置方面也要多注意图形api调用的问题（vulkan、opengl、waylandvk、x11vk、wayland、x11）。 https://github.com/redomCL/mpv_fruit/tree/Linux-mpv

* Ubuntu内置Openvpn方便了很多回家需要的部署，远程则可以用apt库中的Remmina工具。

* P2P方面，Linux当然更不缺少相关工具，我依然喜欢使用一直最常用的qbittorrent，这是我唯一觉得比Windows平台上的同款更好看的带UI的工具。

# 这是一个笔记本，用来记录Linux桌面版日常家用笔记

![](https://github.com/redomCL/Linux-desktop-note/blob/main/Ubuntu.png)
![](https://github.com/redomCL/Linux-desktop-note/blob/main/duckstation.png)
![](https://github.com/redomCL/Linux-desktop-note/blob/main/gnome-software.png)
![](https://github.com/redomCL/Linux-desktop-note/blob/main/synaptic.png)

# 前言：
* Linux目前的发展相比Windows真的不适合日常家用娱乐，易用性要差的相当多，但是为了不完全依赖商业形式运转的Windows操作系统，我还是尽可能的去了解一下Linux，本合集为Linux为了日常家用娱乐为主的笔记。 具体主要用途：
*  1、家庭影音：主要以跨平台的优秀播放器mpv为主，也可以用基于mpv的gnome mpv、smplayer
*  2、网络通讯：微信、QQ、跨平台的优秀浏览器firefox
*  3、游   戏：steam和wine，Linux原生模拟器
*  ...

## 一、包管理相关：软件安装
* 实际上GNOME除了作为Ubuntu的桌面，同时也为大部分包管理器（软件商店）提供了一个图形界面，apt、snap、flatpak和dnf都可以用gnome-software作为图形包管理器（图形软件商店）

* deb/Ubuntu：Ubuntu；前端包管理器apt，图形前端包管理器synaptic/gnome-software，安装软件的基础。

* ubuntu snap：Ubuntu；前端包管理器snap，有图形前端snap-store/gnome-software，用于对apt的扩充。

* Flathub：多种Linux桌面发行版；前端包管理器flatpak，图形前端包管理器gnome-software，用于对apt的扩充。包含大量游戏模拟器软件。

* Fodera/RedHat RPM：Fodera；RedHat；前端包管理器dnf，图形前端包管理器gnome-software。

* fuse：用户空间文件系统，用于对apt的扩充，ubuntu下通过apt安装libfuse2，实现对appimage独立包的直接运行。

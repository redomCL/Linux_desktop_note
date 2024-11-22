# 这是笔记，用来记录Linux桌面版日常家用的经历

![](https://github.com/redomCL/Linux-desktop-note/blob/main/Ubuntu.png)
![](https://github.com/redomCL/Linux-desktop-note/blob/main/duckstation.png)

# 前言：
* 目前Linux桌面发行版的发展相比Windows真的不适合日常家用娱乐，易用性要差的相当多；当然了，Linux桌面发行版目前的软件生态也真的满纯粹，绝大多数软件都可以默认安装，没有广告没有额外的骚扰，不需要像Windows一样每接触新的软件都要特别小心怕被捆绑等其他骚扰，目前Linux桌面发行版的软件生态问题主要还是1.软件不够，大多数厂商因为利益关系都没有动力在Linux桌面发行版上发布较新的家用软件；2.虽然有开源软件，但是这种非利益驱动下的软件表现参差不齐，有功能和界面都很差的，也有功能强大界面极其粗糙的，对普通家用用户来说非常不友好；3.Linux桌面发行版非常碎片，各种包管理器和图形化软件商店以及各种桌面眼花缭乱，另外个人虽然觉得各种桌面很华丽，但是手感上觉得是不如Windows的，无论是GNOME还是KDE，都有一种边界判定不清晰，“粘手”的感觉；4.依赖问题相当头大，相应的解决办法就是依靠包管理器，但是就像3中所说的，包管理器本身都相当碎片。以上，但为了不完全依赖商业形式运转的Windows操作系统这种独（毒？）苗，我还是尽可能的去了解一下Linux桌面发行版，本合集是Linux桌面发行版为了日常家用娱乐为主的笔记。 具体主要用途：
* 1、家庭影音：主要以跨平台的优秀播放器mpv为主，也可以用基于mpv的gnome mpv、smplayer
* 2、网络通讯：微信、QQ、跨平台的优秀浏览器firefox
* 3、游戏：steam和wine，Linux原生模拟器
* ...

## EX1、快速运行篇&系统设置完善篇：在介绍包管理前记录一些快捷笔记
* 关于/usr：bin目录放可执行文件，lib目录放库文件，share目录放必要数据，由系统包管理器管理，安装的各种包都在这里；/usr/local里面的这三个目录由用户自己手动管理，放自行下载的程序，系统包管理器不管理；/home/users/.local：此处这三个目录是用户自己的目录，用户自己管理，自己使用。
* 列举所有硬件：sudo lshw，查看网卡型号：`lspci | grep -i net`，查看蓝牙：`hciconfig -a`
* 完善图形apt：安装apt图形管理工具新立得：`sudo apt install synaptic`
* 运行当前目录程序：./xxx.xxx可运行当前目录下可执行程序，图形下可直接拖拽到终端运行，`chmod +X ....`开启可执行程序权限。
* 独立可执行程序：executable/appimage这类独立可执行程序目前依赖要根据不同软件的说明而定，根据目前遇到的，mesen.executable需要.net，cegui，而mesen.appimage需要afuse，注意在ubuntu24.04.1下，安装fuse会引起删除桌面等重要组建，注意区分afuse和fuse，总之，运行appimage要注意fuse，linux任何时候都要考虑依赖（类似windoiws运行库？）。
* 如果桌面环境受损，参考以下：ctrl+alt+Fx唤起TTY，运行apt命令重新安装，例如：`sudo apt install ubuntu-desktop`,注意两点，一是注意apt库更新防止出错，二是运行sudo apt时可能出现菱形，此为提示输入root申请密码，按回车结束开始执行，安装桌面可能很慢。
* 安装flathub：flathub有大量软件尤其是仿真器，而且更新速度非常快，可以查看flathub官网底部的设置教程，参考命令：sudo install flatpak
* 注意ubuntu会包含专用闭源驱动：如果硬件设备有没正常工作的，可以运行附加驱动，会自动查找一些专用设备驱动。
* nautilus启用rootmode和smb：root组件：sudo apt nautilus-admin，smb组件：`sudo apt nautilus-share`,部署smb：部署用户组：`sudo usermod -aG sambashare $(whoami)`后重启，设置smb密码：`sudo smbpasswd -a $(whoami)`，否则报错权限不够。对于访问windows非全盘共享，可尝试输入完整分享路径，例：`smb://192.168.110.124/users/`，可能出现无限提示输入账号密码，可尝试输入自己linux的登陆账号和密码。nautilus可创建连接（快捷方式）。
* 远程回家：ubuntu自带openvpn，直接导入配置文件然后输入密码即可。
* 蓝牙：专用驱动虽然在ubuntu中已经包含，但实际仍可能有问题，对于搜索不到设备的情况，可`sudo dmesg | grep -i blue`查找缺少问题，如遇到缺少固件，则进行补足`sudo cp ”缺失部分" /lib/xxx/xxx/`，`sudo modprobe -r btusb`，`sudo modprobe btusb`
* 系统语言方面：在系统-区域与语言中，对语言全面设置中文，即可将所有软件默认语言处于中文状态，并且会包含中文输入法，fcitx只是一种输入法可以卸载，对于libreoffice安装后如果是英文，可以在包管理中搜索中文包。
* 让独立可运行程序能固定在dock并且显示图标：以火狐的样板为例，创建.desktop，编辑后放入`/usr/local/share/applications`，创建一个快捷链接，放入：`/usr/local/bin`
  `[Desktop Entry]`

  `Version=1.0`

  `Name=Firefox Web Browser`

  `Comment=Browse the World Wide Web`

  `GenericName=Web Browser`

  `Keywords=Internet;WWW;Browser;Web;Explorer`

  `Exec=firefox %u`

  `Terminal=false`

  `X-MultipleArgs=false`

  `Type=Application`

  `Icon=/opt/firefox/browser/chrome/icons/default/default128.png`

  `Categories=GNOME;GTK;Network;WebBrowser;`

  `MimeType=text/html;text/xml;application/xhtml+xml;application/xml;application/rss+xml;application/rdf+xml;image/gif;image/jpeg;image/png;x-scheme-handler/http;x-scheme-handler/https;x-scheme-handler/ftp;x-scheme-handler/chrome;video/webm;application/x-xpinstall;`

  `StartupNotify=true`

## EX2、权限管理篇：
* root是一个用户，对系统拥有最高权限：`root	ALL=(ALL:ALL) ALL`，sudo是一个root创建的用户组，该用户组下的所有用户可以申请root的权限来执行工作（%用于标识该名字是用户组，`ALL=(ALL:ALL) ALL`表示`主机=(用户:用户组) 命令`）：`%sudo	ALL=(ALL:ALL) ALL`。查看用户的权限：`sudo -l -U user_name`,查看用户所在组：`groups user_name`，列举sudo用户组的用户：`getent group sudo`。
* 因此，在操作系统中，如果希望用户以root权限免密码运行工作则改为：`%sudo	ALL=(ALL:ALL) NOPASSWD:ALL`。但此时图形下运行需要root权限的工作仍然需要密码，尚未解决此问题。
* 当用户不在sudo用户组，则无法以root权限工作（可能的提示是：用户名不在sudoers文件中），此时需要将用户添加到sudo用户组：`usermod -a -G sudo <users>`。同样的反推：将用户从sudo用户组删除：`sudo deluser <users> sudo`。
* 各种情况导致失去root密码：开机时按住shift+tab显示grub。按下e编辑：`rw init=/bin/bash`替换`ro Quiet Splash $vt_handoff`，之后可执行无密码root进行维护(如`passwd`修改root密码)。`exec /sbin/init`刷新配置并退出维护。

## 一、包管理篇：软件安装

* Linux发行版不同于Windows的软件安装习惯，Linux发行版一般有自己的在线软件库（各国都有镜像源解决不能访问的问题），并通过搭配内置的包管理器（命令行/图形界面）进行管理，以下是一些用过的包管理器列举。

* GNOME的桌面环境，同时提供了一个图形界面的包管理器gnome-software(软件商店)，各种命令行包管理器都可以通过它实现图形界面包管理器，同理的还有KDE桌面的plasma-discover(Discover软件管理中心)。

* Debian/Ubuntu .deb：命令行包管理器apt，专有图形界面包管理器synaptic。删除PPA仓库:`sudo add-apt-repository --remove ppaname`

* Ubuntu .snap：命令行包管理器snap，专有图形界面包管理器snap-store。

* RedHat/Fedora .RPM：命令行包管理器器dnf，默认使用图形包管理器gnome-software。

* openSUSE .RPM：命令行包管理器zypper，默认使用图形包管理器Yast2/Discover软件管理中心。

* *executable：独立可执行程序，可能依赖cegui，.net，根据具体软件而定。

* *fuse .appimage：用户空间文件系统，用于对apt的扩充，ubuntu下通过apt安装libfuse2，实现对appimage独立包的直接运行。注意"fuse"对系统的破坏，注意可能需要"afuse"。

* *Flathub .flatpak：包含大量游戏模拟器软件和主流软件，flathub已经兼容大多数主流系统（ubuntu/debian/fedora/deepin/mint/opensuse），具体部署可查看flathub官网页尾的设置教程。部分系统已经默认内置无需设置。部分系统下可依赖图形工具管理，比如gnome-software，也可以在浏览器或终端下管理。未来版本可能修复的：当前ubuntu下的gnome-software下运行报错，解决方法为在/etc/apparmor.d创建bwrap，内部添加：

  `abi <abi/4.0>,`

  `include <tunables/global>`

  `profile bwrap /usr/bin/bwrap flags=(unconfined) {`

  `  userns,`

  `  # Site-specific additions and overrides. See local/README for details.`

  `  include if exists <local/bwrap>`

  `}`

  执行：`sudo systemctl reload apparmor`

![](https://github.com/redomCL/Linux-desktop-note/blob/main/gnome-software.png)

![](https://github.com/redomCL/Linux-desktop-note/blob/main/synaptic.png)

![](https://github.com/redomCL/Linux-desktop-note/blob/main/flathub部署1.png)

![](https://github.com/redomCL/Linux-desktop-note/blob/main/flathub部署2.png)

![](https://github.com/redomCL/Linux-desktop-note/blob/main/flathub部署3.png)

## 二、Linux显卡驱动篇：由于AMD显卡方面在Linux上开源，所以在Linux上显卡我更偏向于使用AMD而不是英伟达

### AMD显卡篇

* 目前仍在探索阶段，暂且总结一下自己认知下的情形：

* 1、首先是AMD官方自己为Linux制作的fglrx系列：这是闭源的，也正因为如此，所以并不能随着Linux各发行版的更新直接安装，会逐渐出现不兼容。当AMD官方停止更新后，那么这块显卡在更新的Linux发行版上也就随之丧失了这款驱动。

* 2、mesa3D驱动：非AMD官方开源驱动，这是一款在Linux上不仅限于支持AMD显卡的显卡驱动，可以支持OGL、VLK等API，更新很及时，如果显卡在后期不再受官方的支持，我想可能这是最好的选择了。

* 3、AMDVLK开源驱动：AMD的开源驱动项目，貌似可以更持久的维护显卡，但是只支持RX400及以上的显卡，更老的显卡没有办法使用。

### 英伟达显卡篇

* 1、英伟达官方闭源驱动：拓展名为.run的官方驱动，安装该驱动要屏蔽掉Nouveua开源驱动，否则冲突，经过测试英伟达官方驱动在安装时一般会自动进行屏蔽（加入黑名单处理），如果未处理请手动添加，关键词：blacklist。官方驱动更新频率不错，经过测试对游戏和模拟器效率要更好，但是因为某些我不懂的原因，Linus祖师爷表示F**K NVIDIA!开机登陆界面，右下角齿轮可切换x11/wayland。

* 2、Nouveau：英伟达非官方开源驱动，英伟达似乎并不认可，经过测试对游戏和模拟器效率不如官方驱动，不过日常功能都算尚可，安装Ubuntu时作为N卡的默认驱动。

* 3、Linux下英伟达有个控制面板叫做NVIDIA X Server Settings，需要注意的是双显卡笔记本（核显+独立N卡）这种要安装prime-select然后prime-select nvidia让N卡独立工作才可以解决各种奇奇怪怪的问题，比如全屏撕裂问题。

* 英伟达新的闭源驱动开始逐渐支持wayland，但是也可能有各种问题，在基于GNOME桌面环境的Ubuntu中，注意/usr/lib/udev/rules.d/61-gdm.rules这个文件，它在影响wayland和x11之间的切换。 

### 英特尔显卡篇

* 关于英特尔的显卡，不管是独立显卡还是核显，英特尔似乎都将相关数据分发到各Linux发行版供应商手里，由这些Linux发行版供应商自行开发并支持，目前未找到英特尔官方发行的任何Linux驱动安装包。

### 其他硬件驱动篇

* 虚拟机暂且不提，我一共测试了三套不同年代的平台，他们分别是笔记本AMD A8-4500M，笔记本英特尔 酷睿I5-7300HQ + 1050Ti，台式AMD 锐龙5900X + 1060 + B450F，通过真机安装Ubuntu测试，其他硬件驱动似乎都已经被Ubuntu内置集成好的驱动良好的驱动起来了，部分硬件比如无线网卡安装Ubuntu后默认是没有驱动成功的，通过有线网卡或其他可以直接驱动起来的无线网卡，联网更新也可以驱动起来，大多数硬件没有问题，少数Ubuntu没有为其集成驱动的依然是有问题的，这部分硬件的解决办法要么是找硬件厂商网站查看是否有相应驱动，要么去其他网站寻找代码自行编译，还是有一定门槛的。所以我的建议还是尽可能选择Ubuntu默认或者通过后续联网就能支持的硬件。硬件的驱动是否被Ubuntu集成，很大程度的决定因素应该是他本身的驱动是否开源了，退一步至少他应该发布过闭源驱动，再退一步恐怕就只能是至少被人逆向出来过。此外Ubuntu和其他Linux桌面发行版一般是不内置闭源驱动的，这类驱动被收纳在库里，需要安装系统后联网选择，更激进的Linux桌面发行版甚至根本就不收纳闭源形式的驱动。

![](https://github.com/redomCL/Linux_desktop_note/blob/main/Linux%E8%8B%B1%E4%BC%9F%E8%BE%BE%E9%A9%B1%E5%8A%A8.png)

![](https://github.com/redomCL/Linux_desktop_note/blob/main/NVIDIA%20X%20Server%20Settings.png)

![](https://github.com/redomCL/Linux_desktop_note/blob/main/N%E5%8D%A1%E6%AD%A3%E5%B8%B8%E8%AF%86%E5%88%AB.png)

## 三、家用娱乐篇：调试、影音、网络

* 浏览器：注意火狐在登陆账号上是可以切换国际账号和国内账号的，火狐不存在网络问题，因此推荐国际账号。Linux下的火狐默认不会在新标签打开网页，about:config自定义一些使用习惯：

  新标签打开搜索：`browser.search.openintab=true`

  新标签打开链接：`browser.urlbar.openintab=true`（如果安装了标签页优化组件则不需要修改此项）

  新标签打开书签：`browser.tabs.loadBookmarksInTabs=true`

* 播放器：音乐播放器：clementine，视频播放器：mpv因为图形api和Windows有很大不同，所以设置方面也要多注意图形api调用的问题（vulkan、opengl、waylandvk、x11vk、wayland、x11）。 https://github.com/redomCL/mpv_fruit/tree/Linux-mpv，当前默认设置在/.config/mpv。

* P2P下载：qbittorrent是跨平台工具，Linux上提供了多个可执行格式。

* Ubuntu内置OpenVPN：直接导入配置文件然后输入密码即可回家，几乎不需要额外部署设置，远程则可以用apt库中的Remmina工具。

* 远程控制：ubuntu 23.10实际上已经内置远程控制并支持Windows的RDP协议，但在实际使用时，以Windows10 22H2为例并不能正常连接，提示"发生身份验证错误，有更多数据可用"，所以要通过sudo apt install tightvncserver xrdp命令安装xrdp实现。Linux的远程控制和Windows的登录思路有所不同，远程控制实际是使用用户在远程登录并控制电脑，在Linux中，远程控制不能注销当前本地已登录的用户，然后在远程重新登录以完成远程控制，因此远程控制如果想用当前本地已登陆的用户登陆，首先要确保这个用户已经在本地注销！否则远程控制失败。

## 四、Linux下的引导和轮转：
* Linux现在在UEFI标准下使用GRUB2实现引导链。Windows从8开始在UEFI标准下下使用自己的bootmgfw实现引导链。目前bootmgfw不能跳转到GRUB2（Windows的引导加载Linux很麻烦），但是GRUB2支持跳转到bootmgfw（Linux的引导加载Windows），所以Linux和Windows真机共存一般是选择用GRUB2引导。"sudo GRUB_DISABLE_OS_PROBER=true update-grub"命令可以允许GRUB2自动搜索其他操作系统，以此将Windows添加到GRUB2，之后详情可在Linux桌面发行版环境下使用图形工具GRUB Customize进行配置(sudo add-apt-repository ppa:danielrichter2007/grub-customizer -y)，比如引导菜单驻留时间、引导项、引导菜单界面定制。另注意一款引导修复工具：boot-repair。

![](https://github.com/redomCL/Linux_desktop_note/blob/main/GRUB2.jpg)

## 五、GNOME插件篇：GNOME桌面可以安装插件增强功能，以下是例举我个人必备的插件，（名为”扩展管理器“的软件是GNOME的插件管理面板，是核心工具）

*  vitals：监视CPU、内存、网速等设备状态。

*  corectrl：CPU、GPU设置工具。

*  Blur my shell：毛玻璃效果

*  Burn My Windows：窗口开启关闭动效

*  Compiz alike magic lamp effect:窗口最大化最小化动效

*  Compiz windows effect：窗口移动特效

*  Coverflow alt-tab：切换窗口特效

*  windows窗口习惯：Ubuntu dock - 行为设为最小化或显示预览

*  Dynamic Top Panel（已有替代）：状态栏设置

*  ![](https://github.com/redomCL/Linux-desktop-note/blob/main/扩展管理器.png)

## 不明问题但解决篇：我能力有限认知不足，这是我的问题

* /etc/profile.d/vte.sh丢失：`cd /etc/profile.d`，`ls`，输出将包含一个文件，例如 vte-XXX.sh，输入`cp vte-XXX.sh vte.sh`，问题修复。
 

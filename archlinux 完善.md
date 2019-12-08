### network manager 
> *Use `systemctl --type=service` to ensure that no other network service is running before enabling a _netctl_ profile/service.*


1. #### NetworkManager.service 
    > `cli: nmcli / nmtui`

	1. List nearby wifi networks:

		```
        nmcli device wifi list
        ```

	2. Connect to a wifi network:**
		```
		nmcli device wifi connect "kktt" password "12345678"
		```

	3. See a list of network devices and their state:

		```
		nmcli device
		```

	4. Turn off wifi:

		```
		nmcli radio wifi off
		```

2. #### archiso: netctl (wpa_supplicant dhcpcd dialog) 
	> `cli: netctl / wifi-menu`


=========================
临时
=============
## archlinux install

> [参考1](<https://blog.allenchou.cc/arch-linux-tutorial/>)  [参考2](<https://autostudentsite.wordpress.com/2018/08/07/arch-linux-dell-inspiron-15-7577/>)  [参考3](<https://archcheatsheet.com/cheatsheet/arch-chroot.html#locale>)  [参考4](<https://learnku.com/articles/13588/arch-linux-detailed-installation-configuration-in-multisystem?order_by=created_at&>)  [参考5](<https://gimo.me/post/from-macos-to-archlinux/>)  [参考6](<https://blog.inofd.com/2018/06/01/archlinux-install-guide.html>)  [参考7](<https://blog.51cto.com/jxnewdate/1879418>) [参考8](https://io-oi.me/tech/hello-arch-linux/) [参考final](<https://blog.inofd.com/2018/06/01/archlinux-install-guide.html>)  [关于efi](<https://blog.51cto.com/jxnewdate/1879418>)

### DD镜像:

- windows使用rufus(dd模式,老主板主要添加bios支持)

- gun/linux使用: `dd bs=4M if=/path/to/archlinux.iso of=/dev/sdx status=progress && sync`

- 查看是否以UEFI启动

  ```
ls /sys/firmware/efi/efivars # 如果提示efivars不存在，则不是UEFI启动。
  ```

  

  - 查看USB是否占用，如果占用(小数字):

    `umount /dev/sdbxx` 

  - 如果需要格式化 U 盘：

    `mkfs.vfat /dev/sdb -I`

  - 查看磁盘-f可不加:
  
    df -h
  
    blkid
  
    `lsblk -f`(推荐)
  
    fdisk -l
  

### 分区

```
wifi-menu    # 连网
```

  	ping -c 3 www.baidu.com 检查网络

>  To see the networking devices detected.

```
ip addr
```

- 分区：cgdisk (UEFI)/ cfdisk (MBR&UEFI)

  `cgdisk /dev/sdb`

  >  ef00 EFI   
  >
  > 8300 Linux filesystem  
  >
  > 8200 Linux swap  
  >
  > 0700 Microsoft basic data 
  >
  >  0c01 Microsoft reserved  
  >
  > 2700 Windows RE  
  >
  > #partprobe 立即生效，不需重启

- 格式化和挂载

  ```bash
  mkfs.vfat -F32 /dev/sda1 #有则不需要

  mkfs.ext4 /dev/sda4 #archlinux
  
  mkswap /dev/sda3
  
  swapon /dev/sda3  //关闭用 swapoff /dev/sda3 //开启:swapon -s //查看swapon --show
  cat /proc/sys/vm/swappiness ///etc/sysctl.conf设置vm.swappiness=25 //archlinux wiki:/etc/sysctl.d/99-swappiness.conf  vm.swappiness=10 可以彻底删除 sudo rm /swapfile
  
  mount /dev/sda4 /mnt //这是Linux的根/（分区）
  
  mkdir /mnt/boot //把boot分区挂载到此目录
  
  mount /dev/sda1 /mnt/boot //挂载ESP分区到/mnt/boot
  ```
```
  
  mkfs.ntfs /dev/sdb5 microsoft basic data


	**进入chroot再修改社区仓库并安装钥匙**
	
	`sudo pacman -S archlinux-keyring archlinuxcn-keyring`

### 联网:

`wifi-menu`

### 设置时间同步

`timedatectl set-ntp true`

### 安装基本系统

`pacstrap /mnt base`

### 配置并验证系统

`genfstab -U /mnt >> /mnt/etc/fstab`

**验证是否成功mount**

`cat /mnt/etc/fstab`

### 同步时间

timedatectl set-ntp true

### nano快捷

```
^G 查看帮助
^	Ctrl
M-	Alt
复制一整行：Alt+6
剪贴一整行：Ctrl+K
粘贴：Ctrl+U
查找: Ctrl+W
重复上一次搜索: Alt + W
Alt +\ 跳转至第一行
Alt+/跳转至最后一行
Ctrl+Y 前一屏
Crll +V 后一屏
撤销: Ctrl+C
保存: Ctrl+O
退出 : Ctrl+X
Ctrl+A 到行首 
Ctrl+E 到行尾
Alt +(或者9到段落开头
Alt +)或者0到段落结尾

```

### mirrorlist

- 官方中文仓库:

```
  ## China
  Server = https://mirrors.cloud.tencent.com/archlinux/$repo/os/$arch
  Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
  Server = https://mirrors.sjtug.sjtu.edu.cn/archlinux/$repo/os/$arch
  Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
  ```

- 中文社区仓库:

  ```
  [archlinuxcn]
  Server = https://mirrors.cloud.tencent.com/archlinuxcn/$arch
  [archlinuxcn]
  Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
  [archlinuxcn]
  Server = https://mirrors.sjtug.sjtu.edu.cn/archlinux-cn/$arch
  [archlinuxcn]
  Server = https://mirror.xtom.com.hk/archlinuxcn/$arch
  ```
  
  其他地区用:
  
  [archlinuxcn]
  Server = https://cdn.repo.archlinuxcn.org/$arch

  ```
sudo pacman -Syy && sudo pacman -S archlinux-keyring archlinuxcn-keyring
```



lib32打头的需要开启multilib，把/etc/pacman.conf文件中的下面两行取消注释，然后执行pacman -Sy

**如果key有问题**

> 关于KEY的救急
> rm -R  /etc/pacman.d/gnupg/      # 删除gnupg目录及其文件
> pacman-key --init
> pacman-key --populate archlinux
> pacman-key --populate archlinuxcn    # 启用了archlinux中文软件库的还要执行这个

###REPO for MEGA###
  [DEB_Arch_Extra]
  SigLevel = Optional TrustAll
  Server = https://mega.nz/linux/MEGAsync/Arch_Extra/$arch
  ###END REPO for MEGA###

- 排列源

`sudo pacman-mirrors -i -c China -m rank`

```
$ pacman -Syy #更新源
```



## arch-chroot /mnt

​```sh
arch-chroot /mnt //不需要 /bin/zsh 因为没有安装
```

###　设定时区:

ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime 

tzselect

>tzselect命令只告诉你选择的时区的写法，并不会生效。所以现在它还不是东8区北京时间。你可以在.profile、.bash_profile或者/etc/profile中设置正确的TZ环境变量并导出。 例如在.profile里面设置
>
>TZ='Asia/Shanghai'; export TZ     

###时间同步

```
$ pacman -S ntp
$ ntpdate time.nist.gov
启动网络时间同步 
sudo timedatectl set-ntp true
```

### 键盘默认已设置好

> /etc/vconsole.conf` 添加 `KEYMAP=us`, 也可以不设置，默认为us
>
> ```
> # echo KEYMAP=us > /mnt/etc/vconsole.conf
> ```

### 生成/etc/adjtime:

hwclock --systohc --utc //将UTC时间写入BIOS，适用于UTC=yes,使用 localtime 标准那么系统时间不会根据夏令时自动调整

### 语言环境

1. > vi /etc/locale.gen     # 把en_US.UTF-8 UTf-8,zh_CN.GBK GBK,zh_CN.UTF-8 UTF-8,zh_CN GB2312,zh_HK.UTF-8、zh_TW.UTF-8前面的注释去掉

    或者

   	> echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
   	>
   	> echo "zh_CN.UTF-8 UTF-8" >> /etc/locale.gen



2. > echo "LANG=en_US.UTF-8" > /etc/locale.conf

   或者 

   > vi /etc/locale.conf 添加一行LANG=en_US.UTF-8

   不要在这里把系统全局设置成中文，因为终端无法显示中文，请单独将桌面环境设置为中文。

3. locale-gen

### 必要网络工具

pacman  -S wpa_supplicant dhcpcd dialog networkmanager dosfstools ntfs-3g neovim xclip git wget curl zsh bbswitch

>  net-tools #no need
>
> netctl # use netctl of wifi-menu
>
> NetworkManager #nmtui // systemctl disable netctl  //systemctl stop dhcpcd // sudo systemctl disable dhcpcd.service (会冲突)

> gvfs 自动mount文件系统 gnome的,kde不需要kde使用kio(包含在kf5中)
>
> ntfs-3g #ntfs文件支持

### 主机和网络

```
$ echo arch > /etc/hostname

vim /etc/hosts
作如下修改（将myhostname替换成你自己设定的主机名）

127.0.0.1   localhost.localdomain   localhost
::1     localhost.localdomain   localhost
127.0.1.1   arch.localdomain  arch
```



### 提前配置网络

到现在我们已经安装好了桌面环境，但是还有一件事情需要我们提前设置一下。由于我们之前使用的一直都是`netctl`这个自带的网络服务，而桌面环境使用的是`NetworkManager`这个网络服务，所以我们需要禁用`netctl`并启用`NetworkManager`：

```
sudo systemctl enable NetworkManager （注意大小写）
禁用防止与networkmanager冲突
sudo systemctl disable netctl #don't enable //systemctl --type=service
sudo systemctl enable dhcpcd.service
```

正解

<https://archcheatsheet.com/cheatsheet/arch-chroot.html#network-configuration>

<https://www.xennis.org/wiki/Network_tips>



  网络问题，一般用不到

  pacman -S dialog wpa_supplicant netctl wireless_tools wpa_actiond现在不安装 重启之后如果只有wifi则可能无法连接网络
  查看网卡名:
  ip link show
  设置启动dhcp:

  systemctl enable dhcpcd@enp0s2.service

Exit the chroot environment by typing `exit` or pressing `Ctrl+D`

### users和密码

```
# set the root password //root密码
$ passwd
```



```
useradd -m -g users -G wheel -s /bin/zsh kktt
```

passwd kktt

*/etc/resolv.conf* file.

```
nameserver 221.228.255.1
nameserver 114.114.114.115
```

### 安装sudo

pacman -S sudo

```bash
nano /etc/sudoers 编辑
去除其中"%wheel ALL=(ALL) ALL"行注释即可
另一种思路:添加以下
kktt ALL=(ALL) ALL
删除用户:sudo gpasswd -d kktt wheel
```

##　安装 grub

```
pacman -S dosfstools grub efibootmgr os-prober
```

update-grub用于检测添加其他系统

```
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub --recheck 
```

> // if you mount your EFI partition to `/boot`, you will still see a folder `/boot/EFI`. If you mount it to `/boot/efi`, you will see `/boot/efi/EFI`

```
grub-mkconfig -o /boot/grub/grub.cfg
```

### Intel

<https://github.com/GabMus/bestArch#microcode-updates>

```
sudo pacman -S intel-ucode
#Edit `/boot/loader/entries/arch.conf` so that the first `initrd` line is the following:  initrd        /intel-ucode.img
```

用 su 切换到刚建立的用户，然后编辑 ~/.config/locale.conf 修改自己的 Locale

## 重启

exit

umount -R /mnt

reboot

### 双显卡 

闭源显卡intel部安装

lspci | grep VGA # 查看显卡

pacman -Ss xf86-video　#查看哪些可以装 | less

pacman -S xf86-video-intel //Intel 的驱动是内核的 modesetting 驱动，在 Arch Linux 就是不安装 xf86-video-intel

```text
lsmod |grep -i nouveau //命令没有任何输出，则证明开源显卡驱动 nouveau 已被成功禁用
```

pacman -S nvidia nvidia-utils lib32-nvidia-utils //需启用multilib



不需要`xorg.conf`

/etc/X11/xorg.conf.d下10-optimus....自动生成:

```
Section "Device"
	Identifier "intel"
	Driver "modesetting"
	BusID "PCI:0:2:0"
	Option "DRI" "3"
EndSection
```

**以下弃用:**

> // 弃用方案pacman -S bumblebee bbswitch --noconfirm
>
> //sudo usermod -aG bumblebee $USER  #代表当前用户
>
> 8、使用NVIDIA图形   
>
> ​    安装NVIDIA就这样pacman -S bumblebee
> ​    lspci | grep -E "VGA|3D"
> ​    pacman -S mesa
> ​    pacman -S nvdia                                \闭源驱动，自行找寻version
> ​    pacman -S bumblebee                            \手动开启nvidia,可以不安装
> ​    gpasswd -a $USER bumblebee                      \大黄蜂添加用户
> ​    systemctl enable bumblebeed.service
> ​    pacman -S mesa-demos
> ​    optirun glxspheres64                           \检测3D是否启动
> ​    pacman -S bbswitch
> ​    sudo tee /proc/acpi/bbswitch <<< ON
> ​    sudo tee /proc/acpi/bbswitch <<< OFF
> ​    nvidia-smi
>
> nvidia闭源驱动出现黑屏修改
> /etc/X11/xorg.conf驱动改变的问题，修改里面
> Section "Device"
>     Identifier             "Device0"
>     Driver                 "intel"
> EndSection
> 我的集显示intel，独显示nvidia,安装nvidia闭源就出现过黑屏登录不了界面的问题，然后Identifier "intel"修改后就ok了



### 安装nvidia驱动后安装显卡切换

假如您已经预先安装了开源驱动nouveau，请确定已经从`/etc/mkinitcpio.conf`里面去除"nouveau"

sudo vim /etc/modprobe.d/nouveau_blacklist.conf 添加: blacklist nouveau  和 options nouveau modeset=0检查nouveau driver确保没有被加载 重建  initramfs image file : # mkinitcpio -p linux

## 重建mkinitcpio -p linux

- [optimus-manager](https://github.com/Askannz/optimus-manager) //需要配置中bbswitch switching=bbswitch

  - optimus-manager-qt](https://github.com/Shatur95/optimus-manager-qt) //通用前端配置

  KDE用户使用archlinuxcn 源

  ```
  sudo pacman -Sy optimus-manager-qt-kde
  ```

#### 配置 optimus-manager

在nvidia安装重启后安装

```
$ sudo mkdir -p /etc/optimus-manager
```

将 optimus-manager 默认配置拷贝一份到 `/etc/optimus-manager` 下面进行个性化配置:

```
$ sudo cp /usr/share/optimus-manager.conf /etc/optimus-manager/optimus-manager.conf
$ sudo vim /etc/optimus-manager/optimus-manager.conf
内容:
[optimus]
switching=bbswitch 
pci_power_control=yes
auto_logout=yes

[intel]
driver=modesetting
accel=
tearfree=
DRI=3
modeset=yes

[nvidia]
modeset=yes
PAT=yes
DPI=120
options=overclocking, triple_buffer

```

用法

```
$ optimus-manager --switch nvidia
```

```
$ optimus-manager --switch intel
```

设置开机使用intel

```
$ optimus-manager --set-startup=intel
```

更多用法：

```
$ optimus-manager --help
```

acpi 锁死问题, 如果你在用 `bbswitch` 并且遇到开机之后电脑直接卡死什么也动不了的问题，请尝试使用内核参数`acpi_osi="!Windows 2015"` 或 `acpi_osi=! acpi_osi="Windows 2009"`启动,还不行的话尝试`acpi_osi=! acpi_osi="Windows 2013"`  添加到/etc/default/grub` 并且在此行 `GRUB_CMDLINE_LINUX_DEFAULT 后面的引号里并sudo grub-mkconfig -o /boot/grub/grub.cfg

### 安装基本的图形环境以及驱动程序

pacman -S xorg-server

有SDDM不需安装:

~~1. pacman -S xorg-xinit~~
~~2. pacman -S xorg-twm xorg-xclock xterm~~

pacman -S mesa // 添加3D支持,上一个命令会自动安装

### KDE and SDDM

`kf5 kf5-aids plasma-nm plasma ntfs-3g sddm`



#### KDE 系统设置中配置终止 Xorg-server

浏览到子菜单：不要设置,会误触

```
   系统设置 > 硬件 > 输入设备 > 键盘 > 高级（标签） > "Key Sequence to kill the X server" 
```



Firefox 中使用 GTK 外观, 安装breeze-gtk和 [kde-gtk-config](https://www.archlinux.org/packages/?name=kde-gtk-config)  系统设置 -> 程序外观 -> GTK，GTK2/GTK3 主题选择为 Breeze，勾选显示 GTK 按钮的图标。

## 关于sddm  重点设置

安装了私有驱动的 provider 叫做 NVIDIA-0。如果不叫这个名字的话可以用`xrandr --listproviders`查看

```
# nano /usr/share/sddm/scripts/Xsetup
xrandr --setprovideroutputsource modesetting NVIDIA-0
xrandr --auto
```

运行 glxinfo 应该可以看到 OpenGL 的 vendor

```
$ glxinfo | grep "OpenGL vendor"
```

kde setting 设备设置numlock on

sddm-kdm 配置sddm  设置自动登录

kalletmanager

[kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) is not compatible with [GnuPG](https://wiki.archlinux.org/index.php/GnuPG) keys, the KDE Wallet must use the standard `blowfish` encryption. KDE Wallet 必须使用 `blowfish` 加密方式

重新建立一个 kdewallet 密码为空即可 关闭默认的wallet

disable *Close when last application stops using it* in KDE Wallet settings //设置 每次不需要解锁wifi

如果 kwallet Migration Assistant在每次登录之后都要求输入密码，请重命名或删除 `~/.kde4/share/apps/kwallet` 文件夹

### 首次生成用户文件夹

```
pacman -S xdg-user-dirs

xdg-user-dirs-update
```



### 驱动安装

- xf86-input-libinput   以下不再需要

  - 鼠键驱动

    ~~`xf86-input-mouse xf86-input-keyboard xf86-input-evdev`~~

  - 触摸板驱动

     ~~`pacman -S xf86-input-synaptics`~~

- 音频驱动

  `pacman -Sy alsa-utils pulseaudio pulseaudio-alsa`

  ```
  amixer sset Master unmute //取消静音
  ```

- 蓝牙驱动

  `pacman -S bluez bluez-utils blueman`

## 开机启动

#### ps:

```
如果你没有看到Arch Linux系统入口或者该文件不存在，请先检查/boot目录是否正确部署linux内核：

cd /boot
ls
查看是否有initramfs-linux-fallback.img initramfs-linux.img intel-ucode.img vmlinuz-linux这几个文件，如果都没有，说明linux内核没有被正确部署，很有可能是/boot目录没有被正确挂载导致的，确认/boot目录无误后，可以重新部署linux内核：

pacman -S linux
再重新生成配置文件，就可以找到系统入口。
```

### 添加用户组

~~gpasswd -a kktt audio~~

> - There is usually no need to add your user to the `audio` group, as PulseAudio uses [udev](https://wiki.archlinux.org/index.php/Udev) and *logind* to give access dynamically to the currently "active" user. Exceptions would include running the machine headless so that there is no currently "active" user.

gpasswd -a kktt video

gpasswd -a sddm video

> ```
>    效果一样
>    # usermod -a -G video sddm
>    # groupmod -aG video sddm
> ```

一些软件

**pacman -S okular** **yakuake**

```bash
sudo systemctl enable sddm.service    //设置桌面自启动 //sudo systemctl status sddm查看状态
sudo systemctl enable NetworkManager.service  //启用networkmanager
sudo systemctl enable optimus-manager.service
以下不需要
~~sudo systemctl enable tlp //桌面环境已有自己的方案~~
sudo systemctl enable bluetooth    //启用蓝牙
```



###安装 yay

```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

## 安装软件

sudo pacman -S kscreen dolphin dolphin-plugins filelight spectacle ark amarok okular p7zip-gui gwenview yakuake flameshot mpv gstreamer gst-libav gst-plugins-good aria2 transmission xdman tmux polybar udisks2 firefox-kde-opensuse packagekit-qt5 autojump 

OpenSUSE 打过补丁的、具有更好的 KDE 集成的 Firefox 版本

VLC可能在KDE有问题 用gstreamer即可 可以同时安装多个后端，并在 系统设置 > 多媒体 > 后端 中进行优先级设定

// 目前不需要 udisk2(磁盘管理) udev挂载

解压
sudo pacman -S p7zip-gui p7zip-plugins unrar tar

kde:  kf5 kf5-aids kdeutils kdebase kdeconnect kdenetwork

不需要 :kdenetwork

kde框架: kf5 kf5-aids  // krunner 包括在 kf5中 // KWin 是**window manager for KDE Plasma Desktops** 包含在plasma 中 //kdegraphics不需要

字体

`pacman -S noto-fonts-emoji ttf-dejavu otf-fira-code ttf-inconsolata ttf-symbola wqy-zenhei ttf-monaco ttf-hack`

monaco: 等宽非衬线

## yay 安装 aur 软件

yay mimeo (用于替换xdg-open打开软件)

yay chromium-widevine (解决web播放问题)

yay sierrabreeze-kwin-decoration-git (OSX-like window decoration for KDE Plasma)


### 软件配置问题

- yakuake:

> 不能激活问题 `killall -9 yakuake` 目前用ctrl + q

- 设置默认浏览器

>修改 ~/.config/mimeapps.list 文件
>
>把 firefox.desktop 都改成 chromium-browser.desktop
>
><https://github.com/mate-desktop/mate-control-center/issues/91>
>
> 
>
>~/.local/share/applications 里面的删除
>
>mimeapps [Default Applications] =google-chrome.desktop
>
>控制中心设置 google-chrome
>
>===========
>
>我默认的
>
>[Default Applications]
>
>text/html=kfmclient_html.desktop
>
>x-scheme-handler/http=google-chrome.desktop
>
>x-scheme-handler/https=google-chrome.desktop

- 浏览器字体

>firefox设置
>
>about:config
>
>layout.css.devPixelsPerPx 设置为1.2 就是120%
>
>all pages前面到勾去掉
>
> 
>
>chrome设置 系统设置DPI 120即可



### optomize

balooctl status 在系统设置里禁用搜索

balooctl status

balooctl disable

```
查看系统服务和时间
systemctl list-unit-files --type=service | grep enabled 
systemd-analyze blame 
systemd-analyze critical-chain systemd-logind.service
systemd-analyze critical-chain
systemd-analyze time
```



#### 禁用桌面特效

Plasma 默认启用了桌面特效，并且不是所有的游戏都会自动禁用它们。你可以通过*系统设置 > 桌面特效* 禁用桌面特效。你也可以使用 `Alt+Shift+F12` 切换桌面效果。另外，您也可以在 *系统设置 > 窗口管理 > 窗口规则* 下创建自定义KWin规则，以在某个应用程序/窗口启动时自动禁用/启用混合项。

#### 禁用混合项（compositing）

在 *系统设置 > 显示*中取消选中*启动时激活混合器（compositing）*并重启 Plasma





```
sudo pacman -Rns $(pacman -Qtdq)
systemctl enable upower
```

1. Arch Linux 在安装好以后，内核镜像默认没有载入 AHCI 驱动模块。修改 `/etc/mkinitcpio.conf`，添加 `ahci` 到 `MODULES` 变量：

   MODULES="ahci"

   然后重建内核镜像，重新启动后 AHCI 驱动就会加载：

   $ mkinitcpio -p linux

   dmesg查看效果

2. ```
   systemd-analyze #systemd-analyze blame 查看启动时间
   ```

### 输入法

pacman -S fcitx fcitx-rime fcitx-configtool fcitx-gtk2 fcitx-gtk3 fcitx-qt4 fcitx-qt5 kcm-fcitx

```
sudo echo -e "export GTK_IM_MODULE=fcitx\nexport QT_IM_MODULE=fcitx\nexport XMODIFIERS=@im=fcitx">>~/.xprofile
```

或者

```
export XIM=fcitx
export XIM_PROGRAM=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

libreoffice 需安装中文语言包 pacman -Ss libreoffcie 查找中文语言包名称

### oh my zsh

```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

```
sudo chsh -s /bin/zsh //设置为默认
```

```
oh-my-zsh的配置文件在~/.zshrc中，我喜欢将主题改为随机，这样每次打开终端都会有新鲜感。
ZSH_THEME="random"

chsh -s /bin/zsh
失败的话一用下面的地址
chsh -l
chsh -s /usr/bin/zsh

在切换 shell 为 zsh 后，启动系统会加载 ~/.zshrc 文件，而不会加载 ~/.bash_profile 文件（shell 为 bash 时才会执行），导致里面的设置无效，解决方法是在 ~/.zshrc 文件末尾加上以下代码，这样每次启动的时候就会执行  zsh 的配置：
修改后别忘了，source ~/.zshrc 生效。

查看当前当前系统PATH路径。
echo $PATH
使得刚修改的环境变量生效：source <带环境变量的文件>
查看环境变量： env 或 set 
持久化的环境变量主要存在于这几个文件中：
/etc/profile
/etc/environment
~/.bash_profile
~/.bashrc
加载优先级是：1->2->3≈4(3和4之间的优先级不大清楚)
其中1和2是系统的全局环境变量，3和4是用户个人的环境变量
```



cp .oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
vim ~/.zshrc

```bash
ZSH_THEME="ys"
plugins=(git archlinux systemd autojump sublime zsh-wakatime)
```

```
终端透明
在正在使用的 shell 的配置文件（~/.zshrc 或～/.bashrc）中加入如下代码，这两个文件是启动新 shell 时加载

if [ -n "$WINDOWID" ]; then
        TRANSPARENCY_HEX=$(printf 0x%x $((0xffffffff * 80 / 100)))
        xprop -id "$WINDOWID" -f _NET_WM_WINDOW_OPACITY 32c -set _NET_WM_WINDOW_OPACITY "$TRANSPARENCY_HEX"
fi
```

### zsh插件

```
upgrade_oh_my_zsh 更新
```

`$ZSH_CUSTOM` 其实是个变量，代表这个路径`~/.oh-my-zsh/custom`

1. Clone this repository into `$ZSH_CUSTOM/plugins` (by default `~/.oh-my-zsh/custom/plugins`)

   ```
   自动补全:
   git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
   高亮
   git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
   autojump(已内置) 需要source一下 source /etc/profile.d/autojump.bash
   git clone https://github.com/paulirish/git-open.git $ZSH_CUSTOM/plugins/git-open
   ```

2. Add the plugin to the list of plugins for Oh My Zsh to load (inside `~/.zshrc`):

   ```
   plugins=(git zsh-autosuggestions autojump git-open zsh-syntax-highlighting)
   git已默认加载 命令内容可以参考cat ~/.oh-my-zsh/plugins/git/git.plugin.zsh
   git别名放 插件里设置 参考配置(https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/robbyrussell/oh-my-zsh/blob/master/plugins/git/git.plugin.zsh)
   ```

zsh可以更强(<http://hczhcz.github.io/2014/03/27/oh-my-zsh.html>)

### ssr

> wget -P ./Downloads https://raw.githubusercontent.com/the0demiurge/CharlesScripts/master/charles/bin/ssr

进入刚刚克隆的仓库目录并赋予ssr脚本执行权限

cd Linux_ssr_script && chmod +x ./ssr
然后将脚本放入可执行脚本的目录

sudo mv ./ssr /usr/local/sbin/
这样就完成了脚本的安装

使用
输入ssr，便会有如下的提示：
ssr install
ssr start
ssr stop

### zsh tilix yakuake

[tilix配置](<https://gnunn1.github.io/tilix-web/manual/vteconfig/>)

zshrc文件

```
export ALL_PROXY=socks5://127.0.0.1:1080
alias setproxy="export ALL_PROXY=socks5://127.0.0.1:1080"
alias unsetproxy="unset ALL_PROXY"
alias ip="curl -i http://ip.sb"
if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
        source /etc/profile.d/vte.sh
fi
```

### 双系统同步时间

administrator运行

`reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_QWORD /f`

### [环境变量](<https://www.cnblogs.com/liduanjun/p/3536993.html>)

说明:

>  .bashrc: 每次终端登录时读取并运用里面的设置。
>
> .xinitrc: 每次startx启动X界面时读取并运用里面的设
>
> .xprofile: 每次使用gdm等图形登录时读取并运用里面的设

.zshrc

> alias setproxy="export ALL_PROXY=socks5://127.0.0.1:1080; export all_proxy=socks5://127.0.0.1:1080"
> alias unsetproxy="unset ALL_PROXY; unset all_proxy"
> alias ipp="curl -i http://ip.sb"
> if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
>         source /etc/profile.d/vte.sh
> fi
> export PATH=$PATH:/home/kktt/platform-tools
> export PATH=$PATH:/home/kktt/Downloads/software/comma-community-2019.4/bin
> export GTAGSLABEL=ctags
> export PATH=/home/kktt/rakudo/install/share/perl6/site/bin:/home/kktt/rakudo/install/bin:$PATH

.xprofile

> export GTK_IM_MODULE=fcitx
> export QT_IM_MODULE=fcitx
> export XMODIFIERS="@im=fcitx"



`echo $PATH`查看环境变量

一下读取顺序不一样，

首选:	`export PATH=$PAHT:<PATH 1>:<PATH 2>:<PATH 3>:--------:< PATH n >`

次选:	`export PATH=<1>:<2>:$PATH`

使得刚修改的环境变量生效：source <带环境变量的文件>

查看环境变量： env 或 set 

持久化的环境变量主要存在于这几个文件中：

```
/etc/profile
/etc/environment（系同级非登陆用户配置，不修改）
~/.bash_profile
~/.bashrc
```

加载优先级是：1->2->3>4 但是，读取后以用户为准

其中1和2是系统的全局环境变量，3和4是用户个人的环境变量

### python

创建软链接(源文件>目标文件---安装在mkdir -p /usr/local/python3)

**因为 linux 默认去 /usr/bin / 下找 pip3***

ln -s /usr/local/python3/bin/python3 /usr/bin/python3

配置环境变量`export PATH=$PATH:/usr/local/Python3.6/bin`

```
$ wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz
$ mkdir -p /usr/local/python3
$ tar -zxvf Python-3.6.1.tgz
$ cd Python-3.6.1
$ ./configure --prefix=/usr/local/python3
$ make
$ sudo make isntall
$ ln -s /usr/local/python3/bin/python3 /usr/bin/python3
```

```
python --version
whereis python3.5
rm /user/bin/python   删除软链接
重新设置软链接并设置路径
```

### perl6

[perlintro说明](<https://perl6intro.com/zh/>)

- **Perl 6**: 带有测试套件的语言规范。 Perl 6 是通过该规范测试套件的实现。
- **Rakudo**: Perl 6 的编译器。
- **Rakudobrew**: Rakudo 的安装管理器。
- **Zef**: Perl 6 的模块安装程序。
- **Rakudo Star**: 是一个包含 Rakudo, Zef, 和经遴选的 Perl 6 模块与文档的分发包。

`export PATH=/home/kktt/rakudo/share/perl6/site/bin:/home/kktt/rakudo/bin:$PATH`

**编辑器**

[vim-perl6](<https://github.com/vim-perl/vim-perl6>)

[atom](https://atom.io/packages/language-perl6)

[comma IDE](<https://commaide.com/>)



### software

[awesome-linux-software](<https://www.fossmint.com/awesome-linux-software/>)

[archlinux list_applications



## .gitconfig 内容

[user]
	name = kktt007
	email = kktt914968841@gmail.com
[core]
	editor = nvim

---



下载工具

XDM

SteadyFlow

## yay

```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

下载的软件在
/home/kktt/.cache/yay/rakudo-star

---

## grub 配置

sudo pacman -S grub-customizer  //grub设置工具

GRUB boot loader configuration**

GRUB_DEFAULT=saved
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="Arch"
GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet nomce nvidia-drm.modeset=1 intel_iommu=off acpi_backlight=none"
GRUB_CMDLINE_LINUX=""



GRUB_PRELOAD_MODULES="part_gpt part_msdos"

GRUB_GFXPAYLOAD_LINUX=keep

GRUB_DISABLE_RECOVERY=true



GRUB_SAVEDEFAULT="true"

acpi_osi=! acpi_osi=\\"Windows 2015\\" #一般不用,用的时候\可以去掉,加上感觉最好

### 黑屏方案

开机按E  在 quiet 后面空一格，加入 acpi_osi=! acpi="windows 2009"
保存，关闭
接着，在终端里输入
sudo gedit /etc/default/grub 
在弹出的文本页面的末尾加入
GRUB_CMDLINE_LINUX_DEFAULT="$GRUB_CMDLINE_LINUX_DEFAULT "'acpi_osi=! acpi_osi=\\"Windows 2009\\""

```
Non-graphical boot with systemd

进入纯命令

systemd.unit=multi-user.target //用于直接进命令
 然后F10
这也是一个办法
linux   /boot/vmlinuz-4.0.0-1-amd64 root=UUID=5e285652 ro  quiet 3

Runlevel │ Target            │
   ├─────────┼───────────────────┤
   │0        │ poweroff.target   │
   ├─────────┼───────────────────┤
   │1        │ rescue.target     │
   ├─────────┼───────────────────┤
   │2, 3, 4  │ multi-user.target │
   ├─────────┼───────────────────┤
   │5        │ graphical.target  │
   ├─────────┼───────────────────┤
   │6        │ reboot.target     │

查看显卡信息 lspci | grep -i vga 
Nvidia 卡信息的末尾不是 rev ff，表示独显是开启的。
lspci |grep -i 'VGA'    #查看默认集成显卡型号
lspci |grep -i nvidia  #查看NVIDIA类型的显卡型号
sudo dmesg | grep -i 'VGA'  #通过查看开机信息获取显卡信息

但很大可能是重启后发现无法进入图形化界面,你可以尝试在Grub菜单启动界面按[E]编辑，找到quite并在后面加入(注意空格):
acpi_osi=! acpi_osi=’Windows 2009’
或者
acpi_osi=! acpi_osi=Linux acpi_osi=’Windows 2015’ pcie_port_pm=off
(很多硬件厂商的BIOS驱动都对Linux不友好，无法顺利加载ACPI模块，而导致无法驱动独立显卡,acpi_osi=’Windows 2009’的意思是告诉ACPI模块，我是‘Windows 7’，别闹情绪了，赶紧工作吧。)
接着按[Ctrl] [x]或[F10]保存更改并启动系统。

顺利进入系统后打开终端更改配置文件
sudo vim /etc/default/grub

给 “GRUB_CMLINE_LINUX_DEFAULT”添加你可以正常启动Linux的‘acpi_osi’参数，如图我用的是’Windows 2009’。
```

## 关于4K对齐

[DiskGenius可以检测](<http://www.diskgenius.cn/exp/about-4k-alignment.php>)

2048 扇区 1048576 byte = 1M // msr分区保留16M MSR一般是未分配盘符的，因此就谈不上格式化了

4K= 4096 byte=512byte * 8 //默认扇区大小 512byte 物理扇区大小 4096 byte

扇区起始对齐为8扇区的倍数即可

## privoxy 配合ssr代理

参考网址
https://github.com/cckpg/autoproxy2privoxy
https://juejin.im/post/5c91ff5ee51d4534446edb9a
https://www.cnblogs.com/hongdada/p/10787924.html
https://www.zhangweijie.net/post/2016/05/17/2501.html
https://www.privoxy.org/user-manual/actions-file.html
https://blog.zfanw.com/privoxy-tutorial/

安装好后sudo systemctl start privoxy
sudo systemctl status privoxy
sudo systemctl restart privoxy

sudo systemctl start privoxy

sudo systemctl enable privoxy

等来配置测试

因为privoxy模式启用了listen-address  127.0.0.1:8118
系统设置以http 127.0.0.1 8118或者全部以127.0.0.1 8118为代理
/etc/profile写入

```
export ALL_PROXY='http://127.0.0.1:8118'
export all_proxy='http://127.0.0.1:8118'
export socks_proxy='socks5://127.0.0.1:1080/'
export SOCKS_PROXY=$socks_proxy
export no_proxy='localhost,172.16.0.0/16,192.168.0.0/16,127.0.0.1/8,10.10.0.0/16'
```

/etc/privoxy/config   监听地址 listen-address  0.0.0.0:8118  （如果是127.0.0.1 只能用于本地）

原理:  软件或者外部转发 8118端口(环境变量设置是为了系统内部的各种命令转发到代理本机8118 127.0.0.1代表本机)，系统代理把所有协议(支持http的，支持socks5)的转发给到本机8118。，privoxy监听指定地址0000代表全部网络上的使用的端口并转发到自己的规则(需要代理的转发给1080)，因为1080是全部代理，非1080规则设置的不转发。socks5监听来自privoxy的1080转发。

​	(内部修改环境变量为127.0.0.1 8118端口)，系统代理设置本机的127.0.0.1 8118 

```
#forward-socks5 / 127.0.0.1:1080 .
#forward 10.*.*.*/ .
#forward 192.168.*.*/ .
#forward .baidu.com/ .
#forward .ip111.cn/ .
actionsfile pac.action
```

因为使用了pac.action所以以上forward全部都注释掉即可

/etc/privoxy/pac.action

```
{{alias}}
direct      = +forward-override{forward .}
default     = +forward-override{forward-socks5 127.0.0.1:1080 .}
#==========默认代理==========
{default}
/
#==========直接连接==========
{direct} 
.12306.cn
```

检查:sudo ss -nltp | grep 8118

系统设置成http 127.0.0.1:8118

socks5 127.0.0.1 1080
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYzNzI5NzgwMiw5NjM5MTQ2MjcsMTMyOD
g0Njc5OCwtMTM2MzY0MzU3OCwtMjA4NjE5NTkyMSwxNjMzNTc2
MzUsLTEzMjI5MzQzODQsNDQyMTA5OTksLTUwMjk4NjM4OSwxNT
A5NTk0OTkzLC03NzczNzA5MTQsLTEwNjAzMDMzODZdfQ==
-->
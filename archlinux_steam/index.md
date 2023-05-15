# 在ArchLinux上安装Steam并运行拳皇13


![steam][image05]

>得益于`Proton`技术的支持，让我们可以运行`Steam`上的大部分游戏。  
今天`小王同学`就以`拳皇13`为例子来演示`ArchLinux`下安装`Steam`，快来一起看看吧！

{{< admonition >}}
Steam并没有为ArchLinux提供支持，Steam只对`Ubuntu LTS` 提供支持，因此首先你需要开启 `multilib` 库
{{< /admonition >}}

<!--more-->

本文主要参考了Arch Wiki[^wiki]

## 前置操作

编辑 `/etc/pacman.conf` 打开下面两行的注释即可
```bash
#[multilib]
#Include = /etc/pacman.d/mirrorlist
```

然后就可以安装 `steam` 了
```bash
sudo pacman -Syyu
sodo pacman -S steam
```

{{< admonition tip>}}
安装`Steam`时会让你选择依赖的32为图形驱动程序包，请根据你自己的显卡类型选择对应的驱动。  
由于我用的 `nvidia` 显卡驱动，因此我选的`lib32-nvidia-utils`
{{< /admonition>}}

然后安装一些字体，以支持中文
```bash
sudo pacman -S wqy-zenhei
sudo pacman -S noto-fonts-cjk
sudo pacman -S ttf-liberation
```

## 登录Steam

直接命令行运行 `steam` 即可，第一次运行会进行更新

![steam][image01]

## 设置Steam
更新完成后，登录你的`Steam`，我们需要开启`Proton`，它是`Linux`下运行`Windows`游戏必备的东西，它类似`Wine`

![steam][image02]

然后下载你的游戏即可，第一次下载会自动下载`Proton`

![steam][image03]

下载好后就可以愉快的玩耍了，哈哈

## 下面是拳皇13运行截图

![steam][image04]

>PS: 这两张图手机拍的

![steam][image05]
![steam][image06]

[^wiki]: [Arch Wiki Steam 安装文档](https://wiki.archlinux.org/title/Steam_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

[image01]: 01.png
[image02]: 02.png
[image03]: 03.png
[image04]: 04.png
[image05]: 05.png
[image06]: 06.png

# 在ArchLinux上安装MAME模拟器并运行拳皇97

{{< image src="running01.png" caption="最终运行效果" width="100%" height="100%" >}}

>事情的起因是这样的，我最近买了一台街机摇杆`拳霸Q4`，安奈不住激动的心情，马上就装了个`虚拟机`。  
然后通过虚拟机运行模拟器，再把USB接到虚拟机里来玩，但我发现，游戏总是玩不了多久就很卡。  

<!--more-->

## 采用VirtualBox+模拟器的方式的弊端
我用的虚拟机是[VirtualBox](https://www.virtualbox.org/)，增强功能那些都配置好了。 `显存`拉到了最大，开启了`3D加速`，  
内存和`CPU`也都给的比较大了，按理说玩个街机游戏不应该这么卡。

{{< image src="virtualbox01.png" caption="显存和3D加速设置" width="100%" height="100%" >}}
{{< image src="virtualbox02.png" caption="内存设置" width="100%" height="100%" >}}
{{< image src="virtualbox03.png" caption="处理器核心数" width="100%" height="100%" >}}

## 直接在物理机安装MAME模拟器
所以实在受不了了，就想着看`LINUX`下有没有类似的模拟器，结果还真被我找到了，它就是[MAME](https://www.mamedev.org/index.php)  
>这个模拟器在Windows平台下用的人也特别多，所以就选它了

MAME在`ArchLinux`安装特别方便，用如下命令即可
```bash
sudo pacman -S mame
sudo pacman -S mame-tools
```

安装后可以进行一些基础配置，在终端输入`mame`启动

你可以按`tab`切换到`Configure Options`上，也可以用鼠标点
{{< image src="mame01.png" caption="Configure Options" width="100%" height="100%" >}}

在这里你可以配置`UI`，包括`字体`，`语言`等
{{< image src="mame02.png" caption="UI设置" width="100%" height="100%" >}}
{{< image src="mame03.png" caption="字体设置" width="100%" height="100%" >}}

你还可以配置`视频选项`
{{< image src="mame04.png" caption="视频选项" width="100%" height="100%" >}}

配置`全局的输入选项`，我用的摇杆，你可以根据你的需要设置
{{< image src="mame05.png" caption="输入设置" width="100%" height="100%" >}}
{{< image src="mame06.png" caption="输入设置" width="100%" height="100%" >}}

## 要玩任何游戏，你还需要对应游戏的rom

MAME 模拟器的默认`ROMS`位置在`~/.mame/roms` 你只需要把你的`rom`放入这个目录即可

{{< image src="roms.png" width="100%" height="100%" >}}

{{< admonition >}}
需要注意的是，玩拳皇之类的游戏，需要一个`neogeo.zip`文件。  
这个文件可以去网上下载，放入`roms`目录就可以了
{{< /admonition >}}

然后 `mame rom名字`即可运行游戏，比如

```bash
mame kof97
```

然后你就可以愉快的玩耍了，这可比用虚拟机爽多了，祝你玩的开心。
{{< image src="running01.png" caption="Rom" width="100%" height="100%" >}}
{{< image src="running02.png" caption="Rom" width="100%" height="100%" >}}

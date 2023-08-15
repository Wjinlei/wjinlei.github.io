# DEB包的制作方法


>想要制作`deb`包，有多种方法，这里只说我认为最简单的方法`dpkg-deb -b`来生成`deb`包

<!--more-->

### 原理
原理是将要打包进`deb`包中的所有文件复制到一个`根目录`中，然后在编写`控制脚本`，最后一起打包生成

{{< admonition >}}
我们把这个`根目录`路径保存到一个变量中，这里假设为`${buildroot}`它的值是`~/buildroot`。  
然后，要打包的文件以这个`根目录`为开始，保持和系统一致的路径，例如，你这个`deb`包安装后要释放一个启动脚本到系统的`/etc/init.d/`目录下，
那么你需要在这个`根目录`中创建相应的目录层级，然后将文件复制到这个目录下。例如：`~/buildroot/etc/init.d`
{{< /admonition >}}


1. 然后我们还需要编写`~/buildroot/DEBIAN/contorl`文件，这是`最重要`的文件，它描述了这个`包的信息`

```bash
Package: helloworld        # 软件包名字
Version: 1.0.0             # 软件包版本
Section: unkown            # 软件包的分类 https://www.debian.org/doc/debian-policy/ch-archive.html#s-subsections
Priority: optional         # 软件包的优先级，这里一般都是 optional 表示软件包是可选的
Architecture: amd64        # 软件包的架构
Depends: zlib1g-dev        # 软件包依赖哪个软件包，多个用","号分隔,多行用"\"号分隔
Maintainer: Jerry Wang[1976883731@qq.com] # 软件包维护者
Description: nginx build by hws # 软件包描述
Homepage: https://www.hws.com   # 软件包主页
```

2. 下面四个操作是可选的
   - 编写(安装前执行的脚本)`DEBIAN/preinst`
   - 编写(安装后执行的脚本)`DEBIAN/postinst`
   - 编写(卸载前执行的脚本)`DEBIAN/prerm`
   - 编写(卸载后执行的脚本)`DEBIAN/postrm`

3. 最后执行 `dpkg-deb -b` 打包文件
```bash
dpkg-deb -b ${buildroot} helloworld-1.0.0-linux-amd64.deb
```

### 参考
[主机大师deb包参考脚本](https://github.com/Wjinlei/lanmp_debbuild)

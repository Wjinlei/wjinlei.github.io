# RPM包的制作方法


>要制作`RPM`包，我们需要编写`.spec`文件，然后安装`rpm-build`为我们编译并生成`rpm`包

<!--more-->

### 步骤
1. 安装`rpm-build`
2. 创建目录结构
```bash
mkdir -p ~/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS}
```
3. 将要编译的源码包下载到`SOURCES`目录
4. 编写`.spec`文件<br/>
   `.spec`文件建议放在`SPECS`目录中<br/>
   下面是`主机大师`中`pure-ftpd`软件的rpm包`.spec`文件<br/>

```bash
    cat > ~/rpmbuild/SPECS/pure-ftpd.spec << EOF
Name:           pure-ftpd                          # 软件包名称
Version:        1.0.49                             # 版本
Release:        1%{?dist}                          # 不用管,照写
Summary:        pure-ftpd 1.0.49                   # 简介

Group:          Applications/Internet              # 软件包分类
License:        GPLv3+                             # 协议
URL:            https://www.hws.com                # 软件包主页
Packager:       hws                                # 维护者
Source0:        ${pureftpd_filename}.tar.gz        # 编译软件包时依赖的源码包名称，就是你放入`SOURCES`目录中的软件包

BuildRoot:      %_topdir/BUILDROOT                 # 编译软件包时以哪个目录为根，这里表示以`BUILDROOT`为根
BuildRequires:  gcc,make                           # 编译前依赖哪些包
Requires:       openssl-devel,zlib-devel           # 安装时依赖哪些包

%description                                       # 描述
pure-ftpd 1.0.49 build for hws.com

%prep                                              # 编译前的操作，这里一般做准备工作，例如解压源码包
tar zxf \$RPM_SOURCE_DIR/${pureftpd_filename}.tar.gz

%build                                             # 编译阶段，这里一般写`configure`中的编译参数
cd ${pureftpd_filename}
./configure --prefix=${pureftpd_location} \
--with-puredb \
--with-quotas \
--with-cookie \
--with-virtualhosts \
--with-diraliases \
--with-sysquotas \
--with-ratios \
--with-altlog \
--with-paranoidmsg \
--with-shadow \
--with-welcomemsg \
--with-throttling \
--with-uploadscript \
--with-language=english \
--with-ftpwho \
--with-tls

make %{?_smp_mflags}

%install    # 安装阶段，你要把什么东西释放到系统，就通过install指令安装到`BUILDROOT`目录，因为有些东西不是编译时产生的
cd ${pureftpd_filename}
make install DESTDIR=%{buildroot}
install -D -m 0755 \$RPM_SOURCE_DIR/pure-ftpd \$RPM_BUILD_ROOT/etc/init.d/pure-ftpd
install -D -m 0644 \$RPM_SOURCE_DIR/pure-ftpd.conf \$RPM_BUILD_ROOT/${pureftpd_location}/etc/pure-ftpd.conf
install -D -m 0600 \$RPM_SOURCE_DIR/pureftpd.passwd \$RPM_BUILD_ROOT/${pureftpd_location}/etc/pureftpd.passwd
install -D -m 0600 \$RPM_SOURCE_DIR/pureftpd.pdb \$RPM_BUILD_ROOT/${pureftpd_location}/etc/pureftpd.pdb
install -D -m 0600 \$RPM_SOURCE_DIR/pure-ftpd.pem \$RPM_BUILD_ROOT/etc/ssl/private/pure-ftpd.pem
install -D -m 0644 \$RPM_SOURCE_DIR/README \$RPM_BUILD_ROOT/${pureftpd_location}/var/run/README

%post
chkconfig --add pure-ftpd >/dev/null 2>&1            # 安装后阶段
/etc/init.d/pure-ftpd start

%preun                                               # 卸载前阶段
chkconfig --del pure-ftpd >/dev/null 2>&1
/etc/init.d/pure-ftpd stop

%files                                               # 指定哪些文件会被释放到系统，这些文件都是再`BUILDROOT`中的
${pureftpd_location}
/etc/init.d/pure-ftpd
/etc/ssl/private/pure-ftpd.pem

%doc

%clean                                               # 编译后的清理工作
rm -fr %{buildroot}
EOF
```

5. 编译并生成`rpm`包
```bash
rpmbuild -bb ~/rpmbuild/SPECS/pure-ftpd.spec
```

# pyenv Python多版本管理工具的使用

[pyenv](https://github.com/pyenv/pyenv) 是一个`Python`多版本管理工具，使用它可以最大程度的避免你弄坏系统的`Python`<br/>

<!--more-->

## 安装
安装`pyenv`
```bash
curl https://pyenv.run | bash
```

安装`pyenv-virtualenv`
```bash
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv
```
{{< admonition tip "小提示">}}
`pyenv-virtualenv`是一个`pyenv`的插件，它提供了管理`Python`环境的功能，使用它你可以启用一个独立的`Python`环境，在这个环境中的`Python`版本和依赖均不受外部影响。<br/>
{{< /admonition >}}

## 配置环境变量
在你的`shell`配置文件中，添加如下配置
```bash
export PYENV_VIRTUALENV_DISABLE_PROMPT=1
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
if command -v pyenv >/dev/null 2>&1; then
    eval "$(pyenv init --path)"
    eval "$(pyenv virtualenv-init -)"
fi
```
{{< admonition >}}
`curl https://pyenv.run | bash`安装`pyenv`时，可能安装脚本已经帮助配置好了，你可以注意对比一下。
{{< /admonition >}}

## 命令参考
列出可用的`Python`版本
```bash
pyenv install --list
```

安装指定版本的`Python`
```bash
pyenv install 3.9.5
```

卸载指定版本的`Python`
```bash
pyenv uninstall 3.9.5
```

查看当前已安装的`Python`版本
```bash
pyenv versions
```

查看当前激活的`Python`版本
```bash
pyenv version
```

设置全局`Python`版本
```bash
# 会写入~/.pyenv/version
pyenv global 3.9.5 2.7.6 # 可以指定多个版本
```

设置本地`Python`版本
```bash
# 会写入当前目录.python-version
pyenv local 3.9.5 2.7.6 # 可以指定多个版本
```

设置shell`Python`版本
```bash
pyenv shell 3.9.5
```

创建虚拟环境
```bash
pyenv virtualenv 3.9.5 my-virtual-env-3.9.5 # 创建一个3.9.5版本的虚拟环境`my-virtualenv-env-3.9.5`是虚拟环境的名称
```

列出虚拟环境
```bash
pyenv virtualenvs
```

激活虚拟环境
```bash
pyenv activate my-virtualenv-env-3.9.5
```

取消虚拟环境
```bash
pyenv deactivate
```

删除虚拟环境
```bash
pyenv uninstall my-virtualenv-env-3.9.5
# or
pyenv virtualenv-delete my-virtualenv-env-3.9.5
```


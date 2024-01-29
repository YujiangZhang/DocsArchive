# windows

## ISO

- [Windows10](https://www.microsoft.com/zh-cn/software-download/windows10ISO)（其他版本可切换）
- 在 windows 系统下制作系统盘可以避免很多问题



## powershell 默认位置

**获得配置文件路径**

```]
$PROFILE
```

**创建配置文件**

```powershell
New-Item -Path $PROFILE -ItemType File -Force
```

**编辑配置**

```powershell
notepad $PROFILE
```

内容为

```powershell
Set-Location Z:
```



## [Git](https://git-scm.com/downloads)



## nvm

### 安装 nvm

[Github 地址](https://github.com/coreybutler/nvm-windows)，重装、更新或者卸载时，请查看官网说明

> 如果 npm 或相关命令无效，需要再设置 node 的环境变量



### 查看 node

```shell
$ nvm list
$ nvm list installed # 同 list, 查看已安装版本
$ nvm list available # 查看可安装版本号
```



### 安装 node

```shell
$ nvm install 版本
$ nvm list
$ nvm use 版本
# nvm install latest 安装最新版本
# 安装后直接查看版本然后使用 use
```



### 切换 node 版本

```shell
$ nvm use 版本
```



### 查看 node 版本

```shell
$ node v
```



### 卸载 node 版本

```shell
$ nvm uninstall 版本
```



## 系统执行策略更改

> npm 的全局包需要开启

```shell
set-ExecutionPolicy RemoteSigned
```



## yrm

```shell
# 失败则查看权限
$ npm install -g yrm
```

```shell
$ yrm -h
Usage: yrm [options] [command]

  Commands:

    ls                           列出所有的源
    use <registry>               切换使用的源
    add <registry> <url> [home]  增加一个源
    del <registry>               删除一个源
    home <registry> [browser]    在配置的浏览器打开源的主页
    test [registry]              展示一个或所有源的响应速度
    help                         Print this help

  Options:

    -h, --help     output usage information
    -V, --version  output the version number
```



## yarn

```shell
npm install -g yarn
```



## [7-Zip](https://7-zip.org/)



## [Geek Uninstaller](https://geekuninstaller.com/)



## [v2rayN](https://github.com/2dust/v2rayN)

> git 如果超市，检查 `sh -vT git@github.com`，修改代理，注意端口
>
> ```shell
> $ git config --global http.proxy "127.0.0.1:端口"
> $ git config --global https.proxy "127.0.0.1:端口"
> ```
>
> 



## [Snipaste](https://zh.snipaste.com/)



## [Typora](https://typoraio.cn/)



## [Python](https://www.python.org/downloads/)



## pip与venv

> Python官网：[使用 pip 和虚拟环境安装包](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment)



### pip

#### 换源

> 使用帮助：[清华源](https://mirrors.tuna.tsinghua.edu.cn/help/pypi/)

#### 更新

建议：

```
python -m pip install --upgrade pip
```

不建议：

```shell
pip install pip -U
```

可能会失败，导致 pip 丢失，可

```shell
python -m ensurepip
```

升级失败，则使用镜像站升级 pip

```shell
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pip -U
```

更改默认配置

```
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

临时使用

```powershell
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```



### venv

> 参数 env 为虚拟环境的名称



#### 创建虚拟环境

```powershell
python -m venv env
```



#### 启动

```powershell
./env/Scripts/activate
```



#### 退出

```powershell
deactivate
```


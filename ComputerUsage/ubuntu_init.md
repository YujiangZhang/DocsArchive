# ubuntu

## ISO

[Ubuntu](https://cn.ubuntu.com/download)



## 说明

可能会遇到：

- 没有权限时，可以：
  - 换源
    - 已经换过源，就设置网络代理
  - 网络代理
    - 代理后重新打开一个终端，让其生效
  - 手动安装
- 注意 shell 使用的如果是 zsh，则配置则在 ~/.zshrc 中

## 网络代理

查看是否生效，如果生效，可以看到代理服务器的地址和端口

```bash
echo $http_proxy
```

设置代理后，重新打开一个终端，使其生效。

## 换源

备份

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
```

换源，选择版本操作

[Ubuntu 软件仓库镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)
更新软件包列表，以使用最新的源

```bash
sudo apt update
```

## curl 或 wget

可以进行网络请求与下载等操作。

安装

```bash
sudo apt install curl
curl --version

sudo apt install wget
```

## zsh

如果安装了 zsh ，之后的配置 `.bashrc` 换为 `.zshrc`

安装

```bash
sudo apt install zsh
```

主题和插件：Oh My Zsh

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

安装完毕后，会有使用默认 sehll 的提示，y 确认后输入密码即可。

切换到 Zsh，重启就可以为默认 shell。

```bash
chsh -s $(which zsh)
```



## GIt

官网或自带



## Github ssh

```bash
ssh-keygen -t ed25519 -C "lingyou.ly@outlook.com"
```

```bash
cat ~/.ssh/id_ed25519.pub
```



## 传输文件到服务器

```bash
scp /本地/文件的/路径 username@远程服务器IP地址:/目标/目录/路径
```





## nvm

> [nvm](https://github.com/nvm-sh/nvm)

由 nvm 安装 node，并管理。

可以在 Gitbub 上按照其他方式安装。

手动安装

```bash
mkdir ~/.nvm
git clone https://github.com/nvm-sh/nvm.git ~/.nvm
```

添加配置

```bash
vim ~/.bashrc
```

添加以下配置

```bash
# This loads nvm
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

### nvm 常用命令

```markmap
- 安装 node
  - 安装最新版本
    - ```bash
      nvm install node
```
  - 查看可以安装的版本
    - ```bash
      nvm ls-remote
      ```
  - 安装特定版本
    - ```bash
      nvm install xx.xx.x
      ```
- 设置默认版本
  - ```bash
    nvm alias default node
    ```
- 切换 node 版本
  - ```bash
    nvm use node
    ```
- 查看已安装
  - ```bash
    nvm ls
    ```
    
    
    



## 源管理

```bash
npm install -g yrm
```



```bash
yrm ls

yrm use <registry>
```





## pyenv
```
> [pyenv](https://github.com/pyenv/pyenv)

自动安装，可能需要网络代理

```bash
curl https://pyenv.run | bash
```

配置

```bash
vim ~/.bashrc
```

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

### pyenv 常用命令

```markmap
- 安装 Python
  - 查看可以安装的版本
    - ```bash
      pyenv install --list
```
  - 安装特定版本
    - ```bash
      pyenv install 3.9.7
      ```
- 切换 Python 版本
  - 切换全局 python 版本
    - ```bash
      pyenv global 3.9.7
      ```
  - 切换本地项目的版本
    - 将在项目目录中创建名为 `.python-version` 的文件
    - ```bash
      pyenv local 3.9.7
      ```
  - 在当前终端会话中切换到特定版本
    - ```bash
      pyenv shell 3.9.7
      ```
- 查看已安装的版本
  - ```bash
    pyenv versions
    ```
- 卸载 Python 版本
  - ```bash
    pyenv uninstall 3.9.7
    ```
```

```



## nginx

```bash
sudo apt install nginx
```

```bash
sudo systemctl start nginx
sudo systemctl reload nginx
sudo systemctl status nginx
```

配置 并 配置 ssl 证书

```bash
sudo mkdir /etc/nginx/ssh
# 移动证书到该文件夹，也可以自定义路径

sudo vim /etc/nginx/sites-available/yuqicode
# 在自定义配置文件中配置，可域名文件夹
```

```
server {
    listen 80;
    server_name yuqicode.cn;

    # Redirect HTTP to HTTPS
    location / {
        return 301 https://$host$request_uri;
    }
}

server {
    listen 443 ssl;
    server_name yuqicode.cn;

    ssl_certificate /etc/nginx/ssl/yuqicode.cn_bundle.crt;
    ssl_certificate_key /etc/nginx/ssl/yuqicode.cn.key;

    location / {
        root /home/ubuntu/yuqicode-vue/dist;
        index index.html;
    }
}
```

创建链接使用该配置

```bash
sudo ln -s /etc/nginx/sites-available/yuqicode /etc/nginx/sites-enabled/

# 禁用
# sudo rm /etc/nginx/sites-enabled/yuqicode

# 禁用默认
sudo unlink /etc/nginx/sites-enabled/default

# 恢复默认
# sudo ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/
```

测试 nginx 配置文件

```bash
sudo nginx -t
```

通过测试则重新加载

```bash
sudo systemctl reload nginx
```



### 相关权限

这里列出权限问题：

```bash
# 确保 Vue.js 项目的文件和目录具有适当的权限
sudo chmod -R 755 /home/ubuntu/yuqicode-vue/dist/

# 确保 Vue.js 项目的文件和目录的属主和属组设置为 Nginx 使用的用户和组
sudo chown -R www-data:www-data /home/ubuntu/yuqicode-vue/dist/

# 确保 Nginx 用户（通常是 www-data）具有读取项目文件和证书的权限
sudo usermod -aG ubuntu www-data

# 确保 /home/ubuntu/yuqicode-vue/dist/ 目录以及其上层目录都不具有特殊权限或锁定标志
lsattr /home/ubuntu/yuqicode-vue/dist/

sudo systemctl reload nginx
```




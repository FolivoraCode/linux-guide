# Linux Mint 配置向导及应用
## 基本配置

### 联网

1. 锐捷官方客户端

   ```bash
   sudo chmod +x ./rjsupplicant.sh
   sudo ./rjsupplicant.sh --help # 配置使用
   ```

2. Mentohust

   安装 [mentohust_0.3.4-1_amd64.deb](https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/mentohust/mentohust_0.3.4-1_amd64.deb) 包。

   Mentohust 使用 `notify-osd` `libnotify-dev` 提供气泡提示。关于通知的文档：https://wiki.archlinux.org/index.php/Desktop_notifications

   ```bash
   # 修复提示 “！！打开libnotify失败，请检查是否已安装该库文件。”
   sudo ln -s /usr/lib/x86_64-linux-gnu/libnotify.so.4.0.0 /usr/lib/libnotify.so.1
   ```

   配置文件位置 `/etc/mentohust.conf`:

   组播地址：标准

   DHCP 方式：二次认证

### 终端

安装 zsh:

```bash
sudo apt-get install zsh
```

切换默认 zsh:

```bash
chsh -s /bin/zsh
```

安装 `oh-my-zsh`:

```bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

配置文件 `~/.zshrc`:

```bash
# 定义 zsh 主题
ZSH_THEME="ys"

# 设置别名
alias sudo="sudo "                # 授予 sudo 别名权限
alias rj="mentohust"              # 联网
alias qrj="mentohust -k"          # 退出联网
# alias xl="docker start xware"   启动讯雷下载容器
# alias qxl="docker stop xware"   停止讯雷远程下载容器
```

### 字体

下载符号字体解决 wps 符号字体缺失：

[symbol-fonts_1.2_all.deb](https://pan.baidu.com/share/link?uk=505215462&shareid=3369982571)

下载全套 Windows 字体：

[winfonts_1.3_all.deb](https://pan.baidu.com/share/link?uk=505215462&shareid=1223565760)

同时使用 Infinality 优化字体渲染：

> 参考文章：http://www.webupd8.org/2013/06/better-font-rendering-in-linux-with.html

```bash
sudo add-apt-repository ppa:no1wantdthisname/ppa
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install fontconfig-infinality
```

设置风格为 `Infinality`：

```bash
sudo bash /etc/fonts/infinality/infctl.sh setstyle
```

设置渲染风格：

```bash
# 修改 USE_STYLE 为 UBUNTU
sudo vim/etc/profile.d/infinality-settings.sh
```

启用 `Hinting full`。

## 应用软件

### 浏览器

1. Chrome

   ```bash
   wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
   ```


2. Firefox Dev

   ```bash
   # 使用 Umake 安装
   umake web firefox-dev 
   ```

### 编辑器

Visual Studio Code - https://code.visualstudio.com/

### Markdown 写作

```bash
# optional, but recommended
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE
# add Typora's repository
sudo add-apt-repository 'deb https://typora.io ./linux/'
sudo apt-get update
# install typora
sudo apt-get install typora
```

### 效率

1. 白噪音 `ANoise`:

   ```bash
   sudo add-apt-repository ppa:costales/anoise
   sudo apt-get update
   sudo apt-get install anoise
   ```

2. 剪贴板管理 `Diodon`:

   ```bash
   sudo add-apt-repository ppa:diodon-team/stable
   sudo apt-get update
   sudo apt-get install diodon
   ```

3. 截图 `Shutter`:

   ```bash
   sudo apt-get install shutter
   ```

### 开发环境

1. [NVM](https://github.com/creationix/nvm)

2. [Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/)

3. Umake

   Umake 是 Ubuntu 官方的一款用来安装开发环境及开发工具的工具，同样在 Linux Mint 下可用。预装已有 Umake 工具，但支持较少，通过 ppa 来升级。

   ```bash
    $ sudo add-apt-repository ppa:ubuntu-desktop/ubuntu-make
    $ sudo apt-get update
    $ sudo apt-get upgrade
   ```

### 同步工具

1. [坚果云](https://www.jianguoyun.com/)

2. [Dropbox](https://www.dropbox.com/)

   安装过程中需要联网下载，故需使用 `Proxychains` 来启动安装。

   Dropbox 默认目录在 `~/Dropbox` 进行同步，备份目录只需要创建一个软链接到此目录即可。

### 代理工具

1. Shadowsocks

   推荐使用 [Shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5) 来设置。

   ```bash
   sudo add-apt-repository ppa:hzwhuang/ss-qt5
   sudo apt-get update
   sudo apt-get install shadowsocks-qt5
   ```

2. Proxychains

   代理终端命令中的网络请求。在源中安装：

   ```bash
   sudo apt-get install proxychains
   ```

   然后配置文件 `/etc/proxychains.conf`:

3. [Lantern](https://getlantern.org/)

### 文档阅读

1. [Zeal](https://zealdocs.org/)

   ```bash
   $ sudo add-apt-repository ppa:zeal-developers/ppa
   $ sudo apt-get update
   $ sudo apt-get install zeal
   ```

2. Calibre

   ```bash
   sudo -v && wget -nv -O- https://raw.githubusercontent.com/kovidgoyal/calibre/master/setup/linux-installer.py | sudo python -c "import sys; main=lambda:sys.stderr.write('Download failed\n'); exec(sys.stdin.read()); main()"
   ```


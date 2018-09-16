[how_to_install_zsh_and_oh_my_zsh_debian](https://www.reddit.com/r/debian/comments/72wp4t/how_to_install_zsh_and_oh_my_zsh_debian/)

[*How to install the zsh shell in Linux; how to set it as a default login shell*](http://linuxg.net/how-to-install-zsh-shell-how-to-set-it-as-a-default-login-shell/)  
[**How to Setup ZSH and Oh-my-zsh on Linux**](https://www.howtoforge.com/tutorial/how-to-setup-zsh-and-oh-my-zsh-on-linux/)  

[Installing Oh-My-Zsh on Debian-Based Systems](http://www.hildeberto.com/2018/02/oh-my-zsh.html)  

## [Installing ZSH](https://github.com/robbyrussell/oh-my-zsh/wiki/Installing-ZSH) - [the easy way](https://gist.github.com/derhuerst/12a1558a4b408b3b2b6e)

执行 `cat /etc/shells` 查看 raspbian 支持的 shells：

```shell
pi@raspberrypi:~ $ cat /etc/shells
# /etc/shells: valid login shells
/bin/sh
/bin/dash
/bin/bash
/bin/rbash
/usr/bin/screen
```

执行 `echo $SHELL` 查看 raspbian 当前用户的 login shell：

```shell
pi@raspberrypi:~ $ echo $SHELL
/bin/bash
```

### Download and install

For **Debian** based distros(Ubuntu): `$ sudo apt-get install zsh`

For **Red Hat** based distros(CentOS): `$ sudo yum install zsh`

For **Suse** based distros: `$ sudo zypper install zsh`

raspbian 安装 zsh 后，执行 `zsh --version`：

```shell
pi@raspberrypi:~ $ zsh --version
zsh 5.3.1 (arm-unknown-linux-gnueabihf)
```

重新执行 `cat /etc/shells` 查看 raspbian 支持的 shells：

```shell
pi@raspberrypi:~ $ cat /etc/shells
# /etc/shells: valid login shells
/bin/sh
/bin/dash
/bin/bash
/bin/rbash
/usr/bin/screen
/bin/zsh
/usr/bin/zsh
```

可以发现其中已经新增了 `/bin/zsh`（`/usr/bin/zsh`），如果没有可以执行以下命令，将 `/usr/bin/zsh` 添加到 `/etc/shells` 文件中：

```shell
sudo -s 'echo /usr/bin/zsh >> /etc/shells'
```

### set zsh as the default login shell

This works on Fedora / Debian / OpenSuse: `chsh -s /bin/zsh user`

```shell
$ sudo chsh -s /bin/zsh yoda
$ finger yoda | grep zsh
Directory: /home/yoda Shell: /bin/zsh
```

> `user` 可改为 `root` 或不填。

If you want to customize the Z-shell, edit **`~/.zshrc`**: `vim ~/.zshrc`

如果 `/etc/shells` 中没有 zsh，可以复合调用以下命令完成配置切换：

```shell
sudo -s 'echo /usr/bin/zsh >> /etc/shells' && chsh -s /usr/bin/zsh
```

## use zsh

在 raspbian 默认启动的 bash 中执行 `zsh` 即可新建子 shell。

首次启动 zsh 将提示 zsh-newuser-install：

```shell
Last login: Sun Sep 16 14:00:48 2018 from fe80::810:3bb0:26ab:bf3a%wlan0
This is the Z Shell configuration function for new users,
zsh-newuser-install.
You are seeing this message because you have no zsh startup files
(the files .zshenv, .zprofile, .zshrc, .zlogin in the directory
~).  This function can help you with a few settings that should
make your use of the shell easier.

You can:

(q)  Quit and do nothing.  The function will be run again next time.

(0)  Exit, creating the file ~/.zshrc containing just a comment.
     That will prevent this function being run again.

(1)  Continue to the main menu.

(2)  Populate your ~/.zshrc with the configuration recommended
     by the system administrator and exit (you will need to edit
     the file by hand, if so desired).

--- Type one of the keys in parentheses ---
```

按下 0，将自动创建包含一句注释的空 `~/.zshrc` 配置文件。

```shell
raspberrypi% cat .zshrc
# Created by newuser for 5.3.1
```

下次再启动，不会再提示以上内容。

执行 `zsh --version` 或 `echo $ZSH_VERSION` 可查看 zsh 版本：

```shell
raspberrypi% echo $ZSH_NAME
zsh

raspberrypi% echo $ZSH_VERSION
5.3.1
```

### config zshrc

```shell
# 设置随机主题
# Set name of the theme to load
ZSH_THEME="random" #"robbyrussell"

# 历史命令增加时间戳
# time stamp shown in the history command output.
HIST_STAMPS="mm/dd/yyyy"

# 设置开启的插件
# Which plugins would you like to load?
plugins=(
  git
  debian
  svn
  git
  copydir
  z
  wd
  encode64
  extract
  jsontools
  colored-man-pages
  thefuck
  #sublime
  #vscode
  #marked2
  node
  #httpie
  web-search
)

# 设置环境变量
# You may need to manually set your language environment
export LANG=en_US.UTF-8
export LC_CTYPE=en_US.UTF-8

# 设置默认编辑器
# Preferred editor for local and remote sessions
if [[ -n $SSH_CONNECTION ]]; then
   export EDITOR='vim'
else
   export EDITOR='mvim'
fi
```

### source zshrc

配置完 `~/.zshrc` 后，执行 `source .zshrc` 重新加载 zshrc 配置重启 zsh：

```shell
raspberrypi% source .zshrc
thefuck is not installed, you should "pip install thefuck" or "brew install thefuck" first.
See https://github.com/nvbn/thefuck#installation
[oh-my-zsh] Random theme '/home/pi/.oh-my-zsh/themes/skaro.zsh-theme' loaded...
21 ~  »
```

提示需要安装 thefuck，用 pip 或 apt 安装完 thefuck 后，在 `~/.zshrc` 末尾添加一句 `eval $(thefuck --alias)` 重新 source 重启即可使用 **`fuck`** 命令。

## plugins

分别执行以下命令下载第三方插件 `ls`、`zsh-autosuggestions` 和 `zsh-syntax-highlighting`：

```shell
git clone https://github.com/zpm-zsh/ls $ZSH_CUSTOM/plugins/ls
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

将它们配置到 `~/.zshrc` 中的 plugins 数组中，执行 `source ~/.zshrc` 即可重新加载配置生效。
